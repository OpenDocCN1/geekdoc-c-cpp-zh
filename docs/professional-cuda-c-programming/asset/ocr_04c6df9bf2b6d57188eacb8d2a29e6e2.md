```
__global_
void test_shfl_swap(int *d_out, int *d_in, const mask, int firstIdx,
    int secondIdx) {
    int idx = threadIdx.x * SEGM;
    int value[SEGM]

    for (int i = 0; i < SEGM; i++) value[i] = d_in[idx + i];

    swap(value, threadIdx.x, mask, firstIdx, secondIdx);

    for (int i = 0; i < SEGM; i++) d_out[idx + i] = value[i];
}
```

Invoke the kernel by specifying the mask as 1, the first index as 0, and the second as 3:
test_shfl_swap<<<1, block / SEGM>>>(d_outData, d_inData, 1, 0, 3);

These two functions are included in the same file simpleshfl.cu. As shown in the following
results, for each pair of threads the first element of the array thread is swapped
with the fourth element of the second thread.

+   * initial : 0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15
* swap : 7 1 2 3 4 5 6 0 15 9 10 11 12 13 14 8

# Parallel Reduction using the Warp Instruction

In an earlier section, "Parallel Reduction with Shared Memory," you learned how to use shared
memory to optimize parallel reduction algorithms. In this section, you will learn how to solve the
same problem using warp shuffle instructions.

The basic idea is fairly simple. It consists of three levels of reduction:

+   * Warp-level reduction
* Block-level reduction
* Grid-level reduction

A thread block may have several warps. For warp-level reduction, each warp performs its own
reduction. Instead of shared memory, each thread uses a register to store one data element,
reading from global memory:

`int mySum = g_idata[idx];`

Warp-level reduction is implemented as an inline function, as follows:

```
__inline __device__ int WarpReduce(int mySum) {
    mySum += __shfl_xor(mySum, 16);
    mySum += __shfl_xor(mySum, 8);
    mySum += __shfl_xor(mySum, 4);
    mySum += __shfl_xor(mySum, 2);
    mySum += __shfl_xor(mySum, 1);
    return mySum;
}
```