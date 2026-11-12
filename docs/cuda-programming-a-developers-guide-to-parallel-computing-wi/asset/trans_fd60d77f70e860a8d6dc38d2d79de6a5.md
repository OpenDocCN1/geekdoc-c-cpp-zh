

单条获取/解码逻辑随后为分歧线程获取指令流，而其他线程则简单地忽略它。实际上，线程束内的每个线程都有一个掩码，用于启用或禁用其执行。那些不遵循分歧的线程会清除掩码。相反，遵循分支的线程会设置该位。

这种安排称为谓词执行。会创建一个谓词，对于遵循分支的线程束内线程，会设置一位。大多数 PTX 操作码支持可选的谓词，允许选择性线程执行指令。

因此，例如，请考虑以下代码：

```
if (threadIdx.x < 32)
{
    if (threadIdx.x < 16)
    {
        if (threadIdx.x < 8)
            func_a1();
        else
            func_a2();
    }
    else
        func_b();
}
```

在代码的第一行中，程序会消除当前块中除了第一个线程束（即前 32 个线程）之外的所有其他线程束。这不会在线程束内产生任何分歧。块中的其他线程束仅不为此部分代码调度。它们不会停滞，而是直接通过该代码并继续执行后续代码。

第一个线程束随后会遇到 threadIdx.x < 16 的测试，这会将线程束恰好分为两半。这是一种特殊场景，线程束实际上并未发生分歧。尽管线程束大小为 32，但分歧标准实际上是半线程束。如前所述，CUDA 核心按每组 16 个核心（而非 32 个核心）的银行排列。调度器每个周期向两个或多个 16 核心组发送指令。因此，条件的真分支和假分支都会被执行。

在后续步骤中，线程 16 到 31 调用函数 func_b。然而，线程 0..15 遇到了另一个条件判断。这次不是基于半线程束，而是基于四分之一线程束。最小调度数量是 16 个线程。因此，第一组八个线程跳转去调用 func_a1，而第二组八个线程（8..15）则会停滞。

函数 func_b 和 func_a1 将继续独立获取指令并将其分发到两个半线程束。这比单条指令获取效率略低，但仍好于顺序执行。最终 func_a1 将完成，func_a2 将开始，停滞线程 0..7。在此期间 func_b 可能也已完成。我们可以编写一个简短的测试程序来演示这一点。

```
// All threads follow the same path
__global__ void cuda_test_kernel(
u32 * const a,
const u32 * const b,
const u32 * const c,
const u32 num_elements)
{
const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;

if (tid < num_elements)
{
    for (u32 iter=0; iter<MAX_ITER; iter++)
    {
        a[tid] += b[tid] * c[tid];
    }
}
}
```

```
// Thread diverge by half warps
__global__ void cuda_test_kernel_branched_half(
u32 * const a,
const u32 * const b,
const u32 * const c,
const u32 num_elements)
{
const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;

if (tid < num_elements)
{
    for (u32 iter=0; iter<MAX_ITER; iter++)
    {
    if (threadIdx.x < 16)
    a[tid] += b[tid] * c[tid];
    else
    a[tid] -= b[tid] * c[tid];
    }
}
}
```

```
// Thread diverge into one quarter group
__global__ void cuda_test_kernel_branched_quarter(
u32 * const a,
const u32 * const b,
const u32 * const c,
const u32 num_elements)
{
const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;

if (tid < num_elements)
{
    for (u32 iter=0; iter<MAX_ITER; iter++)
    {
    if (threadIdx.x < 16)
    {
        if (threadIdx.x < 8)
        {
            a[tid] += b[tid] * c[tid];
        }
        else
        {
            a[tid] -= b[tid] * c[tid];
        }
    }
    else
    {
        a[tid] += b[tid] * c[tid];
    }
    }
}
}
```

```
// Thread diverge into one eighth group
__global__ void cuda_test_kernel_branched_eighth(
    u32 * const a,
    const u32 * const b,
    const u32 * const c,
    const u32 num_elements)
{
    const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;

    if (tid < num_elements)
    {
        for (u32 iter=0; iter<MAX_ITER; iter++)
        {
            if (threadIdx.x < 16)
            {
                if (threadIdx.x < 8)
                {
                    if (threadIdx.x < 4)
                    {
                        a[tid] += b[tid] * c[tid];
                    }
                    else
                    {
                        a[tid] -= b[tid] * c[tid];
                    }
                }
                else
                {
                    if (threadIdx.x >= 8)
                    {
                        a[tid] += b[tid] * c[tid];
                    }
                    else
                    {
                        a[tid] -= b[tid] * c[tid];
                    }
                }
            }
            else
            {
                a[tid] += b[tid] * c[tid];
            }
        }
    }
}
```

此处我们设置了一系列内核，每个内核表现出不同程度的分歧。第一个是没有分歧的最优情况。第二个基于半线程束发生分歧。这些半线程束应并行执行。然后我们将第一个半线程束进一步细分为两组。这些应串行执行。然后我们再次将第一组细分为总共四条串行执行路径。我们看到的结果如下：

运行 32768 个块，每个块 32 个线程，以计算 1048576 个元素

| ID | 设备 | 所有线程 | 半线程束 | 四分之一线程束 | 八分之一线程束 |
|---|---|---|---|---|---|
| 0 | GeForce GTX 470 | 27.05 ms (100%) | 32.59 ms (121%) | 72.14 ms (267%) | 108.06 ms (400%) |
| 1 | GeForce 9800 GT | 240.67 ms (100%) | 241.33 ms (100%) | 252.77 ms (105%) | 285.49 ms (119%) |
| 2 | GeForce GTX 260 | 120.36 ms (100%) | 122.44 ms (102%) | 149.60 ms (124%) | 174.50 ms (145%) |
| 3 | GeForce GTX 460 | 43.16 ms (100%) | 57.49 ms (133%) | 127.68 ms (296%) | 190.85 ms (442%) |

我们可以在图 9.32 的图形格式中更清楚地看到这一点。

请注意，线程分歧在计算能力 1.x 设备（9800 GT 和 GTX260）上并不是一个如此显著的问题。它有影响，但最大时间仅为最优时间的 145%。相比之下，Fermi 计算能力 2.x 显卡（GTX460、GTX470）在线程束内发生显著分歧时会遭受超过 4 倍的减速。GTX460 似乎对线程束分歧特别敏感。请注意，在没有分歧的情况下，GTX470 的绝对速度几乎是 9800 GT 的 10 倍，这对于仅两代显卡来说是巨大的改进。

如果你好奇 32 向分歧的代价是多少，它会导致计算能力 1.x 显卡减速 27 倍，以及计算能力 2.x 显卡巨大的 125 倍至 134 倍减速。请注意，

![](img/e0b192dbaf05f61ad420bee512a8c4e4_393_0.png)

图 9.32 线程分歧如何影响执行时间。

此测试的代码是基于线程索引的简单 switch 语句，因此与我们在此处使用的代码不可直接比较。然而，显然这种分歧应不惜一切代价避免。

避免线程束内分歧的最简单方法是，简单地屏蔽掉你不希望对结果做出贡献的线程束部分。如何做到这一点？只需对线程束中的每个线程执行相同的计算，但为你希望屏蔽掉的线程选择一个不贡献的值。

例如，对于 32 位整数的 min 操作，为不应贡献的线程选择 0x7FFFFFFF 作为值。反之，对于 max、sum 以及许多其他算术类型操作，只需在你不希望贡献的线程中使用 0。这通常比在线程束内进行分支要快得多。

## 理解底层汇编代码

GPU 将代码编译为名为 PTX（并行线程执行指令集架构）的虚拟汇编系统。这很像 Java 字节码，因为它是一种虚拟汇编语言。它可以在编译时或运行时转换为在设备上执行的实际代码。编译时翻译只是根据你在命令行中指定的架构（–arch 开关）向应用程序插入若干实际二进制文件。

要查看生成的虚拟汇编，只需在编译器命令行中添加 –keep 标志。对于 Visual Studio 用户，默认的 NVIDIA 项目包含保留 PTX 文件（–keep）的选项（图 9.33）。你也可以使用 –keep_dir <directory> 选项指定存储位置，如果你希望它们不弄乱项目目录的话。

然而，PTX 并不是硬件上真正执行的内容，因此其用途仅限于一定程度。你也可以使用 cuobjdump 实用程序查看翻译后的实际二进制文件，如下所示：

```
cuobjdump -sass global_mem_sample_sort_sm_20.cubin > out.txt
```

