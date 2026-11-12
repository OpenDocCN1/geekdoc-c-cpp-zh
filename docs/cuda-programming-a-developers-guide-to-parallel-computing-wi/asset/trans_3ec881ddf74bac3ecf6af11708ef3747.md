

![](img/e0b192dbaf05f61ad420bee512a8c4e4_182_0.png)

## 图 6.16 重叠的内核和内存传输。

![](img/e0b192dbaf05f61ad420bee512a8c4e4_182_1.png)

## 图 6.17 线程 ID 访问的地址。

非阻塞和隐式内存传输可能不受支持。我们将在第 9 章中更详细地探讨这些问题。

通常的执行模型涉及 CPU 将一块数据传输到 GPU，GPU 内核对其进行处理，然后 CPU 发起将数据传回主机内存的传输。这种模型的稍高级形式是使用流（稍后介绍）来重叠传输和内核，以确保 GPU 始终保持忙碌，如图 6.16 所示。

一旦数据位于 GPU 中，问题就变成了如何在 GPU 上高效访问它？请记住，GPU 的计算能力可超过 3 万亿次浮点运算每秒（teraflops），但通常主内存带宽在 190 GB/s 左右，低至 25 GB/s。相比之下，典型的 Intel I7 Nehalem 或 AMD Phenom CPU 可达到 25–30 GB/s 左右，具体取决于所使用设备的速度和内存总线宽度。

显卡使用高速 GDDR（图形动态内存），可实现非常高的持续带宽，但像所有内存一样，具有高延迟。延迟是指返回数据访问的第一个字节所需的时间。因此，就像我们可以对内核进行流水线处理（如图 6.16 所示）一样，内存访问也被流水线化。通过创建通常 10:1 的线程与内存访问数量之比，可以隐藏内存延迟，但前提是以合并的模式访问全局内存。

什么是可合并模式？这是指所有线程访问一个连续且对齐的内存块，如图 6.17 所示。这里我们将 `Addr` 显示为相对于基位置的逻辑地址偏移，假设我们访问的是基于字节的数据。TID 表示线程编号。如果我们对内存进行一对一的顺序且对齐的访问，则每个线程的地址访问会被合并在一起，并发出单个内存事务。假设我们访问的是单精度浮点数或整数值，每个线程将访问 4 字节的内存。内存基于 warp 进行合并（旧的 G80 硬件使用半 warp），这意味着我们得到 32 x 4 = 128 字节的内存访问。

支持的合并大小为 32、64 和 128 字节，这意味着如果访问是顺序模式且对齐到 32 字节边界，则 warp 对字节、16 位和 32 位数据的访问将始终合并。对齐是通过使用特殊的 malloc 指令实现的，即用 `cudaMallocPitch` 替换标准 `cudaMalloc`，其语法如下：

```
extern __host__ cudaError_t CUDARTAPI cudaMallocPitch(void **devPtr, size_t *pitch,
size_t width, size_t height);
```

这相当于 `cudaMallocPitch`（设备内存指针的指针、pitch 指针、行所需宽度（字节）、数组高度（字节））。

因此，如果你有一个包含 100 行、每行 60 个 float 元素的数组，使用常规 `cudaMalloc` 将分配 100 x 60 x sizeof(float) 字节，即 100 x 60 x 4 = 24,000 字节。访问数组索引 [1][0]（即第一行，第零个元素）将导致非合并访问。这是因为 60 个元素的单行长度为 240 字节，当然这不是 2 的幂。

每个线程地址系列中的第一个地址将不满足合并的对齐要求。使用 `cudaMallocPitch` 函数，每行的大小将根据给定设备的对齐要求填充必要的量（图 6.18）。在我们的示例中，在大多数情况下，每行将扩展到 64 个元素，即 256 字节。设备实际使用的 pitch 将通过传递给 `cudaMallocPitch` 的 pitch 参数返回。

让我们看看这在实践中是如何工作的。未对齐的访问会导致发出多个内存读取请求。在等待内存读取时，warp 中的所有线程都会停滞，直到 _所有_ 内存读取从硬件返回。因此，为了获得最佳吞吐量，你需要发出少量的大内存读取请求，这是由对齐且顺序的合并访问产生的。

![](img/e0b192dbaf05f61ad420bee512a8c4e4_183_0.png)

## 图 6.18 使用 cudaMallocPitch 实现的填充。

如果数据以某种方式交错，例如结构体，会发生什么情况？

```
typedef struct
{
    unsigned int a;
    unsigned int b;
    unsigned int c;
    unsigned int d;
} MY_TYPE_T;

MY_TYPE_T some_array[1024]; /* 1024 * 4 bytes = 4K */
```

| 索引 0 元素 A | 索引 0 元素 B | 索引 0 元素 C | 索引 0 元素 D | 索引 1 元素 A | 索引 1 元素 B | 索引 1 元素 C | 索引 1 元素 D | 索引 N 元素 A、B、C、D |
|---|---|---|---|---|---|---|---|---|
| | | | | | | | | |

![](img/e0b192dbaf05f61ad420bee512a8c4e4_184_0.png)

图 6.19 显示了 C 语言如何在内存中布局此结构。元素在内存中的布局顺序与它们在结构体中定义的顺序相同。此类结构的访问模式如图 6.20 所示。如图所示，结构元素的地址在内存中不是连续的。这意味着你无法获得合并，内存带宽会突然下降一个数量级。根据数据元素的大小，可能可以让每个线程读取一个较大的值，然后在线程内部屏蔽掉不需要的位。例如，如果你有基于字节的数据，可以执行以下操作：

![](img/e0b192dbaf05f61ad420bee512a8c4e4_184_1.png)

![](img/e0b192dbaf05f61ad420bee512a8c4e4_184_2.png)

```
const unsigned int value_u32 = some_data[tid];
const unsigned char value_01 = (value_u32 & 0x000000FF);
const unsigned char value_02 = (value_u32 & 0x0000FF00) >> 8;
const unsigned char value_03 = (value_u32 & 0x00FF0000) >> 16;
const unsigned char value_04 = (value_u32 & 0xFF000000) >> 24;
```

也可以通过将结构元素数组视为字数组来简单地保持一个线程对应一个数据元素的映射。然后我们可以为结构的每个元素分配一个线程。然而，如果结构成员之间存在数据流关系，这种解决方案就不合适，例如线程 1 需要结构体的 x、y 和 z 坐标。在这种情况下，最好在 CPU 的加载或传输阶段将数据重新排序为 N 个离散数组。这样，各个数组在内存中并发存放。我们可以直接访问数组 a、b、c 或 d，而不是使用结构体解引用时会使用的 struct->a 表示法。与交错且未合并的模式不同，我们从每个线程获得四个合并访问，访问不同的内存区域，从而保持最佳的全局内存带宽使用。

让我们看一个全局内存读取示例。在此示例中，我们将使用两种方法对结构中所有元素的值求和。首先，我们将对结构数组中的所有值求和，然后对结构体中的数组求和。

```
// Define the number of elements we'll use
#define NUM_ELEMENTS 4096
```

```
// Define an interleaved type
// 16 bytes. 4 bytes per member
typedef struct
{
u32 a;
u32 b;
u32 c;
u32 d;
} INTERLEAVED_T;
// Define an array type based on the interleaved structure
typedef INTERLEAVED_T INTERLEAVED_ARRAY_T[NUM_ELEMENTS];
```

```
// Alternative - structure of arrays
typedef u32 ARRAY_MEMBER_T[NUM_ELEMENTS];
typedef struct
{
ARRAY_MEMBER_T a;
ARRAY_MEMBER_T b;
ARRAY_MEMBER_T c;
ARRAY_MEMBER_T d;
} NON_INTERLEAVED_T;
```

在此代码部分中，我们声明了两种类型；第一种是 INTERLEAVED_T，即成员为 a 到 d 的结构数组。然后我们将 NON_INTERLEAVED_T 声明为包含四个数组（a 到 d）的结构。正如类型名称所示，使用第一种类型时，我们期望数据在内存中是交错的。使用第二种类型时，我们期望有若干个连续的内存区域。

让我们先看看 CPU 代码。

```
__host__ float add_test_non_interleaved_cpu(
    NON_INTERLEAVED_T * const host_dest_ptr,
    const NON_INTERLEAVED_T * const host_src_ptr,
    const u32 iter,
    const u32 num_elements)
{
    float start_time = get_time();

    for (u32 tid = 0; tid < num_elements; tid++)
    {
        for (u32 i=0; i<iter; i++)
        {
            host_dest_ptr->a[tid] += host_src_ptr->a[tid];
            host_dest_ptr->b[tid] += host_src_ptr->b[tid];
            host_dest_ptr->c[tid] += host_src_ptr->c[tid];
            host_dest_ptr->d[tid] += host_src_ptr->d[tid];
        }
    }

    const float delta = get_time() - start_time;

    return delta;
}
```

```
__host__ float add_test_interleaved_cpu(
    INTERLEAVED_T * const host_dest_ptr,
    const INTERLEAVED_T * const host_src_ptr,
    const u32 iter,
    const u32 num_elements)
{
    float start_time = get_time();

    for (u32 tid = 0; tid < num_elements; tid++)
    {
        for (u32 i=0; i<iter; i++)
        {
            host_dest_ptr[tid].a += host_src_ptr[tid].a;
            host_dest_ptr[tid].b += host_src_ptr[tid].b;
            host_dest_ptr[tid].c += host_src_ptr[tid].c;
            host_dest_ptr[tid].d += host_src_ptr[tid].d;
        }
    }

    const float delta = get_time() - start_time;

