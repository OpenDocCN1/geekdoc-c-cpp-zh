
The kernel code for this change is listed here:

```
__global void reduceNeighoredLess(int *g_idata, int *g_odata, unsigned int n) {
    // set thread ID
    unsigned int tid = threadIdx.x;
    unsigned int idx = blockIdx.x * blockDim.x + threadIdx.x;

    // convert global data pointer to the local pointer of this block
    int *idata = g_idata + blockIdx.x*blockDim.x;

    // boundary check
    if (idx >= n) return;

    // in-place reduction in global memory
    for (int stride = 1; stride < blockDim.x; stride *= 2) {
        // convert tid into local array index
        int index = 2 * tid;
        if (index < blockDim.x)
            idata[index] += idata[index + stride];
        // synchronize within threadblock
        __syncthreads();
    }

    // write result to global memory
    if (tid == 0) g_odata[blockIdx.x] = idata[0];
}
```

Notice the following statement is listed, which creates the array index for each thread:

```
int index = 2 * tid;
```

Because index is multiplied by 2, the following statement uses the first half of a thread block to execute the execution:

```
if (index < blockDim.x)
```

With a block size of 512 threads, the first 8 warps execute the first round of reduction, and the remaining 8 warps do nothing. In the second round, the 4 warps execute the execution, and the remaining 12 warps do nothing. Therefore, there is no divergence at all. Divergence only occurs in the last 5 rounds when the total number of threads at each round is less than the warp size. You will learn how to handle this in the next section.

This new kernel is called in the code segment in the main function after the call to the baseline kernel.

```
// kernel divergence
cudaMemcpy(d_idata, h_idata, cudaMemcpyHostToDevice);
cudaDeviceSynchronize();
tStart = seconds();
reduceNeighoredLess<<<grid, block>>>(d_idata, d_odata, size);
cudaDeviceSynchronize();
Elaps = seconds() - tStart;
cudaMemcpy(h_odata, d_idata, grid.x*sizeof(int), cudaMemcpyDeviceToHost);
gpu_sum = 0;
```

```
for (int i=0; i<grid.x; i++)
    gpu_sum += h_odata[i];
printf("%g Neighbor2 elapsed %d ms gpu: %d <<<%d block %d>>>\n", iElaps, gpu_sum,grid.x,block.x);
```

Testing with Neighborless reduction at device 0: Tesla M2070

$ ./reduceInteger vector size 1677726 grid 32768 block 512

cpu elapsed 0.0291338 sec cpu: 2139535471
gpu elapsed 0.0139112 sec gpu: 2139535471 <<<32768 block 512>>>
gpu Neighborless elapsed 0.009321 sec gpu: 2139535471 <<<32768 block 512>>>

The new implementation is 1.26 times faster than the original implementation. Use the inst_per_warp metric to check the average number of instructions executed by each warp:

$ nvprof --metrics inst_per_warp ./reduceInteger

The results are summarized: the original kernel executed twice as many instructions per warp as the new kernel, an indicator of high divergence in the original implementation.

- Neighbored Instructions per warp 295.562500
- Neighborless Instructions per warp 115.312500

Use the gld_throughput metric to check memory load throughput:

$ nvprof --metrics gld_throughput ./reduceInteger

The results are summarized: The new implementation also has a much higher load throughput as it is performing as much I/O but over a much shorter period of time.

- Neighbored Global Load Throughput 67.663GB/s
- Neighborless Global Load Throughput 80.144GB/s

# Reducing with Interleaved Pages

The interleaved pair approach avoids the striding of elements compared to the neighboring approach: The stride is started at half of the thread block size and then reduced by half on each iteration (Figure 3-24). Each thread adds two elements separated by the current stride to produce a partial sum at each round. Compared with Figure 3-23, the working threads in interleaved reduction are not changed. However, the load/store locations in global memory for each thread are different.

The kernel code for interleaved reduction is as follows:

```
/// Interleaved Pair Implementation with less divergence
__global void reduceInterleaved(int *g_idata, int *g_odata, unsigned int n) {
    // set thread ID
    unsigned int tid = threadIdx.x;
    unsigned int idx = blockIdx.x * blockDim.x + threadIdx.x;

    // convert global data pointer to the local pointer of this block
    int *idata = g_idata + blockIdx.x * blockDim.x;

```

// boundary check
if (idx >= n) return;

// in-place reduction in global memory
for (int stride = blockDim.x / 2; stride > 0; stride >>>= 1) {
    if (tid < stride) {
        idata[tid] = idata[tid + stride];
    }
    // synchronize within threadblock
    __syncthreads();
}

```
// write result for this block to global memory
if (tid == 0) g_odata[blockIdx.x] = idata[0];
```

![](img/506ba3a4c9f451223692f3f0de1f3a0.png)
FIGURE 3-24

Notice the following statement in the kernel. The stride between two elements is initialized to half of thread block size, and then is reduced by half in each round.

```
for (int stride = blockDim.x / 2; stride > 0; stride >>>= 1) {
```

The following statement forces the first half of thread block to execute on the first iteration, the first quarter of thread block on the second iteration, and so on.

```
if (tid < stride)
```

The following code added to the main function to execute interleaved reduction:

```
cudaMemcpy(d_idata, h_idata, size, cudaMemcpyHostToDevice);
cudaDeviceSynchronize();
iStart = seconds(0);
```

```
reduceInterleaved<<<grid, block>>>(d_idata, size);
cudaDeviceSynchronize();
iElaps = seconds() - iStart;
cudaMemcpy(h_odata, d_idata, grid.x*sizeof(int), cudaMemDeviceToHost);
gpu_sum = 0;
for (int i = 0; i < grid.x; i++) gpu_sum += h_odata[i];
printf("gpu interleaved elapsed %f sec gpu_sum: %d block %d\n", iElaps, gpu_sum,grid.x);
```

Testing with reduceInterleaved at device 0: Tesla M2070 with array size 1677726 grid 32768 block 512

```
cpu elapsed 0.0293138 sec cpu: 2139535471 <<<32768 block 512>
gpu elapsed 0.011722 sec gpu: 2139535471 <<<32768 block 512>
gpu Neighborless elapsed 0.001172 sec gpu: 2139535471 <<<32768 block 512>
gpu Interleaved elapsed 0.006967 sec gpu: 2139535471 <<<32768 block 512>
```

The interleaved implementation is 1.69 times faster than the first implementation and 1.34 times faster than the second implementation. This performance improvement is primarily a result of the global memory load and store patterns. Interleaved also means the same amount of warp divergence as Neighborless.

# UNROLLING LOOPS

Loop unrolling is a technique that attempts optimize loop execution by reducing the frequency of branches and loop maintenance instructions. In loop unrolling, rather than writing the body of a loop once and using a loop to execute it repeatedly, the body is written multiple times. By enclosing this loop then its iterations are reduced or removed entirely. The number of copies made of the loop is called the loop unrolling factor. The number of iterations in the enclosing loop is divided by the loop unrolling factor. This is most effective at improving performance for sequential array loops where the number of iterations is known prior to execution.

```
for (int i = 0; i < 100; i++) {
    a[i] = b[i] + c[i];
}
```

If you replicate the body of the loop, the number of iterations can be reduced to half of the original loop:

```
for (int i = 0; i < 100; i += 2) {
    a[i] = b[i] + c[i];
    a[i+1] = b[i+1] + c[i+1];
}
```

The reason for performance gains from loop unrolling may not be readily apparent by looking at the high-level code. The improvement comes from low-level instruction efficiencies and optimizations that the compiler performs the unrolled loop. For example, in the unrolled loop example above, the condition i<100 is only checked fifty times, compared to one hundred times in the original loop. Additionally, because the reads and writes performed in each statement of loop are independent, the memory operations can be issued simultaneously by the CPU.

Unrolling in CUDA can mean a variety of things. However, the goal is the same: Improving performance by reducing instruction overhead and creating more independent instructions. As a result, more concurrent operations are added to the pipeline leading to higher saturation of instruction and memory bandwidth. This provides the warp scheduler with more elegant warps that can help hide instruction or memory latency.

# Reducing with Unrolling

You may notice that each thread block in the reduceInterleaved kernel handles just one portion of the data, which you can consider a data block. If you manually unroll the processing of two data blocks by a single thread block? The following kernel is a revision to the reduceInterleaved kernel: For each thread, two data blocks are summed. This is an example of cyclic partitioning (introduced in Chapter 1): Each thread works on one data block and processes a single element from each data block.

```
 void reduceUnrolled(int *g_idata, int *g_odata, unsigned int n) {
  // set thread ID
  unsigned int tid = threadIdx.x;
  unsigned int idx = blockIdx.x * blockDim.x + threadIdx.x;

  // convert global data pointer to the local pointer of this block
  int *idata = blockDim.x * blockDim.x * 2;

  // unroll 2 data blocks
  if (idx + blockDim.x < n) g_idata[idx] += g_idata[idx+blockDim.x];
  __syncthreads();

  // in-reduction in global memory
  for (int stride = blockDim.x / 2; stride >= 0; stride >>= 1) {
    if (tid < stride) idata[tid] += idata[tid + stride];
    // synchronize within threadblock
    __syncthreads();
  }

  // write result for this block to global memory
  if (tid == 0) g_odata[blockIdx.x] = idata[0];
}
```

Note the following statement added at the start of the kernel. Here, each thread is an element from the neighboring data block. Conceptually, you can think of this as an iteration of the loop that reduces data blocks.

```
if (idx + blockDim.x < n) g_idata[idx] += g_idata[idx+blockDim.x];
```
