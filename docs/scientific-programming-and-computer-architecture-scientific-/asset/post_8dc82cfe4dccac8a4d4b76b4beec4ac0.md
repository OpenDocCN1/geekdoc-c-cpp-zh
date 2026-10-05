
# 6.3. MPI examples

advantageous to adopt such a design. Data not to be copied into send buffers or out of receive buffers. Applications such as 2D or 3D finite differences on a regular rectangular grid are amenable to this type of design.

The more difficult scenario is when the data is irregular, or structured but changes format from the sender and the receiver, as in matrix transpose. In these scenarios, the MPI application has to copy into send buffers and out of receive buffers. The way buffering is handled becomes as important as it is in the TCP/IP protocol stack or the hardware implementation of the Infiniband network architecture. The matrix transpose program uses buffering to handle the change in data layout between the matrix at the sending MPI process and the transposed matrix at the receiving process.

## Balanced matrix partitions

If an m × n matrix is stored in column-major order, with a leading dimension to column size in the array[], the (i,j)th entry of the matrix is a[i+j*m]. In row-major order, the (i,j)th entry is a[j+i*n]. If the matrix is transposed and stored in column-major order, the (j,i)th entry of the transposed matrix would be at[j+i*n]. On a single computer, transposing a matrix is equivalent to switching from column-major order to row-major order.

Figure 6.9 shows a matrix is partitioned along columns as well as rows. If the global M × N, it is partitioned across P MPI processes by allocating approximately N/P columns each. Each process gets a contiguous set of columns. Matrix transposition is equivalent to switching the partitioning scheme from columnwise to rowwise, with a twist. As shown in the figure, the set of columns of process P$_i$ intersects the set of rows of process P$_j$ in a block matrix. During matrix transposition, this block must be transmitted from process P$_i$ to process P$_j$. Bidirectional data transfer occurs between every pair of processes.

The twist arises that. Every block that is transmitted must be transposed. The block that is stored in column-major order with leading dimension equal to M, the column size of the global matrix. When it is transposed and stored, the lead dimension changes to N, the row size of the global matrix.

The function BlockDivide(), defined below, is used for columnwise as well as rowwise partitioning.

```cpp
void BlockDivide(long n, int P, long *fst){
  long Q = n/P;
```

# 430 Chapter 6. Special Topic: Networks and Message Passing

| | P0 | P1 | P2 | P3 |
|---|---|---|---|---|
| P0 | | | | |
| P1 | | | B | |
| P2 | | | | |
| P3 | A | | | |

Figure 6.9: Columnwise and rowwise matrix partitions of a matrix between four processor nodes. When the column partitioning is switched to rowwise partitioning, submatrix blocks must be transmitted between nodes. For example, the block labeled A must be sent from $P0$ to $P3$ and the block labeled B must be sent from $P3$ to $P1$.

```cpp
3 long R = n-Q*P;
4 fst[0] = 0;
5 for(int p=0; p < R; p++)
6 fst[p+1] = fst[p] + (Q+1);
7 for(int p=R; p < P; p++)
8 fst[p+1] = fst[p]+Q;
9 }
```

BlockDivide() partitions $n$ items between $P$ processes. The partitioning is stored in the array fst[]. The number of items that each process gets would be exactly equal to the quotient $Q=n/P$ (line 2) if the remainder $R=n-QP$ (line 3) were zero. If $0, 1, \dots, n-1$ are the $n$ items, items $i$ assigned to process $p$ lie in the interval fst[p] $\le i <$ fst[p+1]. Equivalently, the assignment to process $p$ begins in **fst[p]**. The for-loop on lines 5 and 6 assigns $Q$ items to each of the first $R$ processes. The remaining $P-R$ processes are assigned $Q$ items by the for-loop on lines 7 and 8.

It must be noted that fst[] is an array with $P+1$ entries, although there are only $P$ processes. The entry **fst[P]** always gets set to $n$.

The division of work between the processes is nearly balanced. Some of the processes get at most one extra item. When the number of items (columns and rows in matrix transposition) is large, as it must be for parallelization to be meaningful, the slight imbalance by a single item will be inconsequential.

The general principles of algorithm design assume a highly simplified but still pertinent model of the computer. General principles that have a direct bearing on parallel programming are few. Load balancing is one of them. Load balancing requires that work be nearly evenly partitioned between processes that utilize powerful hardware. The speed of a parallel program is determined by the slowest process, which is the one with the highest load.

The principal of balancing the load is no more than common sense. Indeed, it barely requires knowledge of arithmetic. It must not be taken lightly because the consequences of ignoring it can be severe. For example, a careless division of $n$ items between $P$ processes may assign $Q+R$ items to $P_0$ and $Q$ items to all others. If $n$ is much larger than $P^2$, $Q$ will be much larger than $R$, and the resulting imbalance will not be too great. However, if $n$ is of the order of $P^2$, which is not unrealistic, $P_0$ may end up with nearly twice the work of any other process.

## The Transpose class

The Transpose class defined below does not hold any part of the matrix to be transposed nor it store the transposed matrix. It sends and receive buffers a few other items. It provides public member functions for data transfers that arise during matrix transpose and to copy data from matrices to its own buffers.

```cpp
class Transpose{
private:
    int p; //process rank
    int P; //number of processes
    long M;
    long N;
    long *fstM;
    long *fstN;
    double *sendbuf, *recvbuf;
    MPI_Request *sreqlist, *rreqlist;
public:
```

# Chapter 6. Special Topic: Networks and Message Passing

```cpp
13    Transpose(int rank, int nprocs, long Mi, long Ni);
14    ~Transpose();
15    long fstM(int rank){return fstM[rank];};
16    long fstN(int rank){return fstN[rank];};
17    void copyTosendbuf(double *localMN);
18    void postsend();
19    void postrecv();
20    void wait();
21    void copyFromrecvbuf(double *localNM);
22    void transpose(double *localMN, double *localNM);
23 };
```

This class stores just enough data to implement the matrix transpose. It stores the process rank (p on line 3), the total number of MPI processes (P on line 4), and dimensions of the global matrix (M and N on lines 5 and 6). The arrays fstM (line 7) and fstN[] (line 8) are used to partition the matrix. The public interface to the Transpose class consists of the constructor, destructor, and functions to step through. There is also a single member function, transpose() (line 21), for effecting the transposition. The two arguments of this member function are localMN[], which stores the local part of the M x matrix, and localNM[], which stores the N x matrix. The constructor is defined as follows:

```cpp
1 Transpose::Transpose(int rank, int nprocs, long Mi, long Ni)
2                             :p(rank), P(nprocs), M(Mi), N(Ni)
3 {
4     fstM = new long[P+1]; fstN = new long[P+1];
5     BlockDivide(M, P, fstM);
```

# 6.3. MPI examples

```cpp
7 BlockDivide(N, P, fstN);
8 long ncols = fstN[p+1]-fstN[p];
9 long nrows = fstM[p+1]-fstM[p];
10
11 assert(ncols > 0);
12 sendbuf = new double[ncols*M];
13
14 assert(nrows > 0);
15 recvbuf = new double[nrows*N];
16
17 sreqlist = new MPI_Request[P];
18 rreqlist = new MPI_Request[P];
19 }
```

The constructor uses BlockDivide() to calculate the entries of fstM[] (line 6) and fstN[] (line 7). The matrix is partitioned columnwise, and the columns held by process of rank p indices

> fstN[p] ≤ j < fstN[p+1].

When the matrix is transposed, it is in effect partitioned rowwise (see figure 6.9), and the rows it will hold indices

> fstM[p] ≤ i < fstM[p+1].

The number of columns ncols of the matrix and the number of rows nrows of the transposed matrix held on the current process of rank p is calculated on lines 8 and 9, respectively.

The send buffer is allocated on line 12. Each process sends out all the data it holds (we do not attempt to optimize for the diagonal blocks that remain on the processor node). Thus, the size of the send buffer, which is ncols*M on line 12, accounts for every column and every entry of the matrix held by the process. For similar reasons, the size of the receive buffer on line 15 is nrows*N, accounting for every entry of the transposed matrix held by the process.

The discussion extoling the benefits of registering memory explicitly in section 6.3.1, it may seem a bit strange that the send and receive buffers are allocated-
