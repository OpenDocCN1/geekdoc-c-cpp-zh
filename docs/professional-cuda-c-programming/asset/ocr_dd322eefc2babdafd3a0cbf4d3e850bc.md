MPI, only the contents of host memory must be copied back to host memory using the CUDA API before MPI can be used to communicate that data to another node. With CUDA-aware MPI, you can pass GPU memory to MPI functions without staging that data through host memory.

Several commercial and open-source CUDA-aware MPI implementations are available, as:

+   - MVAPICH2 2.0rc2 (http://mvapich.cse.ohio-state.edu/download/mvapich2/)
 MVAPICH2-GDR 2.0b (http://mvapich.cse.ohio-state.edu/download/mvapich2gdr/)
 OpenMPI 1.7 (http://www.open-mpi.org/software/ompi/v1.7/)
 CRAY MPI (MPT 5.6.2)
 IBM MPI Flat (8.3)

MVAPICH2 is an open source MPI implementation designed to exploit Infiniband network features to deliver high performance and scalability for MPI-based applications. Two versions exist: MVAPICH2 is a CUDA-aware MPI implementation, while MVAPICH2-GDR is an extension that also supports GPUDirect RDMA over Infiniband (more on GPUDirect later in this chapter).

MVAPICH2 is a widely used open-source MPI library for Infiniband clusters and supports MPI communication directly from one GPU's device memory to another's. The next sections will test the following cases using the MVAPICH2 platform:

+   - CPU to CPU data transfer over Infiniband with MVAPICH2
 GPU to GPU data transfer over Infiniband with traditional MPI
 GPU to GPU data transfer over Infiniband with CUDA-aware MPI
 GPU to GPU data transfer over Infiniband with MVAPICH2-GDR and GPUDirect RDMA

# CPU-to-CPU Data Transfer

To establish a baseline for comparison, you can test the bandwidth and latency of data transfers over the interconnect between two CPU nodes in a cluster using MVAPICH2. Generally, MPI programs consist of four steps:

+   1. Initialize the MPI environment.
2. Pass messages between processes in different nodes using blocking or non-blocking MPI functions.
3. Synchronize across nodes.
4. Clean up the MPI environment.