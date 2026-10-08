
```cpp
cudaGetDeviceCount(&n_devices);
int device = local_rank % n_devices;
cudaSetDevice(device);

MPI_Init(argc, argv);
```

However, if you used MV2_ENABLE_AFFINITY to set the CPU affinity of an MPI process, and then used MV2_COMM_WORLD_RANK to set the GPU affinity, you have no guarantee that the CPU an MPI process is running on is optimally co-located with the assigned GPU. If they are not optimally co-located, the latency and bandwidth between the host application and device memory may be degraded. Instead, you can use the Portable Hardware Locality package (hwloc) to analyze the hardware topology of a node and pin MPI process to a CPU that is optimally co-located with the GPU assigned to that MPI process.

The following example uses the MPI rank of a process to select a GPU. Then, hwloc is used to determine the best CPU core to pin to, given that GPU.

```c
rank = atoi(getenv("MV2_COMM_WORLD_RANK"));
local_rank = atoi(getenv("MV2_COMM_LOCAL_RANK"));

// Load a full hardware topology of all PCI devices in this node.
hwloc_init(&topology);
hwloc_topology_set_flags(topology, HWLOC_TOPOLOGY_FLAG_WHO_IO);
hwloc_topology_destroy(topology);

// choose a GPU based on MPI rank
cudaSetDevice(local_rank);
cudaGetDevice(&device);

// Iterate through all CPU cores that are physically close to the assigned GPU.
// This code entity de-izes processes across cores using local_rank.
ccpuset = hwloc_bitmap_alloc();
hwloc_bitmap_set_cpuset(topology, device, cpuset);
match = 0;
hwloc_bitmap_foreach_begin(i,cpuset)
  if (match == local_rank) {
    cpu = i;
    break;
  }
  ++match;
hwloc_bitmap_foreach_end();

// Bind this process to the selected CPU.
onecpu = hwloc_bitmap_alloc();
hwloc_bitmap_set(onecpu, cpu);
hwloc_set_cpind(topology, onecpu, 0);

// Cleanup.
hwloc_bitmap_free(onecpu);
hwloc_bitmap_free(cpuset);
hwloc_topology_destroy(topology);

gethostname(hostname, sizeof(hostname));
cpu = sched_getcpu();
printf("*MPI rank %d using GPU %d and CPU %d on host %s\n",
rank, device, cpu, hostname);
```

```cpp
    MPI_Init(&argc, &argv);
MPI_Comm_rank(MPI_COMM_WORLD, &rank);
if (MPI_SUCCESS != MPI_Get_processor_name(procname, &length)) {
    strncpy(procname, "unknown");
}
```

# GPU-to-GPU Communication With MPI

Once a process has pinned itself to a GPU with cudaDevice, device memory and host pinned memory can be allocated for the current device:

```c
    char *h_src, *h_rcv; MYBUFSIZE;
cudaMallocHost((void**)&h_src, MYBUFSIZE);
cudaMallocHost((void**)&h_rcv, MYBUFSIZE);

    char *d_src, *d_rcv;
cudaMalloc((void**)&d_src, MYBUFSIZE);
cudaMalloc((void**)&d_rcv, MYBUFSIZE);
```

Bidirectional data transfer between GPUs using traditional MPI is performed in two steps: First, data is copied from device memory to host memory. Then, data in memory is exchanged between processes using MPI communication library:

```c
if (rank == 0) {
    for (int i = 0; i < loop; i++) {
        cudaMemcpy(h_src, d_src, size, cudaMemcpyDeviceToHost);

        // bi-directional bandwidth
        MPI_Recv(h_rcv, size, MPI_CHAR, other_proc, 10, MPI_COMM_WORLD, &recv_request);
        MPI_Isend(h_src, size, MPI_CHAR, other_proc, 10, MPI_COMM_WORLD, &send_request);
        MPI_Waitall(1, &recv_request, &reqstat);
        MPI_Waitall(1, &send_request, &reqstat);
    }
    cudaMemcpy(d_src, h_rcv, size, cudaMemcpyHostToDevice);
} else {
    for (int i = 0; i < loop; i++) {
        cudaMemcpy(h_src, d_src, size, cudaMemcpyDeviceToHost);

        // bi-directional bandwidth
        MPI_Recv(h_rcv, size, MPI_CHAR, other_proc, 10, MPI_COMM_WORLD, &recv_request);
        MPI_Isend(h_src, size, MPI_CHAR, other_proc, 10, MPI_COMM_WORLD, &send_request);
        MPI_Waitall(1, &recv_request, &reqstat);
        MPI_Waitall(1, &send_request, &reqstat);
    }
    cudaMemcpy(d_src, h_rcv, size, cudaMemcpyHostToDevice);
}
```

You can download the file simpleP2P containing the full code for this example from Wrox.com.
Compile it with the following command:

```bash
$ mpicc -std=c99 -03 simpleP2P.c -o simplep2p
```

Launch the MPI program with mpirun_rsh, as follows:

```bash
$ mpirun_rsh -np 2 node01 node02 ./simplep2p
```

An example report of a system with two Fermi M2090 GPUs is shown. Note the sharp decrease in bandwidth and increase in latency compared to the CPU-to-CPU example. This performance loss is caused by the added overhead of transferring data from the GPU before transmitting it using MPI.

```text
./simplep2p to allocate 4 MB memory and probe host memory CUDA + MPI
node=0(node01): using GPU=1 and other_proc=1
node=1(node02): using GPU=0 and other_proc=0
```

| size | Elapsed | Performance |
| :--- | :--- | :--- |
| 1 KB | 10.24 us | 99.5 MB/sec |
| 4 KB | 11.51 us | 355.8 MB/sec |
| 16 KB | 19.77 us | 828.7 MB/sec |
| 64 KB | 46.34 us | 1414.2 MB/sec |
| 256 KB | 183.31 us | 2237.3 MB/sec |
| 1 MB | 394.07 us | 2669.0 MB/sec |
| 4 MB | 1532.47 us | 2736.9 MB/sec |

# GPU-to-Data Transfer with CUDA-aware MPI

MVAPICH is also a CUDA-aware MPI implementation, which supports GPU to GPU communication through the standard MPI API. You can pass device pointers directly to MPI functions (and avoid the extra cudaMem calls required for traditional MPI):

```c
if (rank == 0) {
    for (int i = 0; i < loop; i++) {
        MPI_Irecv(d_recv, size, MPI_CHAR, other_proc, 100, MPI_COMM_WORLD, &recv_request);
        MPI_Isend(d_src, size, MPI_CHAR, other_proc, 100, MPI_COMM_WORLD, &send_request);
        MPI_Waitall(1, &recv_request, &reqstat);
        MPI_Waitall(1, &send_request, &reqstat);
    }
} else {
    for (int i = 0; i < loop; i++) {
        MPI_Irecv(d_recv, size, MPI_CHAR, other_proc, 100, MPI_COMM_WORLD, &recv_request);
        MPI_Isend(d_src, size, MPI_CHAR, other_proc, 100, MPI_COMM_WORLD, &send_request);
        MPI_Waitall(1, &recv_request, &reqstat);
        MPI_Waitall(1, &send_request, &reqstat);
    }
}
```

You can download the file simpleP2P containing the full code for this example from Wrox.com.
Compile it with the following command:

```bash
$ mpicc -std=c99 -03 simpleP2P.c -o simplep2p
```

Launch the MPI program with mpirun_rsh, as follows:

```bash
$ mpirun_rsh -np 2 node01 node02 ./simplep2p
```

An example report of a system with two Fermi M2090 GPUs is shown. Note the sharp decrease in bandwidth and increase in latency compared to the CPU-to-CPU example. This performance loss is caused by the added overhead of transferring data from the GPU before transmitting it using MPI.

```text
./simplep2p to allocate 4 MB memory and probe host memory CUDA + MPI
node=0(node01): using GPU=1 and other_proc=1
node=1(node02): using GPU=0 and other_proc=0
```

| size | Elapsed | Performance |
| :--- | :--- | :--- |
| 1 KB | 10.24 us | 99.5 MB/sec |
| 4 KB | 11.51 us | 355.8 MB/sec |
| 16 KB | 19.77 us | 828.7 MB/sec |
| 64 KB | 46.34 us | 1414.2 MB/sec |
| 256 KB | 183.31 us | 2237.3 MB/sec |
| 1 MB | 394.07 us | 2669.0 MB/sec |
| 4 MB | 1532.47 us | 2736.9 MB/sec |
