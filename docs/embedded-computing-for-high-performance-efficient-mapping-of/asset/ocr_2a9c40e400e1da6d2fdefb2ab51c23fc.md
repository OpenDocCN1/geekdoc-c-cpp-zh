We now turn our attention to the matrix multiplication example presented in Section 6.1, that is, (C = A x B), and its mapping onto an OpenCL device. The most obvious OpenCL implementation strategy is to use two dimensions and allow each work-item to compute one element of the C matrix:

```
__kernel void mul1(const int *A,
                     const int *N,
                     const int nz,
                     __global float *A,
                     __global float *B,
                     __global float *C)
{
    int i = get_global_id(0);
    int j = get_global_id(1);
    for (int k = 0; k < nz; k++) {
        C[i*nz+j] += A[i*nz+k] * B[k*nz+j];
    }
}
```

In this version, we use global memory to perform the computation over a 2D space. To further optimize performance, we use private and local memories which are considerably faster than global memory:

```
__kernel void mul2(const int *A,
                     const int *N,
                     const int nz,
                     __global float *A,
                     __global float *B,
                     __global float *C,
                     local float *Bw)
{
    int i = get_global_id(0);
    int iloc = get_local_id(0);
    int nloc = get_local_size(0);
    float Aw[DMY][MY];
    // copy A to private memory
    for (int k=0; k<nz; k++) {
        Aw[k] = A[i*nz+k];
    }
    for (int j = 0; j < nz; j++) {
        // copy B to local memory
        for (int k=iloc; k < nz; k+=nloc) {
            Bw[k] = B[k*nz+j];
        }
        barrier(CLK_LOCAL_MEM_FENCE);
        float sum = 0.0f;
        for (int k = 0; k < nz; k++) {
            sum += Aw[k] * Bw[k];
        }
        C[i*nz+j] = sum;
    }
}
```