
## 6.3. MPI examples

### All-to-all data transfer

MPI_Scatter() has the following prototype

```
int MPI_Scatter(void *, int, MPI_Datatype,
               void *, int, MPI_Datatype,
               int, MPI_Comm)
```

A call can be made as in

```
MPI_Scatter(sendbuf, n, MPI_DOUBLE, recvbuf, n,
             MPI_DOUBLE, root, MPI_COMM_WORLD)
```

In this case, the count sendbuf and the count recvbuf are both given as n. The meaning of the call is somewhat opaque partly because this is a collective call and partly because the syntax is not suggestive of the role played by root. Each process has to supply a recvbuf, but only the root needs to supply a valid sendbuf. The sendbuf supplied by the other processes is ignored.

The other complication in MPI_Scatter() is related to the send and receive counts (these are given as n in the call and their interpretations). The relation of receive count to receive buffer is easier to understand. On each process, including the root, recvbuf[] must be large enough to hold n items. The size of sendbuf[] on the root must be n*nprocs items (the WORLD communicator) and not just n items. The effect of this collective call is to copy items r*n through (r+1)*n-1 in the sendbuf[] of the root to the recvbuf[] of the process r for every value of r.

The amount of data sent should be exactly equal to the amount of data received. Why then does the function ask for both a send count and a receive count? In principle, the data types could be different for different receiving processes, and the syntax allows for that. It is uncommon to use different data types at the sender and receiver, or to use anything other than WORLD as the communicator, MPI syntax burdens every single usage with its rules for data types and communicators. Like any library, MPI has its imperfections. These imperfections exist partly because MPI came into prominence in the early days of parallel computing and has been widely used since. As with the x86 architecture and its tortured instruction encoding, success comes with a cost.

The following function illustrates usage of MPI_Scatter():

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

This function must be called simultaneously by all the processes. Both sendbuf[] and recvbuf[] must be of length $n \times process$. In this function, each process takes its turning the root. The data in sendbuf[] of all processes may be arranged in matrix with one column per process:

$\begin{matrix} a_{00} & a_{01} & \dots \ a_{10} & a_{11} & \dots \ \vdots & \vdots & \vdots \ & & a_{nprocs-1,n} \end{matrix}$

Here, the sendbuf[] of the process of rank $r$ is listed in column $r$. The entry $a_{ir}$ represents

```
sendbuf[*n], . . . , sendbuf[(i+1)*n-1]
```

in the sendbuf[] array of the process of rank $r$. The effect of the collective invocation of the function is to copy the data in row $i$ of the matrix to the recvbuf[] of the process of rank $i$. In particular, the entry $a_{ir}$ is copied to

```
recvbuf[*n], . . . , recvbuf[(r+1)*n-1]
```

in the recvbuf[] array of the process of rank $i$.

The MPI library provides a single function call that effects this all-to-all transfer of data. Its usage is as shown below.

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

Table 6.10: Bandwidth in bytes/cycle for three implementations of all-to-all transfer on P MPI processes, one per computer. Multiply by 3.33Z to get bandwidth in GB/s. The network was QDR Infiniband, and each computer was a 3.33 GHz SSE2 machine (see table A.1). Data consisting of $n$ double-precision numbers is exchanged between every pair. The reported numbers are medians.

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

Once again the number of items in the data transfer must be indicated as $n$ for both sendbuf[] and recvbuf[] as MPI allows send and receive data types to be different in general, a facility we never use.

Table 6.10 shows that all-to-all Alltoall() with repeated calls to MPI_Scatter(). Both collective functions are blocking calls, but the transfer of data in each scatter operation is from the root to other processes. The scatter operations do not utilize the bidirectional nature of the.

## Chapter 6. Special Topic: Networks and Message Passing

The bandwidth is, as always, measured as the number of bytes transferred into out of a single computer (which is for convenience the MPI process of rank 0) in a single cycle. The all-all implementation fails rapidly as the number of processes increases (see table 6.10). In contrast, the scatter implementation process takes its turn to be root, which serializes network traffic.

As shown by the table, a send/receive implementation must use MPI_Startall() to do that well. Certain Infiniband vendors support technology that allows to initiate sends and receives simultaneously.¹⁴An example of such a is CORE-Direct available on ConnectX-2 hardware from Mellanox.

Because the plan is to initiate sends and receives simultaneously, MPI_Isend() and MPI_Irecv() are not appropriate. Instead, the send/receive implementation of all-to-all transfer begins by initializing sends and receives in another function.

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

This function returns an array of 2*nprocs objects of type MPI_Request. A request is created for sending and receiving from each process. In this implementation, a process sends data to itself using MPI messages. The request objects are destroyed, when no longer needed. The send/receive implementation of all-to-all transfer is completed by the following function definition:

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

The MPI library function MPI_Startall() sends all the requests to the MPI library in one batch. At that point, it is up to the Open MPI library (or the network hardware) to sequence the requests intelligently and issue RDMA requests promptly.

```cpp
void all2all_finalize(MPI_Request *reqlist){
    delete [reqlist];
}
```

# Reduce

If $f(x_0,...,x_{P-1})$ takes the minimum, maximum, or sum of its arguments, the reduce operation based on $f$ gathers data $x_r$ from each process of rank $r$, $0 \le r < P$,
