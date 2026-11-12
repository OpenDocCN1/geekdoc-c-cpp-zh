

```
const u32 num_elements)
{
// Take the middle of the two sections
u32 size = (num_elements >> 1);
u32 start_idx = 0;
bool found = false;
do
{
    const u32 src_idx = (start_idx+size);
    const u32 test_value = src_data[src_idx];
    if (test_value == search_value)
        found = true;
    else
        if (search_value > test_value)
            start_idx = (start_idx+size);
    if (found == false)
        size >>= 1;
} while ( (found == false) && (size != 0) );
return (start_idx + size);
}
```

二分查找例程通过将 size 参数减小到零来工作。它返回搜索值应放置的索引或桶。

```cpp
// Single data point, atomic add to gmem
__global__ void count_bins_gpu_kernel5(
    const u32 num_samples,
    const u32 * const src_data,
    const u32 * const sample_data,
    u32 * const bin_count)
{
    const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;
    // Read the sample point
    const u32 data_to_find = src_data[tid];
    // Obtain the index of the element in the search list
    const u32 idx = bin_search(sample_data, data_to_find, num_samples);
    atomicAdd(&bin_count[idx],1);
}
__host__ TIMER_T count_bins_gpu(
    const u32 num_samples,
    const u32 num_elements,
    const u32 * const src_data,
    const u32 * const sample_data,
    u32 * const bin_count,
    const u32 num_threads,
    const char * prefix
{
    const u32 num_blocks = num_elements / num_threads;

    start_device_timer();

    count_bins_gpu_kernel5<<<num_blocks, num_threads>>>(num_samples, src_data,
                        sample_data, bin_count);
    cuda_error_check(prefix, "Error invoking count_bins_gpu_kernel5");

    const TIMER_T func_time = stop_device_timer();
    return func_time;
}
```

与选择样本的函数不同（该函数中最大线程数受样本数量限制），这里我们仅受源数组中元素数量的限制。因此，主机函数启动一个内核，该内核每个元素包含一个线程。

内核计算其元素，并以合并的方式从源数据集中读取它。在这里每块使用更多线程可以增加来自全局内存的读取带宽。

每次使用 warp 都会跳转到二分查找，经过不多的迭代后返回。对于随机元素列表，会出现一些线程分歧。然而，在更常见的大部分已排序列表的情况下，所有线程倾向于遵循相同的路径，因此在实践中造成的线程分歧很小。

当 warp 的所有线程从二分查找返回后，它们通过原子写入递增全局内存中 N 个桶之一的值。对全局内存的原子操作是保证完成且不中断的操作，无论是哪个 SM 上的哪个线程发起的操作。因此，我们可以安全地让许多线程写入同一地址。显然只有一个可以物理写入，因此任何值的冲突都会导致请求的串行化。

不幸的是，对于大部分已排序的列表，我们发现由于块是依次分配的，大多数活动块位于相似的内存区域。虽然这对局部性非常有利，但这也意味着所有线程都在写入时访问相同的内存区域。因此，对于已排序列表，我们会看到这种方法的速度下降，但不会太显著，稍后我们将看到。

## 前缀和

前缀和很有用，因为它可以用来创建一个值表，这些值用于索引具有变长记录的数组。在我们的例子中，每个桶的大小是可变长度，每个桶在内存中依次存储。因此，我们可以计算一个前缀和数组，然后使用数组元素 0 访问桶 0 的开头，使用数组元素 1 访问桶 1 的开头，以此类推。

CPU 上前缀和的代码非常简单：

```cpp
__host__ TIMER_T calc_bin_idx_cpu(const u32 num_samples,
                                  const u32 * const bin_count,
                                  u32 * const dest_bin_idx)
{
    const TIMER_T start_time = get_time();
    u32 prefix_sum = 0;

    for (u32 i = 0; i < num_samples; i++)
    {
        dest_bin_idx[i] = prefix_sum;
        prefix_sum += bin_count[i];
    }

    const TIMER_T end_time = get_time();
    return end_time - start_time;
}
```

这里我们只是遍历数组 `bin_count`，该数组包含每个桶中有多少个元素。前缀和从零开始，我们将迄今循环看到的桶计数之和存储到数组 `prefix_sum` 中。

这段代码和前缀和的主要问题是，乍一看它似乎是一个本质上是串行的问题。没有前一个值，你无法计算最后一个值。遍历所有元素的循环实际上是针对单处理器系统计算此问题的一种非常高效的方法。那么，如何以并行方式计算前缀和，以便我们可以利用不止一个 SM 呢？

事实证明，对于少量元素，这种简单的前缀和实现实际上非常快。但是，当样本元素数量变大（4096 以上）时，需要一种稍快且更复杂的方法。

可以通过将数组分割成若干块并对这些块计算前缀和来并行计算前缀和。每个前缀和块的端点被放入另一个数组中。然后对该数组原地再做一次前缀和。将此前缀和的结果添加到原始前缀和计算中的每个元素。这产生了一个我们可以轻松在 GPU 上使用的并行前缀和（图 6.25）。

对于前缀和块，我们将每块使用一个线程。由于每个线程处理相同数量的元素并只是循环迭代，因此没有线程分歧。但是，读取内存访问合并效果不佳，因为线程 0 将访问从零偏移量开始的地址，而线程 1 将访问从 `(NUM_SAMPLES/NUM_BLOCKS)` 偏移量开始的地址。

我们希望在多个 SM 上运行这段代码，这意味着需要创建多个块。我们需要一个中心同步点来执行前缀和。在所有块完成之前，这无法发生。因此，我们需要启动一个内核来执行初始前缀和，另一个内核来对结果执行前缀和，以及最后一个内核来执行加法步骤。

这实际上非常有益，因为它给了我们更改使用的块数和线程数的机会。虽然我们可能每个前缀和块使用一个线程，但加法内核的并行性仅受样本点数量的限制。因此，我们可以运行 `N` 个块，每个块 `M` 个线程，其中 `N x M` 是样本数量，从而最大限度地利用 GPU。

![](img/e0b192dbaf05f61ad420bee512a8c4e4_202_0.png)

图 6.25 并行前缀和。

与大多数更复杂的算法一样，存在一个权衡点，在此点更简单的算法更快。对于串行前缀和与分块前缀和，这个点大约在 4096 个样本点。我们可以进一步实现第一阶段中更复杂的前缀和，但除非我们有非常大的数据集，否则前缀和不会成为排序时间的关键因素。

```cpp
__global__ void calc_prefix_sum_kernel(
    const u32 *num_samples_per_thread,
    const u32 *const bin_count,
    u32 *const prefix_idx,
    u32 *const block_sum)
{
    const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;
    const u32 tid_offset = tid * num_samples_per_thread;
    u32 prefix_sum;

    if (tid == 0)
        prefix_sum = 0;
    else
        prefix_sum = bin_count[tid_offset-1];

    for (u32 i=0; i<num_samples_per_thread; i++)
    {
        prefix_idx[i+tid_offset] = prefix_sum;
        prefix_sum += bin_count[i+tid_offset];
    }
    // Store the block prefix sum as the value from the last element
    block_sum[tid] = prefix_idx[(num_samples_per_thread-1)*i+tid_offset];
}
```

首先，根据块和线程计算我们的 tid 编号。然后，根据线程将要计算前缀和的样本数量计算 tid_offset。对于第一个块，结果必须为零。对于其他块，我们包含桶计数的第一个元素。然后我们只是实现之前看到的代码，但添加 tid_offset 以读写适当的元素。

```cpp
__global__ void add_prefix_sum_total_kernel(
    u32 * const prefix_idx,
    const u32 * const total_count)
{
    const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;
    prefix_idx[tid] += total_count[blockIdx.x];
}
```

加法内核非常简单。程序只是计算线程的单独 tid 并使用它来索引目标数组。要添加的值取自块计数。此实现中隐含的假设是调用者调用 N 个线程，其中 N 是前一个内核中使用的每个线程的样本数量。我们显式地这样做，因为它允许使用 blockIdx.x（块编号）而无需访问线程索引。这使得获取操作落入统一常量缓存，并对线程块内的所有元素造成广播操作。

此外，我们还有一个简单的前缀和内核，用于处理少量元素的情况。并行版本因为需要执行额外的块前缀步骤、另一次加法以及同步，在这种情况下耗时更长。只有在块大小较大、我们可以更好地利用硬件时，才会看到更复杂版本的显著加速。

```cpp
__global__ void calc_prefix_sum_kernel_single(
    const u32 num_samples,
    const u32 * const bin_count,
    u32 * const dest_bin_idx)
{
    u32 prefix_sum = 0;
    for (u32 i=0; i<num_samples; i++)
    {
        dest_bin_idx[i] = prefix_sum;
        prefix_sum += bin_count[i];
    }
}
```

最后是对内核进行编排的主机函数：
