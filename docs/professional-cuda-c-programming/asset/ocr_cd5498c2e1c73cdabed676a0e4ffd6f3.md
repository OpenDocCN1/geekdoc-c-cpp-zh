# Reducing with Complete Unrolling

If you know the number of iterations in a loop at compile-time, you can completely unroll it. Because the maximum number of threads per block on either Fermi or Kepler is limited to 1024 (refer to Table 3-2), and the loop iteration count in this reduction kernels is based on a thread block, it is possible to completely unroll the loop reduction:

```
__global void reduceCompleteUnrollWarp8(int *g_idata, int *g_odata,
    unsigned int tid) {
    // set thread
    unsigned int tid = threadIdx.x;
    unsigned int idx = blockDim.x * 8 + threadIdx.x;

    // convert global data pointer to the local pointer of this thread
    int *idata = g_idata + blockDim.x * 8;

    // unrolling 8
    if (idx + 7 < g_idata[idata]) {
        int a1 = g_idata[idata];
        int a2 = g_idata[idata + blockDim.x];
        int a3 = g_idata[idata + 2 * blockDim.x];
        int a4 = g_idata[idata + 3 * blockDim.x];
        int b1 = g_idata[idata + 4 * blockDim.x];
        int b2 = g_idata[idata + 5 * blockDim.x];
        int b3 = g_idata[idata + 6 * blockDim.x];
        int b4 = g_idata[idata + 7 * blockDim.x];
        g_idata[idata] = a1 + a2 + a3 + a4 + b1 + b2 + b3 + b4;
    }
    syncthreads();

    // in-place reduction complete unroll
    if (blockDim.x>=1024 && tid < 512) idata[tid] += idata[tid + 512];
    syncthreads();

    if (blockDim.x>=256 && tid < 256) idata[tid] += idata[tid + 256];
    syncthreads();

    if (blockDim.x>=128 && tid < 64) idata[tid] += idata[tid + 64];
    syncthreads();
    // unrolling warp
    if (tid < 32) {
        volatile int *vsmem = idata;
        vsmem[tid] += vsmem[tid + 32];
        vsmem[tid] += vsmem[tid + 16];
        vsmem[tid] += vsmem[tid + 8];
        vsmem[tid] += vsmem[tid + 4];
        vsmem[tid] += vsmem[tid + 1];
    }
}
```