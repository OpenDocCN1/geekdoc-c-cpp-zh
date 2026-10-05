
## 6.3. MPI examples

malloc(). Even with this assumption, it is preferable to use RDMA for large messages. But new[] and malloc() do not register memory, and difficulties arise when registering memory.

If the data in the send buffer of one process is transferred to the receive buffer of another process using RDMA, both the buffers must be registered. Registering the memory has the following effect: The host channel adapter will note the map from virtual to physical memory, as already mentioned. But another element we have not mentioned so far becomes quite important here. This other element in registering memory is that physical memory page frames must be pinned. Otherwise the pages may be assigned to different pages by the operating system kernel when the host channel adapter is moving data from DRAM and the network.

Although pinned memory⁹ is essential for RDMA to avoid the wasteful buffers, which is problematic for an Infiniband Verb to pin memory outside MPI's control using new[] or malloc(). We will discuss three ways this problem can be tackled.

The safe method for MPI to register memory using an Infiniband Verb when the send/receive transaction is initiated and deregister the memory after the transaction is completed. The safe method is never used. It is too expensive and defeats the purpose of the Infiniband architecture. Pinning and unpinning memory require calling the operating system kernel. These calls are exposed to much of the complexity of the kernel's memory management system and are expensive. The Infiniband architecture sets up host channel adapters, protection domains, and queue pairs so that messages can be sent directly from processes to the host channel adapter bypassing the kernel. Thus, to register and deregister memory at each transaction would defeat one of the principal goals of Infiniband design, which is to bypass the kernel during send and receive. Another safe method is for the MPI library to use internal buffers that are registered and pinned in advance. This safe method is also expensive and defeats the other principal goal of Infiniband design—avoiding wasteful buffering and buffer copies.

The second method is fast but not perfectly safe. It is the method used by default by most MPI implementations. In this method, buffers are registered before communication, if they are not already registered. But the buffers are not deregistered once the communication ends. The expectation is that the same buffers will be repeatedly for communication. Later communication incurs no overhead because of registering and deregistering memory. The deregistration may be performed during MPI_Finalize().

This method is unsafe for the following reason. The user process may deallocate memory without knowledge of the MPI library. If it does, the virtual memory inside the host adapter becomes invalid. The user process may later claim some more memory that is mapped to the same addresses as the deallocated memory to different page frames in DRAM. Dangerous memory errors will follow. Techniques such as replacing malloc() and free() with MPI versions at link time can render this method safe. It is unclear how completely these are implemented within MPI libraries and how effective the implementations are in preventing memory

Table 6.2 shows that the combination of memory allocation using C/C++ libraries and nonblocking communication leads only to a small in bandwidth if the second method is used. This method corresponds to the column marked “pinned” in the table.

While the second method is the default method, Open MPI implements a third method. This third method is turned on by setting the Open MPI parameter

```
mpi_leave_pinned
```
to zero. This third method is called pipelined RDMA. Table 6.2 shows that the third method leads to a loss of bandwidth but is still quite fast.

In pipelined RDMA, the long message is broken up into pieces. Some of the pieces are sent using channel semantics. When these pieces are in transit, the MPI library registers some of the other pieces, and it deregisters them as the transfer completes. Pipelined RDMA overlaps registration and deregistration of memory with communication over the network so that the bandwidth is not severely compromised. It is perfectly safe.

Pipelined RDMA uses RDMA write, not RDMA read. The activity of breaking the message into pieces and overlapping memory registration with network activity is best performed at the sender’s end. Although RDMA is one sided, RDMA read, it provides a facility to pack immediate data into the last packet. This immediate data causes the host channel adapter to recognize completion of the RDMA write and inform the responder or receiver. The information is passed up to the Verb layer by placing a completion element on the completion queue.

Of course, the pros and cons of the various methods for implementing noncommunication are rendered moot if the user process allocates buffers using MPI_Alloc_mem(). With such memory allocation, communication is safe but not necessarily fast.

It might seem that it is always better to allocate and receive buffers with MPI_Alloc_mem(). The MPI library can be relieved of the hassle of registering and deregistering memory. There are important situations where the programmer is better off using new or malloc(). One such situation occurs when we discuss the matrix transpose in this chapter. In Open MPI, MPI_Alloc_mem() assigns frames to the allocated virtual memory pages immediately. The page frames will not be allocated in memory that is nearest to the processor that accesses it for in multithreaded programs, the use of MPI_Alloc_mem() may imply additional overhead in copying to send buffers and copying out of receive buffers. This is the speed of the Infiniband network that this additional overhead in filling and emptying buffers can be significant, as we find in a later section on the matrix transpose.

## Blocking exchange

The syntax of the blocking calls MPI_Send() and MPI_Recv() were discussed in section 6.1.2, and there is not much to add. The function defined below reverses the order of send and receive on the process of rank 1 (nprocs-1) to avoid deadlock.

```
double exchange_blocking(int rank, int nprocs,
double* sendbuf, double* recvbuf,int bufsize){
TimeStamp clk;
int tag = 0;
double cycles=0;
if(rank==0) {
clk.tic();
MPI_Send(sendbuf, bufsize, MPI_DOUBLE,
nprocs-1, tag, MPI_COMM_WORLD);
MPI_Recv(recbuf, bufsize, MPI_DOUBLE,
nprocs-1, tag, MPI_COMM_WORLD,
MPI_STATUS_IGNORE);
cycles = clk.toc();
}
else if (rank==nprocs-1){
MPI_Recv(recbuf, bufsize, MPI_DOUBLE,
0, tag, MPI_COMM_WORLD, MPI_STATUS_IGNORE);
MPI_Send(sendbuf, bufsize, MPI_DOUBLE,
0, tag,MPI_COMM_WORLD);
}
return cycles;
```

Table 6.2 shows that blocking communication nearly halves the network bandwidth. The Infiniband network is bidirectional, but blocking communication forces unidirectional communication. Blocking communication should not be used on modern networks such as Infiniband. It is too inefficient and has a tendency to cause deadlocks.

## Cyclic exchange

Using data exchange to learn MPI syntax, as we did, has a few advantages. Although the setting with only two processes communicating is quite limited, the syntax carries over with few changes to the setting where many processes are communicating with each other. Here we will look at cyclic data exchange.

Figure 6.7 illustrates cyclic exchange of data. The processes are arranged on a cycle, and each process communicates with the neighbor to its left as well as the neighbor to its right. The communication between pairs of neighboring processes is much like the data exchange we have studied in detail. Consequently, no new points of MPI syntax arise. Therefore, we give the interface to the Cycle class omit its definition from the text.

The main purpose is to examine network bandwidth as the number of communicating agents increases. Network bandwidth depends on the pattern of communication between host computers. Two hosts exchanging data is one of the simplest patterns.

> ⁹The limit on pinned memory can be On the author's desktop it is just 64 KB. However, on many high-performance clusters, this limit is set to infinity to enable RDMA communication. The limit may be found using the GNU/Linux command ulimit -a.

> ¹⁰For pipelined RDMA, see Woodall et al. (2006).
