Despite most of this being commonplace to you now, it is worth examining the computation for the number of blocks we launch. We discussed how the dot product is a reduction and how each block launched will compute a partial sum. The length of this list of partial sums should be something manageably small for the CPU yet large enough such that we have enough blocks in flight to keep even the fastest GPUs busy. We have chosen 32 blocks, although this is a case where you may notice better or worse performance for other choices, especially depending on the relative speeds of your CPU and GPU.

But what if we are given a very short list and 32 blocks of 256 threads apiece is too many? If we have N data elements, we need only N threads in order to compute our dot product. So in this case, we need the smallest multiple of threadsPerBlock that is greater than or equal to N. We have seen this once before when we were adding vectors. In this case, we get the smallest multiple of threadsPerBlock that is greater than or equal to N by computing (N + threadsPerBlock-1) / threadsPerBlock. As you may be able to tell, this is actually a fairly common trick in integer math, so it is worth digesting this even if you spend most of your time working outside the CUDA C realm.

Therefore, the number of blocks we launch should be either 32 or (N+threadsPerBlock-1) / threadsPerBlock, whichever value is smaller.

```
const int blocksPerGrid =
    min(32, (N+threadsPerBlock-1) / threadsPerBlock );
```

Now it should be clear how we arrive at the code in main(). After the kernel finishes, we still have to sum the result. But like the way we copy our input to the GPU before we launch a kernel, we need to copy our output back to the CPU before we continue working with it. So after the kernel finishes, we copy back the list of partial sums and complete the sum on the CPU.

```
// copy the array 'c' back from the GPU to the CPU
HANDLE_ERROR( cudaMemcpy( partial_c, dev_partial_c,
    blocksPerGrid*sizeof(float),
    cudaMemcpyDeviceToHost ) );
```