
如果你在主机上有一个具有 $M$ 行 $N$ 列单精度浮点数的稠密列主序矩阵 $A$，你可以使用 `cublasSetMatrix` 通过以下命令传输整个矩阵：

```
cublasSetMatrix(M, N, sizeof(float), A, dA, M);
```

你也可以使用 `cublasSetVector` 将矩阵 A 的单列传输到设备上的向量 $DV$。`cublasSetVector` 接受以下参数：

```
cublasStatus_t cublasSetVector(int n, int elemSize, const void *x, int incx, void *y, int incy)
```

其中 x 是主机上的源位置，y 是设备上的目标位置，$n 是要传输的元素个数，$elemSize 是每个元素的字节大小，，$incx/incy$ 是元素之间的步长。将列主序矩阵 $A$ 中长度为 $M$ 的单列传输到向量 $DV$ 可以这样实现：

```
cublasSetVector(M, sizeof(float), A, 1, DV, 1);
```

你还可以使用 `cublasSetVector` 将矩阵 A 的单行传输到设备上的向量 $DV$：

```
cublasSetVector(N, sizeof(float), A, M, DV, 1);
```

该函数从 A 拷贝 $N$ 个元素到 $DV$，每次跳过 A 中的 $M$ 个元素。由于 $A$ 是列主序的，此命令将 A 的第一行拷贝到设备上。拷贝第 $i$ 行的实现方式如下：

```
cublasSetVector(N, sizeof(float), A + i, M, DV, 1);
```

这种数据比 cuSPARSE 暴露的数据要简单得多。除非你的应用程序能够从稀疏结构中显著获益，否则使用 cuBLAS 可能会提高性能并使开发过程更加简单。

## 演示 cuBLAS

这里演示的 cuBLAS 示例将重点介绍 cuBLAS 的一致性，以及 GPU 带来的性能优势——与优化的仅主机 BLAS 库相比，其速度可以快 15 倍以上，而使用 cuBLAS 的开发工作仅比旧版 BLAS 实现略微多出一点点。

## 一个简单的 cuBLAS 示例

此示例将在 GPU 上执行矩阵-向量乘法，这是一种 cuBLAS 2 类操作。你可以通过 Wrox.com 下载 `cublas.cu` 示例代码，或使用以下片段进行练习：

```
// 创建 cuBLAS 柄
cublasCreate(&handle);
```

```
// 分配设备内存
cudaMalloc(void **DA, sizeof(float) * M * N);
cudaMalloc(void **DX, sizeof(float) * N);
cudaMalloc(void **DY, sizeof(float) * M);
```

```
// 将输入传输到设备
cublasSetVector(N, sizeof(float), X, 1, dX);
cublasSetVector(M, sizeof(float), Y, 1, dY);
cublasSetMatrix(M, N, sizeof(float), A, M, dA, M);
```

```
// 执行矩阵-向量乘法
cublasSgemv(handle, CUBLAS_OP_N, M, N, &alpha, dA, dX, &beta, dY);
```

```
// 从设备检索输出向量
cublasGetVector(M, sizeof(float), DY, 1, Y);
```

使用 cuBLAS 库非常简单。与之前的 cuSPARSE 相比，`cublas.cu` 展示了通用库工作流的子集。它包含了以下步骤：

- 1. 使用 `cublasCreateHandle` 创建 cuBLAS 柄。
- 2. 使用 `cudaMalloc` 为输入输出分配设备内存。
- 3. 使用 `cublasSetVector` 和 `cublasSetMatrix` 在分配的设备内存中填充输入。
- 4. 执行 `cublasSgemv` 库将矩阵-向量乘法操作卸载到 GPU。
- 5. 使用 `cublasGetVector` 从设备内存检索结果。
- 6. 使用 `cudaFree` 和 `cublasDestroy` 释放 CUDA 和 cuBLAS 资源。

可以使用以下命令编译此示例：

```
$ nvcc -lcublas cublas.cu
```

使用 cuBLAS 库比使用 cuSPARSE 库所需的精力更少，主要因为 cuBLAS 设计为与旧 BLAS 库高度兼容。

## BLAS 的迁移

将旧 BLAS 库的应用程序迁移到 cuBLAS 是简单的。迁移过程通常包含四个主要步骤：

- 1. 为任何输入或输出向量或矩阵添加设备内存分配 (`cudaMalloc`) 和设备内存释放 (`cudaFree`)。
- 2. 添加在主机和设备之间传输输入和矩阵的方法（例如 `cublasSetVector`、`cublasSetMatrix`、`cublasGetVector`、`cublasGetMatrix`）。
- 3. 将对 BLAS 库的实际调用转换为等效的 cuBLAS 程序。可能可能对参数进行微调。例如，上一个示例使用了 cuBLAS 函数：

```
cublasStatus_t cublasSgemv(cublasHandle_t handle, cublasOperation_t trans, int m, int n, const float *alpha, const float *A, const float *x, const float *beta, float *y, int incy);
```

库中对应的 BLAS 函数接口略有不同：

```
void cblas_sgemv(const CBLAS_ORDER order, const CBLAS_TRANSPOSE trans, int m, int n, const float *alpha, const float *A, int lda, const float *x, int incx, const float *beta, float *y, int incy);
```

虽然许多参数相同或相似的（trans, m, n, alpha, lda, x, incx, beta, y, incy），但 cuBLAS 包含了顺序参数（允许你以行主序或列主序指定输入），并且 cuBLAS 增加了柄。另外注意，BLAS 的 alpha 和 beta 参数不像在 cuBLAS 中那样通过引用传递的。对于所有 cuBLAS 函数来说，这些都是微小的差异，不会成为迁移应用程序到 cuBLAS 的主要障碍。

最后，你也可以在实现后选择优化你的新 cuBLAS 应用程序。这一步可以包括：

- a. 重用内存分配，而不是为每次 cuBLAS 调用都进行分配和释放。
- b. 移除对后续 cuBLAS 调用使用的向量和矩阵的冗余设备到主机拷贝。
- c. 使用 `cublasStream` 添加基于流的执行以启用异步传输。有关流如何提高性能，请参阅第 6 章“流与并发”。

## cuBLAS 开发中的重要主题

与 cuSPARSE 相比，如果你有旧 BLAS 库的经验，cuBLAS 会更加熟悉和直观。因此，更容易理解背后发生的过程。这意味着可能出现的潜在问题在 cuSPARSE 中更容易管理。

如果你使用行主序编程语言，使用 cuBLAS 开发可能需要对细节给予额外关注。很容易使用你熟悉的代码模式，例如，使用行主序索引平化数组。为了帮助，你可以定义宏来自动将从 0 开始的行主序索引转换为列主序：

```
#define R2C(r, c, nrows) ((c * (nrows) + (r))
```

然而，即使使用这样的宏，你也必须对周围循环的顺序进行更多思考。许多 C/C++ 程序员会倾向于：

```
for (int r = 0; r < nrows; r++) {
  for (int c = 0; c < ncols; c++) {
    A[R2C(r, c, nrows)] = ...;
  }
}
```

虽然这段代码是正确的，但如果它没有线性扫描数组中的内存位置，将是次优的。例如，如果数组从内存位置零开始，此循环的前三个引用将位于0、$nrows$ 和 $2 \times nrows$。由于 $nrows$ 可能很大，跨度很大的内存访问会导致糟糕的缓存局部性。因此，你必须小心反转循环的顺序：

```
for (int c = 0; c < ncols; c++) {
  for (int r = 0; r < nrows; r++) {
    A[R2C(r, c, nrows)] = ...;
  }
}
```

在这样做时要小心，因为你可能无意中在赋值的右侧引起糟糕的缓存局部性。

从旧 BLAS 库迁移到 cuBLAS 是最具吸引力的方面。在这种情况下，主要的更改只是增加了设备内存管理和传输调用。

## cuBLAS 总结

本节介绍了简单易用的 cuBLAS 库，重点关注了其易用性和可移植性。下一节将关注今天科学计算和信号处理中最有算法之一：快速傅里叶变换。

## cuFFT 库

cuFFT 库提供了优化的、基于 CUDA 的快速傅里叶变换 (FFT) 实现。FFT 是信号处理中的一种将信号从时间域转换为频率域的变换。逆 FFT 则是相反的。另一种说是，FFT 接收从定期时间间隔从信号采集的样本序列。它利用这些样本生成一组频率，通过叠加来重建由输入样本生成的信号。图 8-9 显示了两个信号之和形成 $\cos (x)+\cos (2x)$ 信号，并通过 FFT 分解为频率1.0和2.0。提供更深入的 FFT 理解超出了本书的范围。
