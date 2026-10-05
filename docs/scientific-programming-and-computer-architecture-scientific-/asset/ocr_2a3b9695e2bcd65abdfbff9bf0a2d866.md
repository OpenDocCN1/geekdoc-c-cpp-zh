# Chapter 8. Special Topic: Graphics Coprocessor Programming Using CUDA

Let us consider the manner in which the following code fragment is executed by threads grouped into warps:

```
1 int x = threadIdx.x;
2 if (x%2==0)
3 x = x+1;
4 ans += x;
```

Because a warp is a group of 32 threads that execute the same instruction, the discussion will be more precise if phrased using K20 instructions. However, the C statements in this code fragment map almost directly to instructions and will suffice just as well.

Let us suppose all 32 threads in some warp execute line 1. Once this warp instruction completes, all threads in the warp will check the condition on line 2. The condition evaluates to 1 (true) for half the threads in the warp, and it evaluates to 0 for the other threads. The statement on line 3 will correspond to an entire instruction, and when a warp instruction is issued, only half the threads in the warp will be active. The inactive threads do nothing, but stay in sync with the rest of the warp. Line 4 is executed by all the threads in the warp.

Branch instructions can split the threads in a warp so that only some threads are active in some regions of the code. The hardware has to use data structures to keep track of the execution sequence of the different threads so that it knows which threads are active and which ones not. Warp divergence means when a warp instruction is issued, the cores corresponding to the inactive threads must idle. In addition to wasting execution cycles, the manner in which warps diverge and converge have a bearing on program correctness, as we will now see.

# Summing it all using atomic instructions

In the following kernel, result and lock are pointers to single double and int locations, respectively. The partial sum of the Leibniz series will be put in *result.

```
1 //result and lock must be initialized to zero.
2 __global__ void
3 __launch_bounds__(ThInBlock, double* result, int* lock){
4 leibniztotal(int n, 
5 int tid = threadIdx.x+blockIdx.x*blockDim.x;
```