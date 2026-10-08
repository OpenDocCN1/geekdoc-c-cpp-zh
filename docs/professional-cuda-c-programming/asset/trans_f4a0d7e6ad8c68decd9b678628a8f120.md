

使用矩形共享内存会导致内存访问违规。你需要根据矩阵维度重新计算访问索引，并重新实现上一节中描述的所有内核（kernels）。

在不一般的情况下，你将检查一个每行 32 个元素、每列 16 个元素的矩形共享内存数组。这些维度在以下宏中定义：

```
#define BDIMX 32
#define BDIM 16
```

矩形共享内存块的分配如下：

```
__shared__ int tile [BDIMX][BDIMY];
```

为了简单起见，内核将使用一个网格和一个二维块启动，该线程块的大小与矩形共享内存数组相同，如下：

```
dim3 block (BDIMX, BDIMY);
dim3 grid (1,1);
```

## 访问行优先与访问列优先

你将要研究的前两个内核也曾用于正方形情况：

```
__global void setRowReadRow(int *);
__global void setColReadCol(int *);
```

你需要仔细注意每个内核中矩形共享内存数组的声明。共享内存数组块的最内层维度长度与二维线程块的最内层维度相同：

```
__shared__ int tile [BDIMX][BDIMY];
```

在 `setColReadCol` 内核中，共享内存数组块的最内层维度长度与二维线程块的最外维度相同：

```
__shared__ int tile [BDIMX][BDIMY];
```

你可以从 Wrox.com 下载 `checkSmemRectangle.cu` 中的此示例代码。编译它并使用以下 `nvprof` 指标检查 bank（存储）结果：

```
shared_load_transactions_per_request
shared_store_transactions_per_request
```

K40 上的结果报告如下：

```
Kernel:setRowReadRow(int*)
  1 shared_load_transactions_per_request 1.000000
  1 shared_store_transactions_per_request 1.000000
Kernel:setColReadCol(int*)
  1 shared_load_transactions_per_request 8.000000
  1 shared_store_transactions_per_request 8.000000
```

`setReadRow` 内核中对共享内存的存储和加载请求由一个事务处理。而 `setColRead` 内核中的请求由八个事务处理。Kepler K40 的带宽为 8 个字，一列中的 16 个 4 字节元素被排列到各个 中，如图 5-6 所示；因此，操作报告了八路冲突（bank conflict）。

## 行优先写入与列优先读取

在本节中，你将实现一个内核，使用矩形共享内存按行优先顺序写入共享内存并按列优先顺序从共享内存读取。该内核适用于实际应用；它通过使用共享内存进行转置，通过最大化延迟加载存储以及合并全局内存访问来提高性能。

二维共享内存块声明如下：

```
__shared int tile [BDIMY] [BDIMX];
```

该内核有三个内存操作：

-   每个 warp 向共享内存行写入数据以避免 bank 冲突。
-   每个 warp 从共享内存列读取数据以执行矩阵转置。
-   每个 warp 以合并访问的方式写入全局内存行。

计算正确的共享内存和全局内存访问的步骤如下。首先，将当前线程的 2D 线程索引转换为 1D 全局线程 ID：

```
unsigned int idx = threadIdx.y * blockDim.x + threadIdx.x;
```

这种 1D 行优先映射确保了全局内存访问是合并的。由于输出全局内存中的数据元素经过了转置，你需要计算转置矩阵中的新坐标：

```
unsigned int irow = idx / blockDim.y;
unsigned int icol = idx % blockDim.y;
```

你通过以下方式将全局线程 ID 存储到 2D 共享内存块中来初始化：

```
tile[threadIdx.y][threadIdx.x] = idx;
```

此时，共享内存中的数据从 0 到 `BDIMX*BDIMY-1` 线性存储。每个 warp 对共享内存执行行优先写入，写入操作期间没有 bank 冲突。

现在，你可以可以使用先的坐标访问共享内存数据进行转置。通过使用交换后的 `irow` 和 `icol` 访问共享内存，你可以使用全局 1D 线程 ID 转置数据。如下代码段所示，一个 warp 从共享内存的一列读取数据元素，并对全局内存执行合并写入。

```
out[idx] = tile[icol][irow];
```

完整的内核代码如下：

```
__global__ void setRowCol(int *out) {
    // 共享内存
    __shared int tile[BDIMY][BDIMX];

    // 从 2D 线程索引到线性内存的映射
    unsigned int idx = threadIdx.y * blockDim.x + threadIdx.x;

    // 将 idx 转换为转置坐标 (行, 列)
    unsigned int row = idx / blockDim.y;
    unsigned int ncol = idx % blockDim.y;

    // 共享内存存储操作
    tile[threadIdx.y][threadIdx.x] = idx;

    // 等待所有线程完成
    __syncthreads();

    // 共享内存加载操作
    out[idx] = tile[ncol][row];
}
```

*(注：由于原文末尾存在部分重复和截断，上述翻译已根据 CUDA 开发逻辑进行了理顺。)*

