
# Chapter 6. Special Topic: Networks and Message Passing

| P | n | allreduce | send/recv |
|---|---|---|---|
| 10 | 1 | $3.4 \times 10^4 | 4.2 \times 10^4 |
| 10 | $10^6$ | $3.7 \times 10^7 | 8.7 \times 10^7 |
| 20 | 1 | $4.6 \times 10^4 | 5.6 \times 10^4 |
| 20 | $10^6$ | $3.8 \times 10^7 | 1.0 \times 10^8 |
| 50 | 1 | $7.1 \times 10^4 | 7.7 \times 10^4 |
| 50 | $10^6$ | $4.1 \times 10^7 | 1.2 \times 10^8 |
| 100 | 1 | $8.9 \times 10^4 | 9.6 \times 10^4 |
| 100 | $10^6$ | $5.1 \times 10^7 | 1.5 \times 10^8 |

Table 6.11: The number of cycles consumed by reduction on $P$ processes, per host, on QDR Infiniband with each host a 3.33 GHz SSE2 machine (see table A.1). The data on each process is a double array of size $n$. The MPI function is compared with a send/receive implementation.

and deposits the result with either one or all the processes. The following function illustrates MPI reduction capability:

```c
double reducin(int rank, int nprocs,
    double *sendbuf, double *recbuf,
    int bufsize){
    Timestamp clk;
    clk.tic();
    MPI_Allreduce(sendbuf, recbuf, bufsize,
        MPI_DOUBLE, MPI_MIN, MPI_COMM_WORLD);
    double cycles = clk.toc();
    return cycles;
}
```

The array sendbuf[] stores the data to be reduced. The effect of calling the MPI library function MPI_Allreduce() is to gather the sendbuf[] array from all the processes, apply a reduction operation, and store the result in the recbuf[]. All processes must call reducin() to initiate the reduction. The reduction operation is given as MPI_MIN.

Table 6.11 shows that using MPI_Allreduce() is nearly three times faster than a send/receive implementation that does not overlap processor activity with network activity.

## 6.3. MPI examples

Details of that tree-based implementation are omitted.

### 6.3.5 Parallel I/O in MPI

In parallel I/O, a number of MPI processes simultaneously write to or read from the same file. Typical file systems lock a file when it is being accessed by one process, which precludes other processes from accessing it. Parallel I/O is possible only if the file system allows it.

For parallel I/O to be meaningful, the file system must be capable of storing or striping a single file across multiple hard disks. If the entire file is stored on a single hard disk, accesses from multiple processes will have to be serialized, and parallel I/O from multiple processes will not bring any great advantage.

MPI syntax for parallel I/O is quite complicated. We step through the syntax for once writing and for reading a file in parallel. For both writing and reading, we exhibit and exercise MPI functionality for parallel I/O in its simplest form. The function `write_mpi()` defined below is called simultaneously by MPI processes to write to a file in parallel. The data will be written to the array of bytes `data[]` of length `len`, `data[]` and `len` using `write_mpi()`. The other two arguments to `write_mpi()` are `fname`, which is the name of the file, and `disp`. Because many processes may write to the same file, each process must specify its view of the file. A process's view of the file is the part of the file that is visible to it. The final argument `disp` specifies the beginning of the file as an absolute displacement (in bytes) from the beginning of the file. It must be noted that both `len` and `disp` are of type long and not int. An int can count up to $2^{31}-1$, which is not enough for files that go up to terabytes or petabytes.

```c
void write_mpi(void *data, long len,
    char *fname, long disp){
    MPI_File file;
    MPI_File_open(MPI_COMM_WORLD,
        fname,
        MPI_MODE_CREATE|MPI_MODE_WRONLY,
        MPI_INFO_NULL,
        &file);
    char datarep[200];
    sprintf(datarep, "native");
    MPI_File_set_view(file,
    disp,
    MPI_BYTE,
    MPI_BYTE,
    datarep,
    MPI_INFO_NULL);
    long offset = 0;
    int maxcount = 2000*1000*1000;
    while (len > 0) {
        int count = (len<maxcount)?len:maxcount;
        MPI_File_write_at(file,
        offset,
        data,
        count,
        MPI_BYTE,
        MPI_STATUS_IGNORE);
        offset += count;
        data = ((char*)data+count);
        len -= count;
    }
    MPI_File_close(&file);
}
```
