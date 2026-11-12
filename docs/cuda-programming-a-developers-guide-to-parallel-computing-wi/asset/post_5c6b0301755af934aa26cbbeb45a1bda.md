
decrease the number of global memory reads or writes, but you do coalesce all the writes to memory. The kernel for this approach is as follows:

```
__shared__ unsigned int d_bin_data_shared[256];

/* Each read is 4 bytes, not one, 32 x 4 = 128 byte reads */
__global__ void myhistogram256Kernel_O3(
const unsigned int * d_hist_data,
unsigned int * const d_bin_data,
)
{
/* Work out our thread id */
const unsigned int idx = (blockIdx.x * blockDim.x) + threadIdx.x;
const unsigned int idy = (blockIdx.y * blockDim.y) + threadIdx.y;
const unsigned int tid = idx + idy * blockDim.x * gridDim.x;

/* Clear shared memory */
d_bin_data_shared[threadIdx.x] = 0;

/* Fetch the data value as 32 bit */
const unsigned int value_u32 = d_hist_data[tid];

/* Wait for all threads to update shared memory */
__syncthreads();

atomicAdd(&d_bin_data_shared[ ((value_u32 & 0x000000FF) >> 0) ], 1);
atomicAdd(&d_bin_data_shared[ ((value_u32 & 0x0000FF00) >> 8 ) ], 1);
atomicAdd(&d_bin_data_shared[ ((value_u32 & 0x00FF0000) >> 16 ) ], 1);
atomicAdd(&d_bin_data_shared[ ((value_u32 & 0xFF000000) >> 24 ) ], 1);

/* Wait for all threads to update shared memory */
__syncthreads();

/* The write the accumulated data back to global memory in blocks, not scattered */
atomicAdd(&d_bin_data[threadIdx.x], d_bin_data_shared[threadIdx.x]);
}
```

The kernel must do an additional clear operation on the shared memory, as you otherwise have random data left there from other kernels. Notice also you need to wait ( __syncthreads() ) until all the threads in a block have managed to clear their memory cell in the shared memory before you start allowing threads to update any of the shared memory cells. You need to do the same sync operation at the end, to ensure every thread has completed before you write the result back to the global memory.

You should see that, suddenly, you get a huge six times jump in performance, simply by virtue of arranging the writes in order so they can be coalesced. You can now achieve 6800 MB/s processing speed. Note, however, you can only do this with compute 1.2 or higher devices as only these support shared memory atomic operations.

Now that you have the ordering correct, you need to look at reducing the global memory traffic. You have to read every value from the source data, and you only read each value once. You are already using the optimal transfer size for read accesses, so let's look at the data being written. If you process N histograms per block instead of one histogram per block you reduce the write bandwidth by a factor of N.

Table 5.4 shows the value achieved on the 512 MB histogram based on processing different values of N with a Fermi 460 card (which contains seven SMs). You can see a peak of 7886 MB/s at an N value of 64. The kernel is as follows:

```
/* Each read is 4 bytes, not one, 32 x 4 = 128 byte reads */
/* Accumulate into shared memory N times */
__global__ void myhistogram256Kernel_O7(const unsigned int * d_hist_data,
                                        unsigned int * const d_bin_data,
                                        unsigned int N)
{
    /* Work out our thread id */
    const unsigned int idx = (blockIdx.x * (blockDim.x*N) ) + threadIdx.x;
    const unsigned int idy = (blockIdx.y * blockDim.y ) + threadIdx.y;
    const unsigned int tid = idx + idy * (blockDim.x*N) * (gridDim.x);

    /* Clear shared memory */
    d_bin_data_shared[threadIdx.x] = 0;

    /* Wait for all threads to update shared memory */
    __syncthreads();

    for (unsigned int i=0, tid_offset=0; i < N; i++, tid_offset+=256)
    {
        const unsigned int value_u32 = d_hist_data[tid+tid_offset];
        atomicAdd(&d_bin_data_shared[ (value_u32 & 0x000000FF) >> 0 ], 1);
        atomicAdd(&d_bin_data_shared[ (value_u32 & 0x0000FF00) >> 8 ], 1);
        atomicAdd(&d_bin_data_shared[ (value_u32 & 0x00FF0000) >> 16 ], 1);
        atomicAdd(&d_bin_data_shared[ (value_u32 & 0xFF000000) >> 24 ], 1);
    }
    /* Wait for all threads to update shared memory */
    __syncthreads();

    /* The write the accumulated data back to global memory in blocks, not scattered */
    atomicAdd(&d_bin_data[threadIdx.x], d_bin_data_shared[threadIdx.x]);
}
```

Let's examine this a little, because it's important to understand what you are doing here. You have a loop i that runs for N iterations. This is the number of times you will process 256 bytes of data into the shared memory histogram. There are 256 threads invoked for the kernel, one for each bin. As such, the only loop you need is a loop over the number of histograms to process. When you've done one iteration, you move 256 bytes on in memory to process the next histogram (tid_offset += 256).

Notice also that as you're using atomic operations throughout, you need sync points only at the start and end of the kernel. Adding unnecessary synchronization points typically slows down the program, but can lead to a more uniform access pattern in memory.

## Table 5.4 Histogram Results

| Factor | MB/s | Total Blocks | Whole Blocks per SM | Remainder Blocks |
|---|---|---|---|---|
| 1 | 6766 | 524,288 | 74,898 | 3 |
| 2 | 7304 | 262,144 | 37,449 | 1 |
| 4 | 7614 | 131,072 | 18,724 | 6 |
| 8 | 7769 | 65,536 | 9362 | 3 |
| 16 | 7835 | 32,768 | 4681 | 1 |
| 32 | 7870 | 16,384 | 2340 | 6 |
| 64 | 7886 | 8192 | 1170 | 3 |
| 128 | 7884 | 4096 | 585 | 1 |
| 256 | 7868 | 2048 | 292 | 6 |
| 512 | 7809 | 1024 | 146 | 3 |
| 1024 | 7737 | 512 | 73 | 1 |
| 2048 | 7621 | 256 | 36 | 6 |
| 4096 | 7093 | 128 | 18 | 3 |
| 8192 | 6485 | 64 | 9 | 1 |
| 16,384 | 6435 | 32 | 4 | 6 |
| 32,768 | 5152 | 16 | 2 | 3 |
| 65,536 | 2756 | 8 | 1 | 1 |

Now what is interesting here is that, after you start to process 32 or more histograms per block, you see no effective increase in throughput. The global memory bandwidth is dropping by a factor of two every time you increase that value of _N_. If global memory bandwidth is indeed the problem, you should see a linear speed up here for every factor of _N_ you add. So what is going on?

The main problem is the atomic operations. Every thread must contend for access to the shared data area, along with other threads. The data pattern has a huge influence on the execution time, which is not a good design.

We’ll return to this issue later when we look at how you can write such algorithms without having to use atomic operations.

## CONCLUSION

We covered a lot in this chapter and you should now be familiar with how CUDA breaks tasks into grids, blocks, and threads. We covered the scheduling of blocks and warps on the hardware and the need to ensure you always have enough threads on the hardware.

The threading model used in CUDA is fundamental to understanding how to program GPUs efficiently. You should understand how CPUs and GPUs are fundamentally different beasts to program, but at the same time how they are related to one another.

You have seen how arrangement of threads relative to the data you are going to process is important and impacts performance. You have also seen, in particular with applications that need to share data, it is not always an easy task to parallelize a particular problem. You should note that often taking time to consider the correct approach is somewhat more important than diving in with the first solution that seems to fit.

We also covered the use of atomics and some of the problems of serialization these cause. We touched on the problems branching can cause and you should have in the back of your mind the need to ensure all threads follow the same control path. We look at atomics and branching in more detail later in the book.

You have had some exposure to the extended C syntax used within CUDA and should feel comfortable in writing a CUDA program with a clear understanding of what will happen.

By reading this chapter you have gained a great deal of knowledge and hopefully should no longer feel that CUDA or parallel programming is a bit like a black art.

## Questions

- 1. Identify the best and worst data pattern for the histogram algorithm developed in this chapter. Is there a common usage case that is problematic? How might you overcome this?

- 2. Without running the algorithm, what do you think is the likely impact of running this code on older hardware based on the G80 design?

- 3. When processing an array in memory on a CPU, is it best to transverse in row-column order or column-row order? Does this change when you move the code to a GPU?

- 4. Consider a section of code that uses four blocks of 256 threads and the same code that uses one block of 1024 threads. Which is likely to complete first and why? Each block uses four syncthreads() calls at various points through the code. The blocks require no interlock cooperation.

- 5. What are the advantages and disadvantages of an SIMD-based implementation that we find in GPUs versus the MIMD implementation we find in multicore CPUs?

## Answers

- 1. The best case is uniform distribution of data. This is because this loads the buckets equally and you therefore get an equal distribution of atomic operations on the available shared memory banks. The worst case is identical data values. This causes all threads to continuously hit the same shared memory bucket, causing serialization of the entire program through both the atomic operations and bank conflicts in the shared memory. Unfortunately, one very common usage is with sorted data. This provides a variation on the worst-case usage. Here one bank after another gets contiguously hit with atomic writes, effectively serializing the problem. One solution is to step through the dataset such that each iteration writes to a new bucket. This requires knowledge of the data distribution. For example, consider the case of 256 data points modeling a linear function using 32 buckets. Let's assume data points 0 to 31 fall into the first bucket and this is replicated for every bucket. By processing one value for each bucket, you can distribute writes to the buckets and avoid contention. In this example, you would read data points 0, 32, 64, 96, 1, 33, 65, 97, 2, 34, 66, 98, etc.

- 2. The G80 devices (compute 1.0, compute 1.1) don't support shared memory atomics, so the code will not compile. Assuming you modified it to use global memory atomics, we saw a seven-fold decrease in performance in the example provided earlier in the chapter.
