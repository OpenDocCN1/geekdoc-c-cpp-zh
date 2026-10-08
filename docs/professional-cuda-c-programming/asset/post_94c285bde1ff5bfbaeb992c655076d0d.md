
// write result for this block to global mem
if (tid == 0) g_data[blockIdx.x] = idata[0];
}

Invoke this kernel with the following execution configuration:
reduceCompleteUnrollWarp8<<<grid.x / 8, block>>>(d_idata, d_data, size);

Kernel time gains some marginal improvement, executing 1.06 times faster than
reduceUnrollWarp8, and 9.16 times faster than the original implementation.

```
gpuCmptUnrollW8 elapsed 0.001280 sec gpu_sum: 219393471 <<<grid 4096 block 512>>>
```

## Reducing with Template Functions

While it is possible to manually unroll loops, using template functions can help reduce
branch overhead. CUDA supports template parameters on device functions. You can specify the
block size as a parameter of the template function as:

```
template <unsigned int blockSize>
void reduceCompleteUnroll(int *g_idata, int *g_data, unsigned int n) {
 // set thread ID
 unsigned int tid = threadIdx.x;
 unsigned int idx = blockIdx.x * blockDim.x * 8 + threadIdx.x;
 // convert global data to the local pointer of this block
 int *idata = g_data + blockIdx.x * blockDim.x * 8;

 // unrolling 8
 if (idx + 7*blockIdx.x < n) {
  int a1 = g_idata[idx];
  int a2 = g_idata[idx + blockIdx.x];
  int a3 = g_idata[idx + 2 * blockIdx.x];
  int a4 = g_idata[idx + 3 * blockIdx.x];
  int b1 = g_idata[idx + 4 * blockIdx.x];
  int b2 = g_idata[idx + 5 * blockIdx.x];
  int b3 = g_idata[idx + 6 * blockIdx.x];
  int b4 = g_idata[idx + 7 * blockIdx.x];
  g_idata[idx] = a1+a2+a3+a4+b1+b2+b3+b4;
 }

 syncthreads();
```

```
// in-place reduction and complete unroll
if (blockSize <= 1024 && tid < 512) idata[tid] += idata[tid + 512];
 syncthreads();
```

```
if (blockSize <= 512 && tid < 256) idata[tid] += idata[tid + 256];
 syncthreads();
```

```
if (blockSize>=256 && tid < 128) idata[tid] += idata[tid + 128];
__syncthreads();
```

```
if (blockSize==128 && tid < 64) idata[tid] += idata[tid + 64];
__syncthreads();
// unrolling warp
if (tid < 32) {
volatile int *vsmem = idata;
vsmem[tid] += vsmem[tid + 32];
vsmem[tid] += vsmem[tid + 16];
vsmem[tid] += vsmem[tid + 8];
vsmem[tid] += vsmem[tid + 4];
vsmem[tid] += vsmem[tid + 2];
vsmem[tid] += vsmem[tid + 1];
}
```

```
// write result to this global mem
if (tid == 0) g_odata[blockIdx.x] = idata[0];
```

The only difference compared to reduceUnrollWarp8 is that you replaced block size with a template parameter. The statements that check the block size will be evaluated at compile time and removed if the condition is not true, resulting in a very efficient inner loop. For example, if the kernel invoked with a thread block size of 256 the following

```
blockSize>=1024 && tid < 512
```

would always be false. The compiler would automatically remove it from the executed kernel. The switch-case structure as shown allows the compiler to optimize code for particular block sizes, but means it is only valid to launch reduceCompleteUnroll with certain block sizes.

```
switch (blockSize) {
case 1024:
reduceCompleteUnroll<1024><><grid.x/8, block>>>(d_idata, d_odata, size);
break;
case 512:
reduceCompleteUnroll<512><><grid.x/8, block>>>(d_idata, d_odata, size);
break;
case 256:
reduceCompleteUnroll<256><><grid.x/8, block>>>(d_idata, d_odata, size);
break;
case 128:
reduceCompleteUnroll<128><><grid.x/8, block>>>(d_idata, d_odata, size);
break;
case 64:
reduceCompleteUnroll<64><><grid.x/8, block>>>(d_idata, d_odata, size);
break;
}
```

Table 3-5 summarizes the results of all parallel reduction implementations covered in this

## TABLE 3-5: Reduction Kernel Performance

| KERNEL | TIME (S) | STEP SPEEDUP | CUMULATIVE SPEEDUP |
|---|---|---|---|
| Neighbored (divergence) | 0.011722 | | |
| Neighbored (no divergence) | 0.009321 | 1.26 | 1.26 |
| Interleaved | 0.006967 | 1.34 | 1.68 |
| Unroll 8 blocks | 0.001422 | 4.90 | 8.24 |
| Unroll 8 blocks + last warp | 0.001355 | 1.05 | 8.65 |
| Unroll 8 blocks + loop + last warp | 0.001280 | 1.06 | 9.16 |
| Templated kernel | 0.001253 | 1.02 | 9.35 |

The only difference compared to reduceUnrollWarp8 is that you replaced block size with a template parameter. The statements that check the block size will be evaluated at compile time and removed if the condition is not true, resulting in a very efficient inner loop. For example, if the kernel invoked with a thread block size of 256 the following

```
blockSize>=1024 && tid < 512
```

would always be false. The compiler would automatically remove it from the executed kernel. The switch-case structure as shown allows the compiler to optimize code for particular block sizes, but means it is only valid to launch reduceCompleteUnroll with certain block sizes.

```
switch (blockSize) {
case 1024:
reduceCompleteUnroll<1024><><grid.x/8, block>>>(d_idata, d_odata, size);
break;
case 512:
reduceCompleteUnroll<512><><grid.x/8, block>>>(d_idata, d_odata, size);
break;
case 256:
reduceCompleteUnroll<256><><grid.x/8, block>>>(d_idata, d_odata, size);
break;
case 128:
reduceCompleteUnroll<128><><grid.x/8, block>>>(d_idata, d_odata, size);
break;
case 64:
reduceCompleteUnroll<64><><grid.x/8, block>>>(d_idata, d_odata, size);
break;
}
```

Table 3-5 summarizes the results of all parallel reduction implementations covered in this

## TABLE 3-5: Reduction Kernel Performance

| KERNEL | TIME (S) | STEP SPEEDUP | CUMULATIVE SPEEDUP |
|---|---|---|---|
| Neighbored (divergence) | 0.011722 | | |
| Neighbored (no divergence) | 0.009321 | 1.26 | 1.26 |
| Interleaved | 0.006967 | 1.34 | 1.68 |
| Unroll 8 blocks | 0.001422 | 4.90 | 8.24 |
| Unroll 8 blocks + last warp | 0.001355 | 1.05 | 8.65 |
| Unroll 8 blocks + loop + last warp | 0.001280 | 1.06 | 9.16 |
| Templated kernel | 0.001253 | 1.02 | 9.35 |

Note that the largest performance gain is achieved by reduceUnroll8, which you can check load/efficiency using the following command:

```
$nvprof --metrics load_efficiency,store_efficiency
```

The results are summarized in Table 3-6

## TABLE 3-6: Load/Store Efficiency

| KERNEL | TIME (S) | LOAD EFFICIENCY | STORE EFFICIENCY |
|---|---|---|---|
| Neighbored (divergence) | 0.011722 | | |
| Neighbored (no divergence) | 0.009321 | 16.73% | 25.00% |
| Interleaved | 0.006967 | 77.94% | 95.52% |
| Unroll 8 blocks | 0.001422 | 94.68% | 97.71% |
| Unroll 8 blocks + last warp | 0.001355 | 98.99% | 99.40% |
| Unroll 8 blocks + loop + last warp | 0.001280 | 98.99% | 99.40% |
| Templated kernel | 0.001253 | 98.99% | 99.40% |

## DYNAMIC PARALLELISM

So far in this book, all kernels have been invoked from the host. Dynamic Parallelism allows new kernels to be created on the device. Up until now, you had to express your algorithms as individual kernel launches. Dynamic parallelism enables a more hierarchical approach where concurrency can be expressed in levels.

The ability to create work directly from the device can also reduce the need to transfer control between the host and device, as launch configuration can be made at runtime. In this section, you will gain a basic understanding of dynamic parallelism by implementing the recursive reduction example.

## Nested Execution

With dynamic parallelism, the kernel execution contexts (grids, blocks, launch configuration, and on) you are already familiar with can be applied to kernel invocation directly on the GPU. The same kernel invocation syntax is used to launch a new kernel within a kernel.

In dynamic parallelism, kernel executions are classified into two types: parent and child. A parent thread, parent thread block, or parent grid has launched by a parent. A new grid, the child grid. A child thread, child thread block, or child grid has been launched by a parent. A child grid must complete before the parent thread, parent thread block, or parent grids are considered complete. A parent is not complete until all its child grids have completed.

Figure 3-26 illustrates the scope of a parent grid and child grid. The parent grid is configured and launched by the host, and the invocation and completion of the child grid must be properly nested, meaning that the parent is not complete until all child grids have completed. If the invoking threads do not explicitly synchronize with the launched grids, the runtime guarantees an implicit synchronization between the parent and child. In this figure, a barrier is set in the parent thread to explicitly synchronize with its child grid.

Grid launches in a device thread are visible across a device block. This means that a thread may synchronize on the child grids launched by that or other threads in the same thread block. Execution of a thread block is not complete until all child grids created by all threads in the block have completed. If all threads in a block exit before all child grids have, implicit synchronization on those child grids is triggered.

When a parent launches a child grid, the child is not guaranteed to begin execution until the parent block explicitly synchronizes with the child.

Parent and child grids share the same global and constant memory storage, which have distinct local and shared memory. Parent and child grids have concurrent access to global memory, with weak
