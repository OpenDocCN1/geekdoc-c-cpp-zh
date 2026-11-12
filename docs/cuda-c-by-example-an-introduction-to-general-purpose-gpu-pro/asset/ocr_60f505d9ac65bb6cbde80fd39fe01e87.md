instruction on any thread. This is exactly what we need! We know know that when the first thread executes the first instruction after our __syncthreads(), every other thread in the block has also finished executing up to the __syncthreads().

Now that we have guaranteed that our temporary cache has been filled, we can sum the values in it. We call the general process of taking an input array and performing some computations that produce a smaller array of results a reduction. Reductions arise often in parallel computing, which leads to the desire to give them a name.

The naïve way to accomplish this reduction would be having one thread iterate over the shared memory and calculate a running sum. This will take us time proportional to the length of the array. However, since we have hundreds of threads available to do our work, we can do this reduction in parallel and take that is proportional to the logarithm of the length of the array. At first, the following code will look convoluted; we'll break it down in a moment.

The general idea is that each thread will add two of the values in cache [] and store the result back to cache []. Since each thread combines two entries into one, we complete this step with half as many entries as we started with. In the next step, we do the same thing on the remaining half. We continue in this fashion for log2 (threadsPerBlock) steps until we have the sum of every entry in cache []. For our example, we're using 256 threads per block, so it takes 8 iterations of this process to reduce the 256 entries in cache [] to a single sum.

The code for this follows:

```
```c
// for reductions, threadsPerBlock must be a power of 2
// because of the following code
int i = blockDim.x/2;
while (i > 0) {
    if (cacheIndex < i)
        cache[cacheIndex] += cache[cacheIndex + i];
    __syncthreads();
    i /= 2;
}
```
```