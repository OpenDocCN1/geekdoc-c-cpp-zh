```
if (threadIdx.x < 16)
{
    if (threadIdx.x < 8)
    {
        a[tid] += b[tid] * c[tid];
    }
    else
    {
        a[tid] -= b[tid] * c[tid];
    }
}
else
{
    a[tid] += b[tid] * c[tid];
}
}
```

```
// Thread diverge into one eighth group
__global__ void cuda_test_kernel_branched_eighth(
    u32 * const a,
    const u32 * const b,
    const u32 * const c,
    const u32 num_elements)
{
    const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;

    if (tid < num_elements)
    {
        for (u32 iter=0; iter<MAX_ITER; iter++)
        {
            if (threadIdx.x < 16)
            {
                if (threadIdx.x < 8)
                {
                    if (threadIdx.x < 4)
                    {
                        a[tid] += b[tid] * c[tid];
                    }
                    else
                    {
                        a[tid] -= b[tid] * c[tid];
                    }
                }
                else
                {
                    if (threadIdx.x >= 8)
                    {
                        a[tid] += b[tid] * c[tid];
                    }
                    else
                    {
                        a[tid] -= b[tid] * c[tid];
                    }
                }
            }
        }
    }
}
```