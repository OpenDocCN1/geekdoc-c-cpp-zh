
```c
hStreams_app_xfer_memory(h_Ablock[countA], h_Ablock[countA], // <---- hStreams
mem_size_Ablock,(int)countA%max_log_str, HSTR_SRC_TO_SINK, &eventAcpy[countA]);
}
else if((countB<countA || countA==totalblocks_A-1) && (countB<totalblocks_B-1)){
    countB++;
    hStreams_app_xfer_memory(h_Bblock[countB], h_Bblock[countB], //<----- hStreams
    mem_size_Bblock,(int)countB%max_log_str, HSTR_SRC_TO_SINK, &eventBcpy[countB]);
}
// start multiplications
if((countA + countB) >= 0){
    if(countA > countB){ // received a new A block: issue a DGEMM call on the card
        for(int j = 0; j <= countB; j++){
            divresult1 = div(countA, mblocks);
            divresult2 = div(j, nblocks);
            if (divresult1.quot == divresult2.quot){ //validity checking
                cblock_index = divresult1.rem*nblocks + divresult2.rem;
                hStreams_app_event_wait(1, &eventBcpy[j]); // <--------- hStreams
                hStreams_app_event_wait(1, &eventAcpy[countA]); // <--------- hStreams
                hStreams_app_event_wait(1, &eventCset[cblock_index]); // <--- hStreams
                // Async compute using MKL DGEMM on the device
                qindex = (int)cblock_index % max_log_str;
                hStreams_app_dgemm(CblasColMajor, CblasNoTrans, CblasNoTrans, //<-- hStreams
                    numColsB/nblocks, numRowsA/mblocks, numRowsB/kblocks,
                    alpha, h_Bblock[j], numColsB/nblocks, h_Ablock[countA], numColsA/kblocks,
                    beta, h_Cblock[cblock_index], numColsC/nblocks,
                    qindex, &eventCcpy[cblock_index]);
            }
        }
    } else { // received a new B block: issue a DGEMM call
        for(int j = 0; j <= countA; j++){
            divresult1 = div(j, mblocks);
            divresult2 = div(countB, nblocks);
            if (divresult1.quot == divresult2.quot){ // validity checking
                cblock_index = divresult1.rem*nblocks + divresult2.rem;
                hStreams_app_event_wait(1, &eventBcpy[countB]); // <--------- hStreams
                hStreams_app_event_wait(1, &eventAcpy[j]); // <--------- hStreams
                hStreams_app_event_wait(1, &eventCset[cblock_index]); // <--- hStreams
                // Async compute using MKL DGEMM on the device
                qindex = (int)cblock_index % max_log_str;
                hStreams_app_dgemm(CblasColMajor, CblasNoTrans, CblasNoTrans, //<-- hStreams
                    numColsB/nblocks, numRowsA/mblocks, numRowsB/kblocks,
                    alpha, h_Bblock[countB], numColsB/nblocks, h_Ablock[j], numColsA/kblocks,
                    beta, h_Cblock[cblock_index], numColsC/nblocks,
                    qindex, &eventCcpy[cblock_index]);
            }
        }
    }
}
// copy result from device back to host
for (int i = 0; i < totalblocks_C; i++){
    // Synchronize before transferring the result back
    hStreams_app_stream_sync(i%max_log_str); //<---- hStreams
    hStreams_app_xfer_memory(h_Cblock[i], h_Cblock[i], mem_size_Cblock, //<---- hStreams
        (int)i%max_log_str, HSTR_SINK_TO_SRC, &eventCcpy[i]);
}
// assemble fullsize C matrix from the blocks for comparison purposes
```

## MPI-3 Shared Memory Programming Introduction

### Motivation

The Message Passing Interface (MPI) is one of the most popular parallel programming models for distributed memory systems. As the number of cores per node has increased, programmers have increasingly combined MPI with shared memory parallel programming interfaces, such as the OpenMP programming model. This hybrid of distributed-memory and shared-memory parallel programming idioms has aided programmers in addressing the concerns of performing efficient internode communication while effectively utilizing advancements in node-level architectures, including multicore and many-core processor architectures, such as Intel® Xeon® processors and Intel® Xeon Phi™ coprocessors.

Version 3.0 of the MPI standard adds a new MPI interprocess shared memory extension (MPI SHM). This new extension is now supported by many MPI distributions, including versions 5.0.2 and beyond of the Intel® MPI Library. The MPI SHM extension enables programmers to create regions of shared memory that are directly accessible by MPI processes within the same shared memory domain. In contrast with hybrid approaches, MPI SHM offers an incremental approach to managing memory resources within a node, where data structures can be individually moved into shared segments to reduce the memory footprint and improve the communication efficiency of MPI programs.

We present application developers with an introduction to MPI SHM and a tutorial on how to start using MPI SHM on systems with Intel Xeon processors with Intel Xeon Phi coprocessors. We discuss the two central optimization challenges that are addressed by MPI SHM: communication efficiency and memory capacity pressure. We further demonstrate the potential for performance improvement from these new capabilities through a halo exchange example taken from the MPPTEST test suite, which we have extended to include MPI SHM. Halo exchange is a prototypical neighborhood exchange communication pattern. In such patterns, the adjacency of communication partners often results in communication with processes in the same node, making them good candidates for acceleration through MPI SHM. By applying MPI SHM to this common communication pattern, we demonstrate that direct data sharing can be used instead of communication, resulting in significant performance gains.

### MPI's Interprocess Shared Memory Extension

MPI SHM was added in version 3.0 of the MPI specification as an extension to the remote memory access (RMA) interface. The MPI RMA interface was added in version 2.0 of the MPI specification. The MPI RMA API provides a set of operations that can be used to remotely access data located in the memory of different MPI processes, using one-sided communication between MPI processes. In contrast with conventional two-sided communication, where both processes participate through matched send and receive operations, one-sided communications are performed by the initiator without a corresponding operation at the target. For this reason, MPI refers to the process that initiates a one-sided communication operation as the origin process and the process that contains the memory being accessed as the target process.

In the MPI RMA model, processes open windows into their address space through a setup operation that results in a window object. Window object creation is performed collectively—i.e., by all processes—on an existing parent MPI communicator, such as MPI_COMM_WORLD. A handle to the resulting window object is returned in all participating processes; this handle can then be used in subsequent communication operations to access the windows of all other processes that are participants in the window object.

While memory in a process is private by default, opening a window allows other processes to access data contained within the window memory directly using one-sided put and get copy operations, as well as atomic update operations, including compare-and-swap, accumulate, and get-accumulate. MPI also defines several synchronization methods that are used to coordinate remote accesses, ensure data consistency, and provide ordering among remote access operations.

MPI SHM extends the MPI RMA interface with a set of new operations that can be used to:

- identify which processes are located within the same shared memory domain,
- allocate interprocess shared memory, and
- coordinate accesses to the shared memory allocation.

In contrast to conventional MPI windows, shared memory windows can be queried for a direct pointer to the window memory, and window memory can be directly accessed using the pointer. In the coming sections, we discuss the MPI SHM interface in detail and demonstrate its usage. While our discussion focuses on MPI's interprocess shared memory extension, the same concepts and techniques can be applied in the context of interprocess shared memory mechanisms provided by other communication libraries, such as OpenSHMEM.

### When to Use MPI Interprocess Shared Memory

MPI's interprocess shared memory extension addresses two key challenges faced by programmers of modern HPC systems: communication efficiency and memory capacity pressure. As the number of cores per node continues to grow, there is potential for more data exchange to occur within the node, which can be performed more efficiently through direct shared memory accesses, rather than conventional message passing. At the same time, memory is a resource that is shared by the cores in a node. In conventional MPI programs, the memory of each process is private and when every MPI process needs the same data, it is replicated. As a result, the same data may be stored multiple times in a node's memory.
