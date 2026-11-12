may also prefetch pageable memory to the GPU by using cudaMemPrefetchAsync. This could yield performance benefits through optimized data locality.

ATS over NVLink is currently supported only on IBM Power9 systems.

# K.1.7. Hardware Coherency

The second generation of NVLink allows direct load/store/atomic access from the CPU to each GPU's memory. Coupled with a new CPU mastering capability, NVLink supports coherency operations allowing data reads from GPU memory to be stored in the CPU's cache hierarchy. The lower latency of access from the CPU's cache is key for CPU performance. Devices of compute capability 6.x support only peer GPU atomics. Devices of compute capability 7.x can send GPU atomics across NVLink and have them completed at the target CPU, thus the second generation of NVLink adds support for atomics initiated by either the GPU or the CPU.

Note that cudaMalloc allocations are not accessible from the CPU. Therefore, to take advantage of hardware coherency users must use Unified Memory allocators such as cudaMallocManaged or system allocator with ATS support (see System Allocator). The new property directManagedMemAccessFromHost indicates if the host can directly access managed memory on the device without migration. By default, any CPU access of cudaMallocManaged allocations resident in GPU memory will trigger page faults and data migration. Applications can use cudaMemAdviseSetAccessedBy memory access hint with cudaCpuDeviceId to enable direct access of GPU memory on supported systems.

Consider an example code below:

```
__global__ void write(int *ret, int a, int b) {
    ret[ThreadIdx.x] = a + b + threadIdx.x;
}
__global__ void append(int *ret, int a, int b) {
    ret[ThreadIdx.x] += a + b + threadIdx.x;
}
int main() {
    int *ret;
    cudaMallocManaged(&ret, 1000 * sizeof(int));
    cudaMemAdvise(ret, 1000 * sizeof(int), cudaMemAdviseSetAccessedBy,
    cudaCpuDeviceId); // set direct access hint
    write<<< 1, 1000 >>>(ret, 10, 100); // pages populated in GPU
    memory
    cudaDeviceSynchronize();
    for(int i = 0; i < 1000; i++)
    printf("%d: A=%d =%dn", i, ret[i]); //
directManagedMemAccessFromHost=1: CPU accesses GPU memory directly without
migrations
    //
directManagedMemAccessFromHost=0: CPU faults and triggers device-to-host
migrations
    append<<< 1, 1000 >>>(ret, 10, 100); //
directManagedMemAccessFromHost=1: GPU accesses GPU memory without migrations
    cudaDeviceSynchronize(); //
directManagedMemAccessFromHost=0: GPU faults and triggers host-to-device
migrations
    cudaFree(ret);
    return 0;
}
```