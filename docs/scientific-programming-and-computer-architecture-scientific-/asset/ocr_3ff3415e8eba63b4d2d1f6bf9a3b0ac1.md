# 6.3. MPI examples

```
void Jacobi2D::copypp(){
    #pragma omp parallel \
    num_threads(nthreads)
    default(shared)
    {
        int tid = omp_get_thread_num();
        int col1 = tid*dim2/nthreads;
        int col2 = (tid+1)*dim2/nthreads;
        this->copy(col1, col2);
    }
}
```

The structure of the member functions copypp() and copy() is similar to that of member functions used for default initialization and carrying out the Jacobi iteration. The division of work between threads is by columns and is done the same way while copying, initializing, or updating. Dividing data between columns the same way ensures that the threads access near memory of the time, assuming the object is initialized using the member function initialize() soon after it is created. If it is not initialized appropriately, the program will be much slower.

# Iterating with the Jacobi class

The function for iterating and timing the Jacobi2D class looks as follows:

```
double time_jacobi(int rank, int nprocs,
    int dim1, int dim2,
    int nitns){
    int nth = get_nthreads();
    Jacobi2D jacobi(rank, nprocs, dim1, dim2, nth);
    jacobi.initializepp();
    TimeStamp clk;
    clk.tic();
    for(int i=0; i < nitns; i++){
        jacobi.postsendrecv();
        jacobi.wait();
        jacobi.updatepp();
}
```