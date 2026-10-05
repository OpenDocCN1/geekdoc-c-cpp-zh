# Chapter 6. Special Topic: Networks and Message Passing

```
double* recvbuf,
int bufsize){nnTimeStamp clk;
int tag = 0;
double cycles=0;
MPI_Request req1, req2;
int other = (rank==0)?nprocs-1:0;
clk.tic();
MPI_Isend(sendbuf, bufsize, MPI_DOUBLE, other,
    tag, MPI_COMM_WORLD, &req1);
MPI_Irecv(recvbuf, bufsize, MPI_DOUBLE, other,
    tag, MPI_COMM_WORLD, &req2);
MPI_Wait(&req1, MPI_STATUS_IGNORE);
MPI_Wait(&req2, MPI_STATUS_IGNORE);
cycles = clk.toc();
return cycles;
```

The nonblocking MPI_Isend() occurs on lines 11 and 12. Its first arguments are as before: buffer, size or number of items in the buffer, type of each item, destination, tag, and communicator. request object. The nonblocking MPI_Irecv() occurs on lines 13 and 14. Its fourth argument is other, which is the source of the message received. The seventh and last argument is a pointer to a request object as before.

This function uses MPI_Wait() on lines 15 and 16 to wait for the completion of the nonblocking send and receive. A program could do some useful computation after posting a nonblocking send or receive before waiting for its completion. This function does not return the number of cycles used during the exchange.

How this uses the Infiniband network depends on the send and receive buffers on line 2 and recvbuf are allocated. If the buffers are allocated using MPI_Alloc_mem(), this function is no different from persistent exchange. It will map to RDMA read and write in exactly the same way. There is not much to choose between persistent and nonblocking communication in that case.

We will assume that both sendbuf and recvbuf are allocated using new[] or