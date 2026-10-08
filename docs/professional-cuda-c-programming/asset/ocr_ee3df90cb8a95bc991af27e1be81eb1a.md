The stencil calculation is straightforward. The _coef array is the constant memory array that holds the coefficients discussed above. Also, #pragma unroll is used as a hint to the CUDA compiler that this loop should be atomically unrolled.

```
#pragma unroll
for(int i = 1; i <= RADIUS; i++) {
    tmp += coef[i] * (smem[sidx+i] - smem[sidx-i]);
}
```

Because the difference coefficients are stored in constant memory, which is prepared by the host thread, you simply access them in your kernel. The full kernel is the following:

```
__global void stencil_id(float *in, float *out) {
    // shared memory
    __shared__ float smem[BDIM + 2*RADIUS];

    // index to global memory
    int idx = threadIdx.x + blockIdx.x * blockDim.x;

    // index to shared memory for stencil calculation
    int sidx = threadIdx.x + RADIUS;

    // Read data from global memory into shared memory
    smem[sidx] = in[idx];

    // read halo part to shared memory
    if (threadIdx.x < RADIUS) {
        smem[sidx - RADIUS] = in[idx - RADIUS];
        smem[sidx + BDIM] = in[idx + BDIM];
    }

    // Synchronize (ensure all the data is available)
    __synctreads();

    // Apply the stencil
    float tmp = 0.0f;
    #pragma unroll
    for (int i = 1; i < RADIUS; i++) {
        tmp += coef[i] * (smem[sidx+i] - smem[sidx-i]);
    }

    // Store the result
    out[idx] = tmp;
}
```

Declaring the _coef array in constant memory is as simple as:

```
__constant__ float coef[RADIUS + 1];
```

Initializing constant memory from the host side is then done using cudaMemcpyToSymbol CUDA API:

```
void setup_coef_constant(void) {
    const float h_coef[] = {a0, a1, a2, a3, a4};
}...
```