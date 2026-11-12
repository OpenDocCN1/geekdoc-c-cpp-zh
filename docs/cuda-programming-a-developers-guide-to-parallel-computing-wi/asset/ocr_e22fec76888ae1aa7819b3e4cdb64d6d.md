with its thread model, you hit a problem. Two or more threads fetch the same value at step three. They all increment it and write it back. The last thread to do the write wins. The value should have been incremented N times, but it’s incremented only once. All threads read the same value to apply the increment to, thus you lose N increments to the value.

The problem here is that you have a data dependency you do not see on the serial execution version. Each increment of the bin value must complete before the read and increment by the next thread. You have a shared resource between threads.

This is not an uncommon problem and CUDA provides a primitive for this called

```
atomicAdd(&value);
```

This operation guarantees the addition operation is serialized among all threads.

Having now solved this problem, you come to the real choice here—how to structure the tasks you have to cover into threads, blocks, and grids. There are two approaches: the task decomposition model or the data decomposition model. Both generally need to be considered.

With the task decomposition model, you simply allocate one thread to every element in input array and have it do an atomic add. This is the simplest solution to program, but has some major disadvantages. You must remember that this is actually a shared resource. If you have 256 bins and an array of 1024 elements, assuming an equal distribution, you have 4 elements contending for each bin. With large arrays (there is no point in processing small arrays with CUDA) this problem becomes the dominant factor determining the total execution time.

If you assume an equal distribution of values in the histogram, which is often not the case, the number of elements contending for any single bin is simply the array size in elements divided by the number of bins. With a 512 MB array (524,288 elements) you would have 131,072 elements contending for each bin. In the worst case, all elements write to the same bin, so you have, in effect, a serial program due to the serialization of the atomic memory writes.

In either example, the execution time is limited by the hardware’s ability to handle this contention and the read/write memory bandwidth.

Let’s see how this works in reality. Here is the GPU program to do this.

```
/* Each thread writes to one block of 256 elements of global memory and contends for write access */
__global__ void myhistogram256Kernel_01(
    const unsigned char const * d_hist_data,
    unsigned int * const d_bin_data)
{
    /* Work out our thread id */
    const unsigned int idx = (blockIdx.x * blockDim.x) + threadIdx.x;
    const unsigned int idy = (blockIdx.y * blockDim.y) + threadIdx.y;
    const unsigned int tid = idx + idy * blockDim.x * gridDim.x;
    /* Fetch the data value */
```