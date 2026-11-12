![](bbox=[0.11, 0.12, 0.87, 0.54])

# FIGURE 9.33 Visual C options—how to keep PTX files.

If we look at a small device function, this is what we see at the various levels:

```
__global__ void add_prefix_sum_total_kernel(
    u32 * const prefix_idx,
    const u32 * const total_count)
{
    const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;
    prefix_idx[tid] += total_count[blockIdx.x];
}
```

In PTX:

```
.entry _Z27add_prefix_sum_total_kernelPjPjK(
    .param .u64 _Z27add_prefix_sum_total_kernelPjPjK_param_0,
    .param .u64 _Z27add_prefix_sum_total_kernelPjPjK_param_1
{
```