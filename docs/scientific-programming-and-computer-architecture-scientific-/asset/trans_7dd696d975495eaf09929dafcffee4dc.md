
使用 `new[]()` 而不是 `MPI_Alloc_mem()`。如前所述，使用 `new[]` 分配内存是有原因。`MPI_Alloc_mem()` 会显式注册内存，虚拟内存中的页会在分配后立即分配给页帧。相比之下，使用 `new[]` 则保持请求分页。通过请求分页，页帧以接近内存的速度进行分配，这显著加快了 `Transpose` 类。。为了完整性，列出了类的析构函数。

```
Transpose::~Transpose(){
    delete[] fstM;
    delete[] fstN;
    delete[] sreqlist;
    delete[] rreqlist;
    delete[] sendbuf;
    delete[] recvbuf;
}
```

当每个进程调用一次成员函数 `transpose()` 时，存储在 P 个 MPI 进程上的矩阵就会被转置。该成员函数的定义概述了 `Transpose` 类的结构。

```
1 void transpose(double *localMN,
2 double *localNM){
3 TimeStamp clk;
4 clk.tic();
5 copyToSendbuf(localMN);
6 trans_timer.copy += clk.toc();
7
8 clk.tic();
9 postsend();
10 postrec();
11 wait();
12 trans_timer.mpi += clk.toc();
13
14 clk.tic();
15 copyFromrecvbuf(localMN);
16 trans_timer.rcopy += clk.toc();
17 }
```

## 6.3 MPI 示例

当前 MPI 进程持有的 $M \times N$ 矩阵部分位于 `localMN[]`（第 1 行）。由同一 MPI 进程持有的转置后的 $N \times M$ 矩阵部分。为了执行转置，每个进程将 `localMN[]` 拷贝到发送缓冲区（第 5 行），发送并接收（第 9 和 10 行），等待发送和接收完成（第 11 行），最后将其缓冲区拷贝到 `localNM[]`。第 11 行的 `wait()` 在第 9 和 10 行的发送和接收。该类并未尝试将跨网络通信与缓冲区拷贝进行重叠。网络与处理器活动的重叠是一种复杂的优化，我们将在本节末尾介绍。`transpose()` 的定义也显示了该类的一些计时基础设施。程序变量 `trans_timer` 是一个外部定义的结构。计时信息稍后省略。

## 发送数据

在矩阵转置期间，每个进程向每个进程发送一个块矩阵（见图 6.9）。块矩阵在拷贝到发送缓冲区或从接收缓冲区拷贝时必须经过转置。在发送之前进行转置。

转置函数的定义如下：

```
void transposedelta(double *in, int lda,
    long rows, long ncols,
    double *out){
    for(long i=0; i < rows; i++)
        for(long j=0; j < ncols; j++)
            out[j+i*ncols] = in[i+j*lda];
}
```

`array[]` 的主维度 $M$ 通常大于行数。然而，持有转置矩阵并对应发送缓冲区段的数组 `out[]` 主维度等于 `ncols`。注意内层循环体中 $i$ 和 $j$ 的交换。

## 436 第 6 章 特题：网络与消息传递

这不是转置矩阵的最佳程序，我们稍后会改进。成员函数 `copyToSendbuf()` 将 `localMN[]` 拷贝到发送缓冲区。

```
void Transpose::copyToSendbuf(double *localMN){
  long ncols = fN[p+1] - fN[p];
  for(long q=0; q < P; q++){
    long nrows = fM[q+1] - fM[q];
    long sbufindex = ncols * fM[q];
    long localindex = fM[q];
    long lda = M;
    transposew(localMN+localindex, lda,
    nrows, ncols,
    sendbuf+sbufindex);
  }
}
```

在第 2 行，`ncols` 初始化为本地存储的 $M \times N$ 矩阵的列数。本地 MPI 进程排名为 $p$，循环变量 $q$（第 3 行）遍历所有 P 个进程的排名。当前进程 $p$ 发送到排名 $q$ 进程的块矩阵行数在第 4 行使用 `fM[]` 计算。发送缓冲区的索引等于发送给排名小于 $q$ 的进程的总条目数（第 5 行）。`localMN` 的索引简单等于到达排名 $q$ 进程的第一列条目的索引。该条目的行数等于 `fM[q]`（第 7 行）。该函数的调用（第 9 到 11 行）通过将 `localindex` 加到 `localMN` 并设置 `lda` 为 $M$，提取出从当前排名 $p$ 进程发送到排名 $q$ 进程的子矩阵。

成员函数 `postend()` 以相同的方式使用 `fM[]` 和 `fN[]`。

```
void Transpose::postend(){
  long ncols = fN[p+1]-fN[p];
  for(int q=0; q < P; q++){
    long nrows = fM[q+1] - fM[q];
    long sbufindex = ncols * fM[q];
```
