

```
num_threads, (num_elem / 2));

// Invoke the kernel
odd_even_sort_ptr_kernel_gmem<<<num_blocks, num_threads>>>(data_gpu, num_elem);

cuda_error_check("Error Invoking kernel*",
        "odd_even_sort_gpu_kernel_gmem");

// Copy back to CPU memory space
CUDA_CALL(cudaMemcpy(data_cpu, data_gpu, size_in_bytes, cudaMemcpyDeviceToHost));

// Free memory on the device
CUDA_CALL(cudaFree(data_gpu));

print_array(0, data_cpu, num_elem);
```

关于这段代码，你脑海中应该有一个疑问：块边界会发生什么？让我们来看看使用一个块和两个块、数据集足够小以便在此打印的结果：

```
Invoking Odd Even sort with 1 blocks of 8 threads (8 active)
Run 000: 00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15
Test passed

and

Invoking Odd Even sort with 2 blocks of 4 threads (8 active)
Run 000: 08 09 10 11 12 13 14 15 00 01 02 03 04 05 06 07
Test failed
```

注意在第二个输出中，排序仅在块内部发生。右侧的值需要传播到左侧，反之亦然。然而，由于块不重叠，它们无法做到这一点。显而易见的解决方案是重叠块，但这并不是一个理想的解决方案。

CUDA 的设计允许块以任何顺序运行，在单个内核运行内没有跨块同步的机制。可以通过发出多个内核来在块之间同步，但这种机制仅在同步步骤较少时效果良好。在这个内核中，我们需要在每次迭代时重叠块。这将失去所有局部性，因为现在两个 SM 需要共享同一数据集。我们还需要一个全局内存原子操作或归约操作来跟踪是否有任何块执行了交换，并且必须继续发出内核，直到没有任何块发生交换——这涉及大量的主机交互。这不是一个好的选择。

因此，我们只剩下大多数分解为块的排序中常见的两种选择。要么预排序输入列表，使列表 N<sub>i-1</sub> 中的值小于 N<sub>0</sub>，而 N<sub>0</sub> 大于 N<sub>1</sub>，这是我们在示例排序中使用的解决方案；要么合并 N 个独立列表，即我们之前也研究过的归并排序问题。

## 归约

归约在并行编程中被广泛使用。我们将探讨执行归约的许多方式之一，以了解哪种方法在各种计算平台上产生最佳结果，并理解原因。

我们将首先计算 _N_ 个 32 位整数的和，约 4800 万个，以提供合理大小的数据集。在有如此多值的情况下，我们需要首先考虑的问题之一是溢出。如果我们将 0xFFFFFFFF 和 0x00000001 相加，那么对于 32 位数字就会出现溢出条件。因此，我们需要累加到 64 位数字。这带来了一些问题。首先，任何基于原子操作的累加都需要原子 64 位整数加法。不幸的是，这仅在共享内存中与计算 2.x 硬件支持，并在全局内存中从计算 1.2 硬件开始支持。

## 全局原子加法

让我们首先看看最简单的归约形式：

```
// Every thread does atomic add to the same
// address in GMEM
__global__ void reduce_gmem(const uint32 * const data,
u64 * const result,
const uint32 num_elements)
{
    const uint32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;
    if (tid < num_elements)
        atomicAdd(result, (u64) data[tid]);
}
```

在这个第一个示例中，每个线程从内存中读取一个元素，并将其添加到全局内存中的单个结果。虽然这非常简单，但可能是归约操作中最糟糕的形式之一。跨块原子操作意味着该值需要在所有 SM 之间共享。

在旧硬件中，这意味着物理写入全局内存。在计算 2.x 硬件中，这意味着维护一个在所有 SM 之间共享的 L2 缓存条目，并最终将其写入全局内存。我们看到的结果如下：

| | ID:0 GeForce GTX 470:GMEM 耗时 | ID:3 GeForce GTX 460:GMEM 耗时 |
|---|---|---|
| 处理 48 MB 数据，12M 个元素 | 197.84 ms | 164.28 ms |

我们这里将查看计算 2.x 设备，因为这些设备支持 64 位整数原子操作。

原子写入（即使写入 L2 缓存）的问题在于它们强制线程串行化。每个 SM 中有六个块，每个块 256 个线程，每个 SM 生成 1536 个线程。在 GTX470 上我们有 14 个 SM，总共 21,504 个活动线程。在 GTX460 上我们有 7 个 SM，总共 10,752 个活动线程。在单个全局内存单元上执行原子操作意味着我们创建了 10K 到 21K 线程的队列或串行化。每个线程都必须排队，每处理一个元素排队一次。这显然是一个糟糕的解决方案，即使它有些简单。

## 线程内的归约

我们可以通过在线程内执行部分归约来改善这种情况。我们可以非常简单地通过更改数据类型并调整内核来确保不越界来实现这一点。

```
// Every thread does atomic add to the same
// address in GMEM
__global__ void reduce_gmem_ILP2(const uint2 * const data,
u64 * const result,
const u32 num_elements)
{
const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;

if (tid < (num_elements>>1))
{
uint2 element = data[tid];

const u64 add_value = ((u64)element.x) +
((u64)element.y);

atomicAdd(result, add_value);
}
}
```

```
// Every thread does atomic add to the same
// address in GMEM
__global__ void reduce_gmem_ILP4(const uint4 * const data,
u64 * const result,
const u32 num_elements)
{
const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;

if (tid < (num_elements>>2))
{
uint4 element = data[tid];

const u64 add_value = ((u64)element.x) +
((u64)element.y) +
((u64)element.z) +
((u64)element.w);

atomicAdd(result, add_value);
}
}
```

在第一个示例中，我们每个线程处理两个元素，在第二个示例中处理四个元素，使用内置的向量类型 uint2 和 uint4。这产生了以下计时：

- ID:0 GeForce GTX 470:GMEM ILP2 耗时 98.96 ms
- ID:3 GeForce GTX 460:GMEM ILP2 耗时 82.37 ms
- ID:0 GeForce GTX 470:GMEM ILP4 耗时 49.53 ms
- ID:3 GeForce GTX 460:GMEM ILP4 耗时 41.47 ms

虽然这是一个巨大的减少，但我们并没有真正解决问题。我们所做的只是通过执行本地归约，将每个线程需要排队的次数减半或四分之一。这使总时间降至原来的大约一半和四分之一。然而，仍然有 5K 个线程的队列试图写入全局内存。

请注意，在本地执行加法时，我们将全局写入的数量减少了等于 ILP 级别的因子。然而，我们必须小心加法的执行方式。你可以这样写：

```
const u64 add_value = ((u64)element.x) + element.y + element.z + element.w;
```

在 C 中，表达式通常从左到右求值。左操作数的提升会导致右操作数的隐式提升。因此，你可能期望 element.x 被提升为无符号 64 位类型，并且由于 element.y 要添加到它，它也会被提升。由于 element.z 和 element.w 随后将被添加，你可能也期望这些被提升。然而，你是在像串行程序员一样思考。z 和 w 元素可以独立于 x 和 y 计算。PTX 代码正是如此执行的。由于 z 和 w 都没有被提升为 64 位值，加法是作为 32 位加法执行的，这可能导致溢出。

问题在于 C 允许在运算符满足交换律时以任何顺序求值。然而，由于你通常看到从左到右的求值，人们假设所有编译器都是这样工作的。这是 C 编译器之间的可移植性问题之一。当我们转向 GPU 这样的超标量处理器时，它会独立执行两组加法，以充分利用流水线。我们不希望它等待 18–22 个以上周期让第一个加法完成，然后串行地进行后续加法。

因此，编写此类加法的正确方式是：

```
const u64 add_value = ((u64)element.x) + ((u64)element.y) + ((u64)element.z) + ((u64)element.w);
```

在这里，每个值在加法发生之前都被转换为 64 位数字。然后，对于整数值，任何加法顺序都可以。请注意，对于浮点值，仅转换为双精度是不够的。由于浮点数的工作方式，将一个非常小的数字添加到一个非常大的数字会导致小数字被丢弃，因为浮点表示法没有足够的分辨率来保存这样的值。处理此类问题的最佳方法是首先对浮点值进行排序，并从最小的数字到最大的数字进行操作。

我们可以通过使用多个 uint4 元素并相应调整内核，将 ILP 技术进一步推进。

```
// Every thread does atomic add to the same
// address in GMEM
__global__ void reduce_gmem_ILP8(const uint4 * const data,
u64 * const result,
const u32 num_elements)
{
    const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;
    if (tid < (num_elements>>3))
    {
        const u32 idx = (tid * 2);
        uint4 element = data[idx];
        u64 value = ((u64)element.x) +
```

