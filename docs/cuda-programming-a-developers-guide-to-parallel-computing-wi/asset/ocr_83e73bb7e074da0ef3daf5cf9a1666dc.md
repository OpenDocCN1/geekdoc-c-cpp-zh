You may be wondering why we simply do not just use 84 blocks as we calculated earlier. The issue is one of rounding. The 12 million element dataset does not equally divide into 84 blocks. Thus, some blocks would need to process more than others. This means the logic would need to be more complex, but more complex for _every_ block executed. Just running 84 blocks without solving this issue shows a time of 0.62 ms, for a gain of 0.06 ms over the 384-block version. This demonstrates that the 384-block version introduces small enough blocks that the existing load-balancing mechanism handles it quite well. The value of making the code more complex significantly outweighs the benefits and is only necessary if we in fact do not know the size of the input dataset.

Coming back to the question of shared memory versus atomics, which is faster? We can replace the atomic-based reduction with the following code:

```
// Write initial result to smem - 256 threads
s_mem_data[threadIdx.x] = local_result;
__syncthreads();

// 0 .. 127
if (threadIdx.x < 128)
    s_mem_data[threadIdx.x] += s_mem_data[(threadIdx.x)+128];
__syncthreads();

// 0 .. 63
if (threadIdx.x < 64)
    s_mem_data[threadIdx.x] += s_mem_data[(threadIdx.x)+64];
__syncthreads();

// 0 .. 31 - A single warp
if (threadIdx.x < 32)
{
    s_mem_data[threadIdx.x] += s_mem_data[(threadIdx.x)+32]; // 0 .. 31
    s_mem_data[threadIdx.x] += s_mem_data[(threadIdx.x)+16]; // 0 .. 15
    s_mem_data[threadIdx.x] += s_mem_data[(threadIdx.x)+8]; // 0 .. 7
    s_mem_data[threadIdx.x] += s_mem_data[(threadIdx.x)+4]; // 0 .. 3
    s_mem_data[threadIdx.x] += s_mem_data[(threadIdx.x)+2]; // 0 .. 1
}

// Have thread zero write out the result to GMEM
if (threadIdx.x == 0)
    atomicAdd(result, s_mem_data[0] + s_mem_data[1]);
}
```

Notice how the code works. First, all 256 threads (warps 0..6) write out their current local_result to an array of 256 64-bit values in shared memory. Then those threads numbered 0 to 127 (warps 0..3) add to their result, the result from the upper set of warps. As the warps within a block are cooperating with one another, we need to ensure each warp runs to completion, so add the necessary __syncthreads(); call.

We continue this reduction until the point at which we reach 32 threads, the size of a single warp. At this point all threads within the warp are synchronous. Thus, we no longer need to synchronize the threads, as the thread sync operation is really a warp sync operation within a single block.