using new[](), rather than MPI_Alloc_mem(). As mentioned earlier, there is a reasonor allocating with new[]. MPI_Alloc_mem() would register memory explicitly, and
pages in virtual memory would also be assigned to page frames immediately after
allocation. With new[(), in contrast, demand paging remains in place. With demand
paging, page frames are assigned in near memory speeds up the Transpose class significantly.
The class destructor is listed for the sake of completeness.

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

A matrix stored across P MPI process is transposed when each process makes
a single call to the member function transpose(). The definition of that member
function gives an overview of the Transpose class.

```
1 void transpose(double *localMN,
2 double *localMN){
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
15 copyFROMrecvbuf(localMN);
16 trans_timer.rcopy += clk.toc();
```