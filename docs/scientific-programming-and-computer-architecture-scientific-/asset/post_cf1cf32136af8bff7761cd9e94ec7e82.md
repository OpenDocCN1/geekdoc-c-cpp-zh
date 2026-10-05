
## 6.1. MPI: Getting started

```c
MPI_Comm_size(MPI_COMM_WORLD, &nprocs);
}
```

Using mpi_initialize() saves us trouble of remembering the syntax of three MPI library functions. Before making any calls to the MPI library, a program may execute the following code fragment:

```c
int rank;
int nprocs;
mpi_initialize(rank, nprocs);
```

After this fragment, each process knows its rank and the total number of processes. Before exiting, each process must call MPI_Finalize(). Each MPI process uses rank to identify the process to which it sends a message or from which it receives a message.

Our first example of sending and receiving messages is the function unsafe() listed below.

```c
void unsafe(int numOfDoubles, int rank, int nprocs,
    double *sendbuf, double *recvbuf)
{
    int tag, status;
    MPI_Barrier(MPI_COMM_WORLD);
    if(rank==0) {
        MPI_Send(sendbuf, numOfDoubles, MPI_DOUBLE,
            nprocs-1, tag, MPI_COMM_WORLD);
        MPI_Recv(recvbuf, numOfDoubles, MPI_DOUBLE,
            nprocs-1, tag, MPI_COMM_WORLD,
            &status);
    } else if(rank==nprocs-1) {
        MPI_Send(sendbuf, numOfDoubles, MPI_DOUBLE,
            0, tag, MPI_COMM_WORLD);
        MPI_Recv(recvbuf, numOfDoubles, MPI_DOUBLE,
            0, tag, MPI_COMM_WORLD, &status);
    }
}
```

We will assume that the MPI program is started up with exactly two processes and that each process calls unsafe(). The two processes send a certain number of doubles to each other. The number of doubles transmitted is given by the first argument. It is assumed that rank and nprocs have been appropriately initialized by both processes after MPI_initialize(). These are passed to unsafe() as arguments on line 1. The buffers for sending and receiving appear as sendbuf and recvbuf on line 2. These buffers are allocated by each process before the call to unsafe().

The MPI syntax that appears in unsafe(), supplemented by variants of send and receive described in a later section, is nearly all the MPI syntax we need. Line 5 defines status to be type MPI_Status. The MPI_Recv() function returns information on status on lines 12 and 18. Other MPI variants for message passing and probing return status information.

The MPI_Barrier() on line 6 stalls until all processes have entered the barrier. Its argument is a communicator, and the only MPI communicator we use, MPI_COMM_WORLD, includes all processes. The barrier plays no essential role in the function unsafe(). MPI processes get in sync while sending and receiving messages. The situation is different from shared memory where threads might conflict while reading and writing from the same location. Processes that communicate or coordinate using shared memory must spin locks, mutexes, critical regions, or barriers. Barriers are useful in MPI, but they are less frequently used. There is a degree of synchronization inherent in message passing.

The if-block of statements from lines 8 through 12 is executed only by the process with rank 0. The else-if block of statements from lines 15 through 18 is executed by the process with rank nprocs-1. Because we are assuming exactly two processes, the else-if is executed by the process with rank 1. This manner of using rank to distinguish between processes is typical of MPI in the same way that use of thread identifiers is typical of OpenMP.

The crucial bits of syntax in unsafe() are MPI_Send() and MPI_Recv(). On lines 8 and 9, the process with rank 0 sends a message to rank 1. The first argument to MPI_Send() is a pointer to the buffer. This argument is declared to be of type void *. On line 8, the argument is of type double *, which is automatically cast to the right type. Any pointer may be cast to void *. The second argument is the number of items in the buffer, and the third argument is the data type of each item. The data type is given as MPI_DOUBLE. MPI has elaborate constructions for data types. MPI data types are difficult to comprehend in full generality, and it is difficult to imagine how they could be useful. Most programs can get by with MPI_CHAR, MPI_DOUBLE. By giving the data type as MPI_DOUBLE, we are indicating that each item is a double and is 8 bytes wide as in C/C++.

On line 9, the fourth argument to MPI_Send() is given as nprocs-1. This argument is the destination of the message and is indicated here to be the process with rank nprocs-1 or 1. The fifth argument is the tag. The tags must agree when receives are matched with sends. The last argument must be a communicator.

MPI_Recv() has seven arguments, one than MPI_Send(). The first three arguments on line 11 are the receiver buffer, the number of items to be received, and the data type of each item. The fourth argument, which is given on line 12, is the source of the message—the source specifies the destination and the receiver specifies the source. The source is specified to be nprocs-1 or the process with rank 1. The fifth argument is the tag and the sixth argument must be a communicator.

The MPI receive must match the corresponding MPI send. In the case of unsafe(), the send on line 8 matches the receive on 17. The send on line 15 matches the receive on 10.
