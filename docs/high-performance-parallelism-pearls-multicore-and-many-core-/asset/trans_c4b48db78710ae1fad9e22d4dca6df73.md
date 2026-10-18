
```
1: **Partition** card into *nstreams* partitions and **create** one stream per partition  (*hS)
2: **Define** integers *q.potrf*, *q.trsm*, and *q.syrk_gemm* and **set** them all to zero.
3: **Call** LAPACKE_dpotrf on the host CPU for the diagonal hot tile (A[1][1]).
4: **Transfer** the diagonal hot tile (A[1][1]) to the card in stream id: *q.potrf%nstreams* (*hS). Associate an hStreams event, *eventCpyTo*[1][1] with this transfer (*hS). Increment *q.potrf* by 1.
5: **for** *m* = 2, *T* **do**
6:   **Transfer** tile A[*m*][1] to card in stream id: *q.trsm%nstreams*  (*hS)
7:   **Wait** for event *eventCpyTo*[1][1] to finish  (*hS)
8:   **Call** cblas_dtrsm on card in stream id: *q.trsm%nstreams*  (*hS). Associate an event, *eventTrsm*[*m*][1] with this compute (*hS).
9:   **Transfer** tile A[*m*][1] to host in stream id: *q.trsm%nstreams*. Increment *q.trsm* by 1 (*hS)
10: **end for**
11: **for** *n* = 2, *T* **do**
12:  **Transfer** tile A[*n*][*n*] to card in stream id: *q.syrk_gemm%nstreams*  (*hS).
13:  **Wait** for event *eventTrsm*[*n*][1] to finish  (*hS).
14:  **Call** cblas_dsyrk for tile A[*n*][*n*] on card in stream id: *q.syrk_gemm%nstreams* (*hS). Increment *q.syrk_gemm* by 1.
15:  **for** *m* = *n* + 1, *T* **do**
16:    **Transfer** tile A[*m*][*n*] to card in stream id: *q.syrk_gemm%nstreams*  (*hS).
17:    **Wait** for event *eventTrsm*[*m*][1] to finish  (*hS).
18:    **Wait** for event *eventTrsm*[*n*][1] to finish  (*hS).
19:    **Call** cblas_dgemm for tile A[*m*][*n*] on card in stream id: *q.syrk_gemm%nstreams* (*hS). Increment *q.syrk_gemm* by 1.
20:  **end for**
21: **end for**
```

### 图 15.19

将协处理器划分为多个物理分区，并为每个分区关联一个流。同样地，在图中，属于 hStreams API 的所有操作在算法中都标注了 (*hS)。我们定义了三个队列，一个用于 dpotrf，一个用于 dtrsm，一个同时用于 dsyrk 和 dgemm。在对协处理器排队的每次计算之后，这些队列都会递增，并在可用的最大流数处回绕，从而提供良好的负载均衡。如前所述，dpotrf 在主机上对对角线热点分片执行。dpotrf 执行完成后，对角线热点分片被传输到协处理器以供后续使用。算法的其余部分遵循图 15.17 中给出的主机原生分片 Cholesky 算法，并插入了数据传输和同步事件。

## 性能

现在我们来看 Cholesky 分解的性能。为此，我们将考察分片 hStreams 卸载程序的两个版本。

第一个程序遵循图 15.19 中的算法，我们使用主机 CPU 计算对角线分片上的 dpotrf，其余计算（即 dtrsm、dsyrk 和 dgemm）在协处理器上完成。为了与之对比，我们考察 MKL 的自动卸载（AO）特性对 dpotrf 函数的性能。图 15.20 显示了这些性能结果。对于分片 hStreams 版本，图中显示了三条不同的曲线，分别对应于不同的分片数 T 和流数（等于协处理器分区数）nstreams 取值。首先，我们注意到分片 hStreams 程序的性能对 T 和 nstreams 的选择很敏感。可以观察到，对于小矩阵，T = 6、nstreams = 5 的情况表现最佳；对于大矩阵，T = 10、nstreams = 3 的情况表现最佳。T = 8、nstreams = 5 的情况在整个矩阵尺寸范围内都表现出良好的性能。很难先验地预测对于给定的矩阵尺寸，这些参数的哪种组合是最佳的。这是因为存在与以下因素相关的复杂性：(a) 协处理器上的计算效率随矩阵尺寸变化而变化，且不同函数（即 dtrsm、dsyrk 和 dgemm）的敏感度不同；(b) 传输与计算的并发；(c) 总计算并发度的动态水平，它影响流或分区上计算的负载均衡。一般来说，较大的分片数应有利于隐藏数据传输延迟，如果计算任务的并发度是流数的整数倍，我们应能获得良好的负载均衡。然而，应该记住，总计算并发度是外层循环迭代索引的函数，如前所述。因此，最好对这些参数的一系列取值进行试验，以获得给定矩阵尺寸下的最佳值。我们还在图 15.20 中注意到，分片 hStreams 程序的性能低于 MKL AO 的性能。这是意料之中的，因为分片 hStreams 程序除了计算对角线分片上的 dpotrf（仅占总计算的一小部分）之外，并没有充分利用主机处理器，而 MKL AO 则很好地利用了主机处理器和协处理器卡。即便如此，有趣的是，在矩阵尺寸为 5000 到 10,000 之间时，分片 hStreams 的性能与 MKL AO 的性能相当接近。在不久的将来，当 hStreams API 增加了在主机处理器上运行流的能力时，我们应该能够同时充分利用处理器和协处理器，从而提升分片 hStreams 程序的性能。

# Cholesky  
分片 hStreams 在 Xeon 上的 dpotrf  

![](img/16cb41208935c5f22dd1044f03f2e31b_345_0.png)

### 图 15.20

![](img/16cb41208935c5f22dd1044f03f2e31b_346_0.png)

### 图 15.21

分片 hStreams 程序在分片数（T）和流数（nstreams）取不同值时的纯卸载性能，以及编译器卸载程序的纯卸载性能。同时还显示了仅协处理器计算的 dpotrf 性能。

为了更深入地了解分片以及并发调用传输和计算的好处，我们接下来展示另一组性能结果。在这些运行中，分片 hStreams 程序被修改为所有计算都在协处理器上进行，甚至包括对角线分片上的 dpotrf。为此，算法被稍作修改，并按照图 15.18 所示的任务图添加了一些不同的同步事件。我们将这种方法称为“纯卸载”（pure offload），因为主机完全不参与计算。图 15.21 显示了纯卸载模式下分片 hStreams 程序和 dpotrf 编译器卸载程序的性能。它还显示了 dpotrf（在完整的未分片矩阵上）的仅协处理器计算性能，该性能不包括传输时间，只包括协处理器上的时间。纯卸载分片 hStreams 程序和 dpotrf 编译器卸载程序的整体性能低于图 15.20 中所示分片 hStreams 程序和 dpotrf-MKL 自动卸载的相应数值，因为在纯卸载情况下主机不参与计算。我们再次注意到分片 hStreams 程序对参数 T 和 nstreams 的敏感性。只要参数选择得当，分片 hStreams 程序就能进一步隐藏数据传输延迟，其性能优于 dpotrf 编译器卸载版本。有趣的是，在最大的矩阵尺寸下，T = 10、nstreams = 3 的情况甚至优于仅协处理器计算的 dpotrf 情况。这表明分片算法相对于在未分片矩阵上调用 dpotrf 函数具有优势。

## LU 分解

我们希望到目前为止的示例已经充分说明了 hStreams 的用法，使您对这种异构机器编程方法产生兴趣。出于篇幅考虑，我们没有在书中介绍 hStreams 的一个重要的相关使用示例——LU 分解。对于 LU 分解，与 LAPACKE_mkl_dgetrfnpi 的主机原生运行相比，分片 hStreams 实现了 1.95 倍的性能，在
