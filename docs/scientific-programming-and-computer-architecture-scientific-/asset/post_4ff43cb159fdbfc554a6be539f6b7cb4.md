
## 6.2. High-performance network architecture

conversion of data in program memory to Infiniband data packets is pipelined over the host channel adapter.

### MPI protocol for short messages

MPI libraries use RDMA to transmit large messages over Infiniband networks. The responder must send its remote requester before an RDMA operation is initiated. There are other overheads that arise when MPI library calls are mapped to Infiniband Verbs. Latency measurements do not include these overheads. For large messages, the overheads are a small fraction of the transmission time and therefore not significant. However, the overhead of setting up RDMA transfers can prove to be too great for small messages.

The alternative is to use channel semantics. When two processes use the sender posts a send request to the sender queue of a queue pair, and the receiver receives a request to the receiver of another queue pair that is bound to the sender's queue pair. When the send message arrives at the receiver, it has no information about the region of memory to which its payload must be copied. The sent must be matched with receive to complete the data transfer. Having to match sends with receives implies that the MPI library has to implement flow control to the extent it uses channel semantics. The need for flow control, which brings with it the need to retry and resend messages, makes channel semantics unattractive.

For long messages, the overhead of arranging a rendezvous between the sender and receiver before initiating an RDMA transfer is not significant. For short messages, this overhead can be avoided if there are preassigned buffers to which the messages are copied. Open MPI and other MPI implementations do that. They use preassigned buffers and RDMA transfer for short messages. The buffers at the sender and the receiver are matched in advance. The sender will copy its message to a send buffer as soon as a function call is issued in the MPI library. The buffer is transmitted using RDMA write. The receiver polls the corresponding buffer on the receiver side to check whether the receive is complete. A special flag is written into the receive buffer to indicate that the data transfer is complete.

> 8 The transmission of short messages using preassigned buffers and RDMA is described by Liu et al. (2004).

## Chapter 6. Special Topic: Networks and Message Passing

Using preassigned buffers and RDMA transfers means that short messages must be copied to and from buffers. MPI implementations may use a combination of RDMA with preassigned buffers and channel semantics for short messages.

In this chapter, we attempt to tie discussion of the MPI library to Infiniband architecture as far as possible. An advantage is that some phenomena otherwise look arbitrary will begin to look more reasonable. Knowledge of how the network actually works will us make better use of the MPI library. An example is the connection of the short message protocol to the behavior of `unsafe()` defined in 6.1.2. The function `unsafe()` deadlocks if the message is longer than 12 KB but not for shorter messages. What is special about messages smaller than 12 KB? The command `mpi_info` reveals that default Open MPI treats messages as short if they are shorter than 12 KB. For short messages, MPI_Send() copies the message to a local buffer and returns immediately. The buffer will be transmitted with RDMA.

For longer messages, the MPI library registers the buffer in `MPI_Send()` and sends the remote key to the destination. The destination is expected to initiate after the RDMA read when it comes after a matching `MPI_Recv()`. The `MPI_Send()` returns after the RDMA operation is complete. For longer messages, the processes of rank 0 and 1 execute each `MPI_Send()` in `unsafe()` and wait for a RDMA read operation. They deadlock in that state because neither of them gets to execute the matching `MPI_Recv()` and initiate an RDMA read operation.

**Exercise 6.2.1.** Consider a binary tree with $2^n$ leaves at level $n$. Assume that messages pass each pair of leaves in either direction with equal probability. Calculate the expected number of messages passing between level $k$ and level $k+1$ for $k=0, \dots, n-1$. The number of edges between levels $k$ and $k+1$ is $2^{k+1}$. By what factor does the number of messages per edge vary?

**Exercise 6.2.2.** Figure 6.1 shows how a fat-tree with 8 leaves might be laid out on a plane surface. Describe the layout for fat-trees with 16, 32, and 64 leaves.

**Exercise 6.2.3.** In the Infiniband architecture, what is the maximum number of bytes that can be broken up into a single train of packets?

**Exercise 6.2.4.** Find out the format of TCP/IP packets as well as Ethernet frames. Are the Infiniband packets more similar to TCP/IP packets or Ethernet frames?

**Exercise 6.2.5.** Is it possible to create protection domains without kernel intervention? Is it possible to set up page tables without kernel intervention?

## 6.3. MPI examples

**Exercise 6.2.6.** To initiate an RDMA write, the initiating node or the requester needs to know the remote address into which the data should be written. Should this address be a virtual address or a physical address or can it be either?

**Exercise 6.2.7.** When an RDMA read or write function call is made, the requester needs to know the memory location at the responder that will be involved in the data transfer. Therefore, there must be a prior exchange of information between the requester and the responder before the RDMA transaction is initiated. This prior exchange involves an overhead. Explain why RDMA reads and writes are efficient despite this overhead.

In this section, we get more deeply into syntax. Our systems/architecture brings out other aspects of sending and receiving. In this chapter, we attempt to tie discussion of the MPI library to Infiniband architecture as far as possible. An advantage is that some phenomena otherwise look arbitrary will begin to look more reasonable. Knowledge of how the network actually works will us make better use of the MPI library.

In this section, we get more deeply into syntax. However, RDMA transactions are one sided. On Infiniband clusters, all sends and receives map to RDMA transactions. In matrix transposition, the data format at the receiver differs from the data format at the sender. The change in data format implies a need for buffers and copying into and out of buffers. The challenge in matrix transposition is to hide the cost of copying into and out of buffers by overlapping with network activity.
