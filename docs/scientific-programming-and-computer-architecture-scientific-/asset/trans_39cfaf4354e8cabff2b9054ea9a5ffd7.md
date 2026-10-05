

## 6.3. MPI 示例

 全对全数据传输 (All-to-all data transfer)

MPI_Scatter() 具有以下原型：

```
int MPI_Scatter(void *, int, MPI_Datatype,
               void *, int, MPI_Datatype,
               int, MPI_Comm)
```

可以如下所示进行调用：

```
MPI_Scatter(sendbuf, n, MPI_DOUBLE, recvbuf, n,
             MPI_DOUBLE, root, MPI_COMM_WORLD)
```

在这种情况下，`sendbuf` 的计数和 `recvbuf` 的计数都给于 `n`。该调用的意义有些模糊，部分是因为这是一个集合调用（collective call），部分是因为语法没有体现出 `root` 所扮演的角色。每个进程都必须提供一个 `recvbuf`，但只有 `root` 需要提供一个有效的 `sendbuf`。其他进程提供的 `sendbuf` 会被忽略。

`MPI_Scatter()` 的另一个复杂之处与发送和接收计数有关（这些在调用中给出 `n`，其解释也不同）。接收计数与接收缓冲区之间的关系更容易理解。在包括 root 在内的每个进程上，`recvbuf[]` 必须足够大以容纳 `n` 个项目。root 上的 `sendbuf[]` 必须是 `n*nprocs` 个项目（WORLD 通信器），而不仅仅是 `n` 个。此集合调用的效果是对于每一个 `r` 值，将 `sendbuf[]` 中从 `r*n` 到 `(r+1)*n-1` 的项目拷贝到进程 `r` 的 `recvbuf[]` 中。

发送的数据量与接收的数据量完全相等。为什么函数还要请求发送计数和接收计数呢？原则上，不同的接收进程可以使用不同的数据类型，语法也允许这样做。在发送端和接收端使用不同的数据类型，或者使用除 WORLD 以外的通信器并不常见，MPI 语法通过其数据类型和通信器的规则给每一次使用都加上了负担。像任何库一样，MPI 也有其不完美之处。这些不完美之处部分是因为 MPI 在并行计算早期兴起并从那时起被广泛使用。正如 x86 架构及其扭曲的指令编码一样，成功是有代价的。

以下函数说明了 `MPI_Scatter()` 的用法：

```cpp
double scatter_all2all(int rank, int nprocs,
double *sendbuf, double *recvbuf,
int n){
    Timestamp clk;
    clk.tic();
    for(int root=0; root < nprocs; root++){
    MPI_Scatter(sendbuf, n, MPI_DOUBLE,
    recvbuf+n*root,n,MPI_DOUBLE,
    root,MPI_COMM_WORLD);
    }
    double cycles = clk.toc();
    return cycles;
}
```

此函数必须由所有进程同时调用。`sendbuf[]` 和 `recvbuf[]` 的长度必须为 $n \times process$。在这个函数中，每个进程轮流担任 root。所有进程的 `sendbuf[]` 中的数据可以排列成矩阵，每个进程占一列：

$\begin{matrix} a_{00} & a_{01} & \dots \ a_{10} & a_{11} & \dots \ \vdots & \vdots & \vdots \ & & a_{nprocs-1,n} \end{matrix}$

在这里，rank 为 $r$ 的进程的 `sendbuf[]` 列在第 $r$ 列。项 $a_{ir}$ 代表

```
sendbuf[*n], . . . , sendbuf[(i+1)*n-1]
```

在 rank 为 $r$ 的进程的 `sendbuf[]` 数组中。该函数集合调用的效果是将矩阵中第 $i$ 行的数据拷贝到 rank 为 $i$ 的进程的 `recvbuf[]` 中。特别是，项 $a_{ir}$ 被拷贝到：

```
recvbuf[*n], . . . , recvbuf[(r+1)*n-1]
```

在 rank 为 $i$ 的进程的 `recvbuf[]` 数组中。

MPI 库提供了单一函数调用来实现这种全对全的数据传输。其用法如下所示。

| P | n | scatter | send/recv | alltoall |
| :--- | :--- | :--- | :--- | :--- |
| 10 | $10^5$ | 0.27 | 1.45 | 1.53 |
| 10 | $10^6$ | 0.27 | 1.54 | 1.56 |
| 20 | $10^5$ | 0.13 | 1.07 | 1.13 |
| 20 | $10^6$ | 0.13 | 1.12 | 1.14 |
| 50 | $10^5$ | 0.05 | 1.23 | 1.35 |
| 50 | $10^6$ | 0.05 | 1.34 | 1.41 |
| 100 | $10^5$ | 0.02 | 1.03 | 1.16 |
| 100 | $10^6$ | 0.02 | 1.09 | 1.19 |

表 6.10：在 P 个 MPI 进程上（每台计算机一个）三种全对全传输实现的带宽（单位字节/周期）。乘以 3.33Z 得到 GB/s 带宽。网络是 QDR Infiniband，每台计算机都是 3.33 GHz SSE2 机器（见表 A.1）。由 $n$ 个双精度数字组成的数据在每对进程之间交换。报告的数字是位数。

```cpp
double mpi_all2all(int rank, int nprocs,
    double *sendbuf, double *recvbuf,
    int n){
    TimeStamp clk;
    clk_tic();
    MPI_Alltoall(sendbuf, n, MPI_DOUBLE, recvbuf, n,
MPI_DOUBLE, MPI_COMM_WORLD);
    double cycles = clk_toc();
    return cycles;
}
```

再次，数据传输中的项目数必须对 `sendbuf[]` 和 `recvbuf[]` 都指示为 $n$，因为 MPI 通常允许发送和接收数据类型不同，我们从不使用这种功能。

表 6.10 显示了通过重复调用 `MPI_Scatter()` 实现的全对全 `Alltoall()`。这两个集合函数都是阻塞调用，但每次 scatter 操作中的数据传输都是从 root 到其他进程的。scatter 操作没有利用双向性。

## 第 6 章 特殊主题：网络与消息传递

带宽一如既往，测量为单周期内进出单台计算机（为了方便起见，指为 0 的 MPI 进程）的字节数。随着进程数量的增加，all-all 实现迅速失效（见表 6.10）。相比之下，scatter 实现进程轮流担任 root，这串行了网络流量。

如表所示，scatter 实现必须使用 `MPI_Startall()` 来这样做。某些 Infiniband 厂商支持允许同时发送和接收的技术⁴例如 Mellanox 的 ConnectX-2 硬件。

由于计划是同时发送和接收，`MPI_Isend()` 和 `MPI_Irecv()` 并不合适。相反，全对全发送/接收实现通过另一个函数初始化发送和接收：

```cpp
MPI_Request *all2all_init(int rank, int nprocs,
double *sendbuf, double *recvbuf,
int n) {
    MPI_Request *reqlist = new MPI_Request[2*nprocs];
    for(int i=0; i < nprocs; i++) {
        int dest = i;
        int tag = rank;
        MPI_Send_init(sendbuf+dest*n, n, MPI_DOUBLE,
        dest, tag, MPI_COMM_WORLD, reqlist+i);
    }
    for(int i=0; i < nprocs; i++) {
        int source = i;
        int tag = source;
        MPI_Recv_init(recvbuf+source*n,n,MPI_DOUBLE,
        source, tag, MPI_COMM_WORLD,
        reqlist+nprocs+i);
    }
    return reqlist;
}
```

此函数返回一个包含 2*nprocs 个 `MPI_Request` 对象的数组。为每个发送和接收创建一个请求。在这种实现中，进程使用 MPI 消息向自己发送数据。不再需要时销请求对象。全对全发送/接收实现通过以下函数定义完成：

```cpp
double all2all(int rank, int nprocs, MPI_Request*
    reqlist){
    TimeStamp clk;
    clk.tic();
    MPI_Startall(2*nprocs, reqlist);
    MPI_Waitall(2*nprocs, reqlist, MPI_STATUS_IGNORE);
    double cycles = clk.toc();
    return cycles;
}
```

MPI 库函数 `MPI_Startall()` 将所有请求一次性发送到 MPI 库。此时，由 Open MPI 库（或网络硬件）智能地安排请求并及时发布 RDMA 请求。

```cpp
void all2all_finalize(MPI_Request *reqlist){
    delete [reqlist];
}
```

# 归约 (Reduce)

如果 $f(x_0,...,x_{P-1})$ 取参数的最小值、最大值或和，则基于 $f$ 的归约操作从每个 rank 为 $r$ 的进程（$0 \le r < P$）收集数据 $x_r$，

