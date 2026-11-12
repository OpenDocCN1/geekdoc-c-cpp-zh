
((u64)element.y) +
((u64)element.z) +
((u64)element.w);
element = data[idx+1];
value += ((u64)element.x) +
((u64)element.y) +
((u64)element.z) +
((u64)element.w);
atomicAdd(result, value);
}
}

// 每个线程对GMEM中的同一
// 地址执行原子加

```cpp
__global__ void reduce_gmem_ILP16(const uint4 * const data,
                                  u64 * const result,
                                  const u32 num_elements)
{
    const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;
    if (tid < (num_elements >> 4))
    {
        const u32 idx = (tid * 4);

        uint4 element = data[idx];
        u64 value = ((u64)element.x) +
                    ((u64)element.y) +
                    ((u64)element.z) +
                    ((u64)element.w);

        element = data[idx + 1];
        value += ((u64)element.x) +
                 ((u64)element.y) +
                 ((u64)element.z) +
                 ((u64)element.w);

        element = data[idx + 2];
        value += ((u64)element.x) +
                 ((u64)element.y) +
                 ((u64)element.z) +
                 ((u64)element.w);

        element = data[idx + 3];
        value += ((u64)element.x) +
                 ((u64)element.y) +
                 ((u64)element.z) +
                 ((u64)element.w);

        atomicAdd(result, value);
    }
}
```

// 每个线程对GMEM中的同一
// 地址执行原子加

```cpp
__global__ void reduce_gmem_ILP32(const uint4 * const data,
                                  u64 * const result,
                                  const u32 num_elements)
{
    const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;

    if (tid < (num_elements >> 5))
    {
        const u32 idx = (tid * 8);

        uint4 element = data[idx];
        u64 value = ((u64)element.x) +
                    ((u64)element.y) +
                    ((u64)element.z) +
                    ((u64)element.w);

        element = data[idx + 1];
        value += ((u64)element.x) +
                 ((u64)element.y) +
                 ((u64)element.z) +
                 ((u64)element.w);

        element = data[idx + 2];
        value += ((u64)element.x) +
                 ((u64)element.y) +
                 ((u64)element.z) +
                 ((u64)element.w);

        element = data[idx + 3];
        value += ((u64)element.x) +
                 ((u64)element.y) +
                 ((u64)element.z) +
                 ((u64)element.w);

        element = data[idx + 4];
        value += ((u64)element.x) +
                 ((u64)element.y) +
                 ((u64)element.z) +
                 ((u64)element.w);

        element = data[idx + 5];
        value += ((u64)element.x) +
                 ((u64)element.y) +
                 ((u64)element.z) +
                 ((u64)element.w);

        element = data[idx + 6];
        value += ((u64)element.x) +
                 ((u64)element.y) +
                 ((u64)element.z) +
                 ((u64)element.w);

        element = data[idx + 7];
        value += ((u64)element.x) +
                 ((u64)element.y) +
                 ((u64)element.z) +
                 ((u64)element.w);

        atomicAdd(result, value);
    }
}
```

请注意，我们将数据加载与加法混合在一起。我们可以将所有加载移到函数开头。但是，请考虑每个 uint4 类型需要四个寄存器。因此，ILP32 示例仅为了保存单次读取迭代中的值就需要 32 个寄存器。此外，加法和最终写入还需要一些寄存器。如果使用过多寄存器，可调度的块数量将减少，或者内核会将寄存器溢出到“本地”内存。这种本地内存对 compute 2.x 设备是 L1 缓存，对 compute 1.x 设备是全局内存。这些 ILP 内核的结果如下所示：

```
ID:0 GeForce GTX 470:GMEM ILPB passed Time 24.83 ms
ID:3 GeForce GTX 460:GMEM ILPB passed Time 20.97 ms
ID:0 GeForce GTX 470:GMEM ILP16 passed Time 12.49 ms
ID:3 GeForce GTX 460:GMEM ILP16 passed Time 10.75 ms
ID:0 GeForce GTX 470:GMEM ILP32 passed Time 13.18 ms
ID:3 GeForce GTX 460:GMEM ILP32 passed Time 15.94 ms
```

可以看出，ILP 显著降低了执行时间，前提是不要过度使用。请注意，ILP32 解决方案实际上耗时更长。尽管相对于最简单的版本实现了 20 倍的加速，但我们仍未解决原子写入排队问题，只是减少了元素的总数。仍然有太多的原子写入（10–21 K）都在尝试写入同一个累加器。

## 减少块的数量

目前，我们调用 N 个块，其中 N 是问题大小，即 1200 万个元素（48 MB）除以每个块的线程数乘以每个块处理的元素数。最终我们得到 N 个原子写入，它们全部被串行化并造成瓶颈。

如果我们创建的块数量少得多，并大大增加每个块执行的工作量，就可以减少竞争的数量。但是，我们必须在不增加寄存器使用量的情况下做到这一点，而 ILP32 示例正是如此做的。这反过来又由于本地内存读写而导致了减速。

目前，我们启动 48 K 个块，但可以将其减少到 16、32、64、128 或 256 个块。然后，我们可以让每个线程遍历内存，将结果累积到寄存器中，仅在块完成时才写出结果。根据块的数量，这应该在 SM 之间产生相当好的内存引用局部性，从而充分利用内存带宽和 L2 缓存（如果存在）。

```cpp
// Every thread does atomic add to the same
// address in GMEM after internal accumulation
__global__ void reduce_gmem_loop(const u32 * const data,
                                 u64 * const result,
                                 const u32 num_elements)
{
    // Divide the num. elements by the number of blocks launched
    // ( 4096 elements / 256 threads ) / 16 blocks = 1 iter
    // ( 8192 elements / 256 threads ) / 16 blocks = 2 iter
    // ( 16384 elements / 256 threads ) / 16 blocks = 4 iter
    // ( 32768 elements / 256 threads ) / 16 blocks = 8 iter
    const u32 num_elements_per_block = (num_elements / blockDim.x) / gridDim.x;

    const u32 increment = (blockDim.x * gridDim.x);

    // Work out the initial index
    u32 idx = (blockIdx.x * blockDim.x) + threadIdx.x;

    // Accumulate into this register parameter
    u64 local_result = 0;

    // Loop N times depending on the number of
    // blocks launched
    for (u32 i = 0; i < num_elements_per_block; i++)
    {
        // If still within bounds, add into result
        if (idx < num_elements)
            local_result += (data[idx]);

        // Move to the next element in the list
        idx += increment;
    }

    // Add the final result to the GMEM accumulator
    atomicAdd(result, local_result);
}
```

第一项任务是计算每个线程需要对数据进行多少次迭代。参数 gridDim.x 保存启动的块数量。每个块由 blockDim.x 个线程组成。因此，我们可以计算出每个线程必须累积多少个数据元素。然后我们将这些值累积在 local_result 中，仅在块完成时才对全局内存执行一次写入。

这将竞争从线程级别降低到了块级别。由于我们只启动了几百个块，它们都需要同时写入的概率相当低。显然，随着块数量的增加，潜在的竞争也会增加。一旦我们用允许的最大块数加载了所有 SM，除非是为了工作负载均衡，否则再增加块数量的理由不大。

GTX460 或许是最糟糕的示例，因为只有 7 个 SM，每个 SM 有 6 个块，仅 42 个块就能使设备饱和。GTX470 需要 90 个块。因此，我们尝试从 49,152 个块开始，以 2 的幂递减到 16 个块，更少的块就足以完全填充 SM。这生成了以下结果：

```
ID:0 GeForce GTX 470:GMEM loop1 49152 passed Time 197.82 ms
ID:0 GeForce GTX 470:GMEM loop1 24576 passed Time 98.96 ms
ID:0 GeForce GTX 470:GMEM loop1 12288 passed Time 49.56 ms
ID:0 GeForce GTX 470:GMEM loop1 6144 passed Time 24.83 ms
ID:0 GeForce GTX 470:GMEM loop1 3072 passed Time 12.48 ms
ID:0 GeForce GTX 470:GMEM loop1 1536 passed Time 6.33 ms
ID:0 GeForce GTX 470:GMEM loop1 768 passed Time 3.35 ms
ID:0 GeForce GTX 470:GMEM loop1 384 passed Time 1.62 ms
ID:0 GeForce GTX 470:GMEM loop1 192 passed Time 2.62 ms
ID:0 GeForce GTX 470:GMEM loop1 96 passed Time 1.87 ms
ID:0 GeForce GTX 470:GMEM loop1 64 passed Time 1.48 ms
ID:0 GeForce GTX 470:GMEM loop1 48 passed Time 1.50 ms
ID:0 GeForce GTX 470:GMEM loop1 32 passed Time 1.75 ms
ID:0 GeForce GTX 470:GMEM loop1 16 passed Time 2.98 ms
```

```
ID:3 GeForce GTX 460:GMEM loop1 49152 passed Time 164.25 ms
ID:3 GeForce GTX 460:GMEM loop1 24576 passed Time 82.45 ms
ID:3 GeForce GTX 460:GMEM loop1 12288 passed Time 41.52 ms
ID:3 GeForce GTX 460:GMEM loop1 6144 passed Time 21.01 ms
ID:3 GeForce GTX 460:GMEM loop1 3072 passed Time 10.77 ms
ID:3 GeForce GTX 460:GMEM loop1 1536 passed Time 5.60 ms
ID:3 GeForce GTX 460:GMEM loop1 768 passed Time 3.16 ms
ID:3 GeForce GTX 460:GMEM loop1 384 passed Time 2.51 ms
ID:3 GeForce GTX 460:GMEM loop1 192 passed Time 2.19 ms
ID:3 GeForce GTX 460:GMEM loop1 96 passed Time 2.12 ms
ID:3 GeForce GTX 460:GMEM loop1 64 passed Time 2.05 ms
ID:3 GeForce GTX 460:GMEM loop1 48 passed Time 2.41 ms
ID:3 GeForce GTX 460:GMEM loop1 32 passed Time 1.96 ms
ID:3 GeForce GTX 460:GMEM loop1 16 passed Time 2.70 ms
```

如果我们首先查看非常大的块数量，可以看到对于 GTX470 和 GTX460 显卡，随着每次运行块数量减半，时间呈相当线性的下降。我们正在将块数量减半
