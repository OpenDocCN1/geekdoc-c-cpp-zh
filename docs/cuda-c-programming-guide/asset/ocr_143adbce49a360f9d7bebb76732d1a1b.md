+   2. If applications have warp-synchronous codes, they will need to insert the new `__syncwarp()` warp-wide barrier synchronization instruction between any steps where data is exchanged between threads via global or shared memory. Assumptions that code is executed in lockstep or that reads/writes from separate threads are visible across a warp without synchronization are invalid.

```
float s_buf[tid] = val;
__syncthreads();

// Inter-warp reduction
for (int i=BID/2; i>0; i/=2) {
    s_buf[tid] += s_buf[tid+i];
    __syncthreads();
}

// Intra-warp reduction
// Butterfly reduction simplifies syncwarp mask
if (tid < 32) {
    float temp;
    s_buf[tid] += temp; __syncwarp();
    s_buf[tid] += temp; __syncwarp();
    temp = s_buf[tid^8]; __syncwarp();
    s_buf[tid] += temp; __syncwarp();
    temp = s_buf[tid^4]; __syncwarp();
    s_buf[tid] += temp; __syncwarp();
    temp = s_buf[tid^2]; __syncwarp();
    s_buf[tid] += temp; __syncwarp();
}

if (tid == 0) {
    *output = s_buf[0] + s_buf[1];
}
__syncthreads();
```

+   3. Although `__syncthreads()` has been consistently documented as synchronizing all threads in the thread block, Pascal and prior architectures could only enforce synchronization at the warp level. In certain cases, this allowed a barrier to succeed without being executed by every thread as long as at least some thread in every warp reached the barrier. Starting with Volta, the CUDA built-in `__syncthreads()` and PTX instruction `bar.sync` (and their derivatives) are enforced per thread and thus will not succeed until reached by all non-exited threads in the block. Code exploiting the previous behavior will likely deadlock and must be modified to ensure that all non-exited threads reach the barrier.

The racecheck and synccheck tools provided by cuda-memcheck can aid in locating violations of points 2 and 3.

To aid migration while implementing the above-mentioned corrective actions, developers can opt-in to the Pascal scheduling model that does not support independent thread scheduling. See Application Compatibility for details.

# H.6.3. Global Memory

Global memory behaves the same way as devices of compute capability 5.x (See Global Memory).