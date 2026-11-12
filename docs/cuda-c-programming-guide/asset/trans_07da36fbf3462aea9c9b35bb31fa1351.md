

![](img/c13b0ff67eed8f2c7b32afa2a587a8d6_40_0.png)

## 图 9 不使用共享内存的矩阵乘法

以下代码示例是一个利用共享内存进行矩阵乘法的实现。在此实现中，每个线程块负责计算 C 的一个方形子矩阵 Csub，块中的每个线程负责计算 Csub 的一个元素。如图 10 所示，Csub 等于两个矩形矩阵的乘积：与 Csub 具有相同行索引的 A 的子矩阵（维度为 (A.width, block-size)），以及与 Csub 具有相同列索引的 B 的子矩阵（维度为 (block-size, A.width)）。为了适应设备资源，这两个矩形矩阵被分成必要数量的 block_size 维度的方形矩阵，Csub 计算为这些方形矩阵乘积之和。这些乘积中的每一个首先通过从全局内存加载两个对应的方形矩阵到共享内存（每个线程加载每个矩阵的一个元素），然后让每个线程计算乘积的一个元素来执行。每个线程将每个乘积的结果累积到寄存器中，完成后将结果写入全局内存。

通过这种方式阻塞计算，我们利用快速共享内存并节省大量全局内存带宽，因为 A 仅从全局内存读取 (B.width / block_size) 次，B 读取 (A.height / block_size) 次。

前一个代码示例中的 Matrix 类型增加了一个 stride 字段，以便可以用相同的类型高效表示子矩阵。__device__ 函数用于获取和设置元素以及从矩阵构建任何子矩阵。

```
// Matrices are stored in row-major order:
// M(row, col) = *(M.elements + row * M.stride + col)
typedef struct {
    int width;
    int height;
    int stride;
    float* elements;
} Matrix;

// Get a matrix element
__device__ float GetElement(const Matrix A, int row, int col)
{
    return A.elements[row * A.stride + col];
}

// Set a matrix element
__device__ void SetElement(Matrix A, int row, int col,
                           float value)
{
    A.elements[row * A.stride + col] = value;
}

// Get the BLOCK_SIZE x BLOCK_SIZE sub-matrix Asub of A that is
// located col sub-matrices to the right of col sub-matrices and
// row sub-matrices down from the upper-left corner of A
__device__ Matrix GetSubMatrix(Matrix A, int row, int col)
{
    Matrix Asub;
    Asub.width    = BLOCK_SIZE;
    Asub.height   = BLOCK_SIZE;
    Asub.stride   = A.stride;
    Asub.elements = &A.elements[A.stride * BLOCK_SIZE * row
                              + BLOCK_SIZE * col];
    return Asub;
}

// Thread block size
#define BLOCK_SIZE 16

// Forward declaration of the matrix multiplication kernel
__global__ void MatMulKernel(const Matrix, const Matrix, Matrix);

// Matrix multiplication - Host code
// Matrix dimensions are assumed to be multiples of BLOCK_SIZE
void MatMul(const Matrix A, const Matrix B, Matrix C)
{
    // Load A and B to device memory
    Matrix d_A;
    d_A.width = A.width; d_A.height = A.height;
    size_t size = A.width * A.height * sizeof(float);
    cudaMalloc(&d_A.elements, size);
    cudaMemcpy(d_A.elements, A.elements, size,
               cudaMemcpyHostToDevice);
    Matrix d_B;
    d_B.width = B.width; d_B.height = B.height;
    size = B.width * B.height * sizeof(float);
    cudaMalloc(&d_B.elements, size);
    cudaMemcpy(d_B.elements, B.elements, size,
               cudaMemcpyHostToDevice);
    // Allocate C in device memory
    Matrix d_C;
    d_C.width = d_C.stride = C.width; d_C.height = C.height;
    size = C.width * C.height * sizeof(float);
    cudaMalloc(&d_C.elements, size);
    // Invoke kernel
    dim3 dimBlock(BLOCK_SIZE, BLOCK_SIZE);
    dim3 dimGrid(B.width / dimBlock.x, A.height / dimBlock.y);
    MatMulKernel<<<dimGrid, dimBlock>>>(d_A, d_B, d_C);
    // Read C from device memory
    cudaMemcpy(C.elements, d_C.elements, size,
               cudaMemcpyDeviceToHost);
    // Free device memory
    cudaFree(d_A.elements);
    cudaFree(d_B.elements);
    cudaFree(d_C.elements);
}

// Matrix multiplication kernel called by MatMul()
__global__ void MatMulKernel(Matrix A, Matrix B, Matrix C)
{
// Block row and column
int blockRow = blockIdx.y;
int blockCol = blockIdx.x;
// Each thread block computes one sub-matrix Csub of C
Matrix Csub = GetSubMatrix(C, blockRow, blockCol);
// Each thread computes one element of Csub
// by accumulating results into Cvalue
float Cvalue = 0;
// Thread row and column within Csub
int row = threadIdx.y;
int col = threadIdx.x;
// Loop over all the sub-matrices of A and B that are
// required to compute Csub
// Multiply each pair of sub-matrices together
// and accumulate the results
for (int m = 0; m < (A.width / BLOCK_SIZE); ++m) {
// Get sub-matrix Asub of A
Matrix Asub = GetSubMatrix(A, blockRow, m);
// Get sub-matrix Bsub of B
Matrix Bsub = GetSubMatrix(B, m, blockCol);
// Shared memory used to store Asub and Bsub respectively
__shared__ float As[BLOCK_SIZE][BLOCK_SIZE];
__shared__ float Bs[BLOCK_SIZE][BLOCK_SIZE];
// Load Asub and Bsub from device memory to shared memory
// Each thread loads one element of each sub-matrix
As[row][col] = GetElement(Asub, row, col);
Bs[row][col] = GetElement(Bsub, row, col);
// Synchronize to make sure the sub-matrices are loaded
// before starting the computation
__syncthreads();

// Multiply Asub and Bsub together
for (int e = 0; e < BLOCK_SIZE; ++e)
    Cvalue += As[row][e] * Bs[e][col];

// Synchronize to make sure that the preceding
// computation is done before loading two new
// sub-matrices of A and B in the next iteration
    __syncthreads();
}
// Write Csub to device memory
// Each thread writes one element
    SetElement(Csub, row, col, Cvalue);
}
```

![](img/c13b0ff67eed8f2c7b32afa2a587a8d6_43_0.png)

## 3.2.4. 页锁定主机内存

运行时提供函数以允许使用页锁定（也称为固定）主机内存（与由 malloc() 分配的常规可页主机内存相对）：

- cudaHostAlloc() 和 cudaFreeHost() 分配和释放页锁定主机内存；
- cudaHostRegister() 页锁定由 `malloc()` 分配的一段内存（有关限制，请参阅参考手册）。

使用页锁定主机内存有多种好处：

- 对于某些设备，页锁定主机内存与设备内存之间的拷贝可以与内核执行并发进行，如异步并发执行中所述。
- 在某些设备上，页锁定主机内存可以映射到设备的地址空间，从而无需将其拷贝到或从设备内存拷贝，如映射内存中详细说明。
- 在具有前端总线的系统上，如果主机内存分配为页锁定，则主机内存和设备内存之间的带宽更高；如果还分配为写合并，则带宽更高，如写合并内存中所述。

然而，页锁定主机内存是一种稀缺资源，因此页锁定内存的分配将在可页内存分配失败之前很久就开始失败。此外，通过减少操作系统可用于分页的物理内存量，消耗过多页锁定内存会降低整体系统性能。

> 页锁定主机内存在非 I/O 一致 Tegra 设备上不缓存。此外，cudaHostRegister() 在非 I/O 一致 Tegra 设备上不受支持。

简单的零拷贝 CUDA 示例附带有关页锁定内存 API 的详细文档。

### 3.2.4.1. 可移植内存

一块页锁定内存可以与系统中的任何设备一起使用（有关多设备系统的更多详细信息，请参阅多设备系统），但默认情况下，上述使用页锁定内存的好处仅在分配块时当前的设备（以及共享同一统一地址空间的所有设备，如果有，如统一虚拟地址空间中所述）可用时才可用。要使这些优势对所有设备可用，该块需要通过将标志 cudaHostAllocPortable 传递给 cudaHostAlloc() 来分配，或通过将标志 cudaHostRegisterPortable 传递给 cudaHostRegister() 来页锁定。

### 3.2.4.2. 写合并内存

默认情况下，页锁定主机内存分配为可缓存。也可以通过将标志 cudaHostAllocWriteCombined 传递给 cudaHostAlloc() 将其分配为写合并。写合并内存释放主机的 L1 和 L2 缓存资源，为应用程序的其余部分提供更多缓存。此外，写合并内存在跨 PCI Express 总线传输期间不被监听，可将传输性能提高多达 40%。

从主机读取写合并内存的速度极慢，因此写合并内存通常应仅用于主机只写入的内存。

