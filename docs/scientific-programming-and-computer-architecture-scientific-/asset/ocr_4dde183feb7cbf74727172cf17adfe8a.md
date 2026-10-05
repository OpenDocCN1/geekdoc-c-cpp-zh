# 6.3. MPI examples

```
double *al = a + dim1;
double *ar = a + dim1*dim2;
double *right = a + dim1*(dim2+1);
MPI_Send_init(al, dim1, MPI_DOUBLE, lrank, tag,
    MPI_COMM_WORLD, reqlist+0);
MPI_Send_init(ar, dim1, MPI_DOUBLE, rrank, tag,
    MPI_COMM_WORLD, reqlist+1);
MPI_Recv_init(left, dim1, MPI_DOUBLE, lrank, tag,
    MPI_COMM_WORLD, reqlist+2);
MPI_Recv_init(right, dim1, MPI_DOUBLE, rrank, tag,
    MPI_COMM_WORLD, reqlist+3);

```

This constructor uses the same tag for both left-going and right-going messages, unlike the constructor for the Cycle class. The Jacobi2D class must be used only when the number of MPI processes is greater than two. The dimensions dim1 and dim2 are assumed to be divisible by two and nthreads, respectively, the number of threads is also assumed to be divisible by two to reduce clutter in the implementation.

The arrays left[] and right[] point to the leftmost and rightmost columns (dashed columns in figure 6.8). The arrays al[] and ar[] point to the leftmost and rightmost columns "owned" by the current node. The array al[] is sent to the node on the left of rank lrank, and the array ar[] is sent to the node on right of rrank. Data from the left is received into left and data from the right goes into right. The pattern of communication is as shown in figure 6.8.

The definition of the destructor is included for completeness.

```
Jacobi2D::~Jacobi2D() {
    assert(gl_mpi_inoff == MPION);
    MPI_Request_free(reqlist+0);
    MPI_Request_free(reqlist+1);
    MPI_Request_free(reqlist+2);
    MPI_Request_free(reqlist+3);
    delete[] a;
    delete[] b;
}

```