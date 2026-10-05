# 8.2. Introduction to CUDA

the code will deadlock.^6

Suppose all 32 threads of a warp execute line 3 and set their local variables `lockcopy` to 1. All threads of the warp will check the while-loop condition on line 4 using the same warp instruction. The condition will be valid for the entire warp and all the threads will next execute the `atomicExch()` instruction on line 5. Several warps will be competing to read `*lock`. We suppose this warp is lucky and one of its threads read `*lock` to 0. Then the other 31 threads in the warp must read `*lock` to be 1. At this point, we have warp divergence. The thread that read 0 exits the loop and waits for the other threads in the warp to converge to it. The other 31 threads will go back to line 4 and check the while-loop condition and then do the atomic exchange on line 5. While the other 31 threads are in spin-loop, the thread that read 0 from `*lock` and diverged from the warp is inactive. The thread that read 0 cannot enter the critical region and execute the statement on line 6 until all 31 threads in the warp converge with its execution sequence. The other 31 threads cannot get out of the spin-loop until the thread that read 0 gets to line 7 and releases the lock, which means the program is in a deadlock.

The following implementation of `atomicAddDouble()` does not deadlock. Crucially, it is assumed that `*result` and `*lock` are global locations that are initialized to zero before the kernel is called.

```
1 __device void atomicAddDouble(double value,
2     volatile *result, volatile *lock){
3     for(int i=0; i < WARP; i++){
4         if(ThreadIdx.x%WARP==0){
5             int lockcopy=1;
6             while(lockcopy==1)
7                 lockcopy=atomicExch((int *)lock, 1);
8             *result += value;
9             atomicExch((int *)lock, 0);
10     }
11 }
12 }
```

> ^6Thanks to a member of an NVIDIA forum for explaining this point to me.