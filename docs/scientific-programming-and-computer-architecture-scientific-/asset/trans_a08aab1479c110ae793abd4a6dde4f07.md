

# 第 6 章 特殊主题：网络与消息传递

```cpp
for(int j=0; j < ncols; j+=B){
    int iib = (nrows-i < B)?nrows-i:B;
    int jjb = (ncols-j < B)?ncols-j:B;
    for(int ii=0; ii < iib; ii++)
        for(int jj=0; jj < jjb; jj++)
            out[j+jj+(i+ii)*ncols]
                = in[i+ii+(j+jj)*lda];
}
```

该 for 循环分块实现了矩阵转置。在大规模问题中，大多数块是 $B \times B$，但在矩阵边缘处，块的大小通过 iib 和 jjb 进行了调整。外层循环使用 OpenMP 进行并行化。分块矩阵转置在第 4 和第 5 章中讨论过。这里块大小 $B = 50$ 的选择受到了之前讨论的影响。

`copywlda()` 的定义修改如下：

```cpp
void copywlda(double *in, int nrows, int ncols,
               double *out, int lda){
#pragma omp parallel for
    num_threads(THREADS)
    shared(in, nrows, ncols, out, lda)
    for(long j=0; j < ncols; j++)
        for(long i=0; i < nrows; i++)
            out[i+j*lda] = in[i+j*nrows];
```

修改更为简单。外层循环使用了 OpenMP 模型构造函数进行限定。

表 6.6 显示了通过使用更快的程序在缓冲区之间进行拷贝，带宽得到了显著提高。在主机上实现的双向带宽在所有情况下都大于 2.5 GB/s。当网络中有 100 台主机时，达到了 QDR Infiniband 标称带宽的 55%。

仍然有很大的改进空间。表 6.6 显示，在拷贝出缓冲区时，仍有近 30% 的周期被占用。虽然无法进一步改进拷贝，但我们可以尝试将 MPI 消息传递与拷贝操作重叠。

## 6.3. MPI 示例

| nprocs (or P) | M | N/P | b/w | send copy | MPI | recv copy |
|---|---|---|---|---|---|---|
| 10 | $5 \times 10^4$ | $5 \times 10^3$ | 0.93 | 16.9% | 68.6% | 14.5% |
| 20 | $5 \times 10^4$ | $5 \times 10^3$ | 0.81 | 15.1% | 71.1% | 13.0% |
| 50 | $5 \times 10^4$ | $5 \times 10^3$ | 0.76 | 13.7% | 74.3% | 12.0% |
| 100 | $5 \times 10^4$ | $5 \times 10^3$ | 0.82 | 14.1% | 72.3% | 13.6% |

表 6.6：在使用 OpenMP 线程级并行进行缓冲区进出拷贝后，每周期字节数的带宽改进情况。网络为 QDR Infiniband，主机为 3.33 GHz SSE2 机器（见表 A.1）。

| nprocs (or P) | M | N/P | b/w | send copy | MPI | recv copy |
|---|---|---|---|---|---|---|
| 10 | $5 \times 10^4$ | $5 \times 10^3$ | 1.39 | 27% | - | 24% |
| 20 | $5 \times 10^4$ | $5 \times 10^3$ | 1.14 | 23% | - | 20% |
| 50 | $5 \times 10^4$ | $5 \times 10^3$ | 1.22 | 23% | - | 21% |
| 100 | $5 \times 10^4$ | $5 \times 10^3$ | 1.11 | 19% | - | 20% |

表 6.7：当网络活动与处理器活动以及快速拷贝重叠时，每周期字节数的带宽。通过 3.33 GHz 的时钟频率获得 GB/s 的带宽。网络为 QDR Infiniband，所有主机均为 12 核 3.33 GHz SSE2 机器（见表 A.1）。

## 重叠网络与处理器活动

表 6.7 显示了在如文所述的利用快速拷贝之外，将网络活动与处理器活动重叠时带宽的提升。在具有 100 个节点的情况下，实现的网络带宽达到了 5 GB/s 峰值的 75%。在 10 个节点时，实现的带宽超过了峰值的 90%。

新类 `FastTrans` 展示了如何将网络活动与处理器活动重叠。

```cpp
class FastTrans{
  private:
    int p; // rank
    int P; //number of processes
    long M;
    long N;
    long *fstM;
    long *fstN;
    double *sendbuf, *recvbuf;
    MPI_Request *sreqlist, *reqlist;
    int *sender;
    int *rcvd_list;

public:
    FastTrans(int rank, int nprocs, long Mi, long Ni);
    FastTrans();
    long fstM(int rank){return fstM[rank]};
    long fstN(int rank){return fstN[rank]};
    void copyToSendbuf(int q, double *localMN);
    void postsend(int q);
    void postrecv(int q);
    void wait(); /* wait on all sends */
    void copyFromrecvbuf(int q, double *localMN);
    void transpose(double *localMN);
};
```

`FastTrans` 类在许多方面上与 `Transpose` 类相似，尽管存在一些变化。在私有部分，有两个新项：`sender` 和 `rcvd_list`。成员函数 `transpose()` 用于排序发送并跟踪接收。在公共部分，`postsend()` 和 `postrecv()` 接收参数 `q`。发送和接收请求不再同时启动。成员函数 `transpose()` 将发送和接收与处理器活动重叠。数组 `sender` 由类构造函数初始化。

```cpp
FastTrans::FastTrans(int rank, int nprocs, long Mi, long Ni)
    :p(rank), P(nprocs), M(Mi), N(Ni) {
    fstM = new long[P+1];
    fstN = new long[P+1];
    BlockDivide(M, P, fstM);
    BlockDivide(N, P, fstN);
    long ncols = fstN[p+1]-fstN[p];
    long nrows = fstM[p+1]-fstM[p];
    assert(ncols > 0);
    sendbuf = new double[ncols*M];
    assert(nrows > 0);
    recvbuf = new double[nrows*N];
    sreqlist = new MPI_Request[P];
    reqlist = new MPI_Request[P];
    sender = new int[P];
    rcvd_list = new int[P];
    sender[0] = 0;
    for(int i=0; i < P/2 + P%2; i++) {
        sender[2*(i-1)+1] = i;
        sender[2*(i-1)+2] = P-i;
    }
    if(P%2 == 0) {
        sender[P-1] = P/2;
    }
    for(int i=0; i < P; i++) {
        sender[i] = (sender[i]+p)%P;
    }
}
```

`fstM[]` 和 `fstN[]` 的索引初始化在 `Transpose` 类中。发送和接收缓冲区的大小与之前相同。然而，发送和接收的方式完全不同。在第 23 到 29 行，`sender[]` 数组初始化为 `0, 1, P-1, 2, P-2, 3, ...`。

这种发送顺序假设本地进程 `p = 0`。为了获取当前进程 `p` 的发送顺序，第 31 和 32 行的 for 循环通过加上 `rank p` 来修改 `sendorder[]`，其中 `P` 是 MPI 进程总数。

发送顺序假设进程 `p` 紧邻 `(p-1) mod P` 和 `(p+1) mod P`。事实上，处理器到节点的分配可能是随机的。尽管如此，不同进程之间的发送顺序似乎存在某些收益。

给出析构函数的定义以保持完整。

```cpp
FastTrans::~FastTrans(){
    delete[] fstm;
    delete[] fstn;
    delete[] sreqlist;
    delete[] reqlist;
    delete[] sendbuf;
    delete[] recvbuf;
    delete[] sendorder;
    delete[] rcvd_list;
}
```

`copyTosendbuf()` 和 `copyFromrecvbuf()` 的定义与之前相同，但它们接收索引 `q`。它们只拷贝发送到或从 `rank q` 接收的矩阵部分。

```cpp
void FastTrans::copyTosendbuf(int q, double *localMN) {
    long ncols = fstn[p+1] - fstn[p];
    long rows = fstm[q+1] - fstm[q];
    long sbufindex = ncols * fstm[q];
    long localindex = fstm[q];
    long lda = M;
    transposewlda(localMN+localindex, lda,
        rows, ncols,
        sendbuf+sbufindex);
}
```

```cpp
void FastTrans::copyFromrecvbuf(int q, double *localNM){
  long ncols = fstm[p+1]-fstm[p];
  long nrows = fstN[q+1]-fstN[q];
  long Alphaindex = ncols*fstN[q];
  long localindex = fstN[q];
  long lda = N;
  copywlda(recvbuf+rbufindex, nrows, ncols,
localNM+localindex, lda);
}
```

与 `Transpose` 类对应的成员函数不同，这些成员函数没有使用 for 循环与每个其他 MPI 进程通信。因此，它们更加透明。`transpose()` 和 `copywlda()` 函数与之前的版本完全相同，此处省略。成员函数 `postend()` 和 `postrec()` 与另一个为 `rank q` 的进程通信。

```cpp
void FastTrans::postend(int q){
  long ncols = fstm[p+1]-fstN[p];
  long nrows = fstm[q+1]-fstm[q];
  long sbufindex = ncols*fstm[q];
  int count = ncols*nrows; //MPI无法处理long
  int tag = 0;
  MPI_Isend(sendbuf+sbufindex, count, MPI_DOUBLE,
  q, tag, MPI_COMM_WORLD, sreqlist+q);
}
```

```cpp
void FastTrans::postrec(int q){
  long ncols = fstm[p+1]-fstm[p];
  long nrows = fstN[q+1]-fstN[q];
  long Alphaindex = ncols*fstN[q];
  int count = nrows*ncols; //MPI无法处理long
  int tag = 0;
  MPI_Irec(recvbuf+rbufindex, count, MPI_DOUBLE,
  q, tag, MPI_COMM_WORLD, rreqlist+q);
}
```

