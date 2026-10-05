
[content]
## 8.2. Introduction to CUDA

```cpp
double ans=0;
int step = blockDim.x*gridDim.x;
for(long i=tid; i < n; i+=step)
    ans = ans + 4.0/(2.0*i+1.0);
if(tid%2==1)
    ans = -ans;
atomicAddDouble(ans, result, lock);
```

Two possibilities exist for the warp divergence in this. In the for-loop on lines 8 and 9, n may be a multiple of neither the step nor the warp size, which will cause exactly one warp to diverge near the end of the loop. All the warps will diverge when executing the conditional on lines 10 and 11.

These instances of warp divergence have little impact on program efficiency and hide no subtlety related to program correctness. The warp divergence that occurs inside the device function atomicAddDouble() called on line 12 has a more subtle effect on program execution.

Our first attempt at implementing atomicAddDouble() follows:

```cpp
void atomicAddDouble(double ans, volatile double *result, volatile int *lock){
    int lockcopy=1;
    while(lockcopy==1)
        lockcopy = atomicExch((int *)lock, 1);
    *result += ans;
    atomicExch((int *)lock, 0);
}
```

This code has a fatal flaw. It will always deadlock. Let us begin by understanding how this code is supposed to work. On line 1, the __device__ qualifier is appended to the function definition. This qualifier is another CUDA extension. Functions defined using __device__ may be called by other device functions or kernels but not by host code.

On line 2, the pointers result and lock are declared with volatile qualifier. The volatile qualifier is a hint to the compiler that several threads use these pointers. Therefore, *result and lock may change by the action of some other thread. Thus, every time *result and lock are used, the compiler will generate a reference to global memory and not values cached in registers.

If we go back to the body of the function atomicAddDouble(), this is provided by CUDA as an extension to the C language. When a thread executes atomicExch(lock, 1), it returns the content of the location *lock and will move 1 to the location after reading *lock. The two actions of reading *lock and writing to *lock are guaranteed to be an atomic unit. Between the actions, hardware guarantees that no other thread is allowed to read or write that location.

Our first attempt at implementing atomicAddDouble() attempts to enclose line 6, which is result within a critical region. If a thread reads the content of *lock to 0, it assumes that the lock is open and can enter the critical region. Before entering the critical region, it writes 1 to *lock so that no other thread be in critical region simultaneously. On line 5, the value of *lock is read into lockcopy, which is a local variable, and 1 is written to *lock using an atomic operation. If *lock is already 1, then its value won't change, and the lock remains shut.

On line 7, the thread exits the critical region by writing 0 to *lock and opening the lock. CUDA syntax for writing device code encourages us to think of each thread as an independent entity. However, the hardware executes warp by warp and not by thread. If we think of how a warp of 32 threads step through atomicAddDouble(), it becomes clear the code will deadlock.^

Suppose all 32 threads of a warp execute line 3 and set their local variables lockcopy to 1. All threads of the warp will check the while-loop condition on line 4 using the same warp instruction. The condition will be valid for the entire warp and all the threads will next execute the atomicExch instruction on line 5. Several warps will be competing to read *lock. Suppose this warp is lucky and one of its threads read *lock to 0. Then the other 31 threads in the warp must read *lock to be 1. At this point, we have warp divergence. The thread that read 0 exits the loop and waits for the other threads in the warp to converge to it. The other 31 threads will go back to line 4 and check the while-loop condition and then do the exchange on line 5. While the other 31 threads are in spin-loop, the thread that read 0 from *lock and diverged from the warp is inactive. The thread that read 0 cannot enter the critical region and execute the statement on line 6 until all 31 threads in the warp converge with its execution sequence. The other 31 threads cannot get out of the spin-loop until the thread that read 0 gets to line 7 and releases the lock, which means the program is in a deadlock.

The following implementation of atomicAddDouble() does not deadlock. Crucially, it is assumed that *result and *lock are global locations that are initialized to zero before the kernel is called.

```cpp
__device void atomicAddDouble(double value,
    volatile *result, volatile *lock){
    for(int i=0; i < WARP; i++){
        if(ThreadIdx.x%WARP==0){
            int lockcopy=1;
            while(lockcopy==1)
                lockcopy=atomicExch((int *)lock, 1);
            *result += value;
            atomicExch((int *)lock, 0);
        }
    }
}
```

> ^6Thanks to a member of an NVIDIA forum for explaining this point to me.

| NBLKS | Partial | Total | NBLKS | Partial | Total |
|---|---|---|---|---|---|
| 3 | 0.65 | 0.65 | 26 | 0.11 | 0.12 |
| 7 | 0.28 | 0.28 | 260 | 0.11 | 0.18 |
| 13 | 0.15 | 0.15 | 2600 | 0.12 | 0.88 |

Table 8.1: Number of cycles per sum the Leibniz series on the K20 coprocessor. The cycles are cycles of the 2.7 GHz AVX host. Data is given for both the kernel in which each thread returns its own sum (partial) and the kernel in which the threads combine to do a reduction (total).

This implementation has an if-statement (lines 4 through 10) nested inside a for-loop (lines 3 through 11). The threads in a warp take turns, and an attempt to enter the critical region is made only inside the if-block. Therefore, there is no deadlock.

# Timing the kernels

Because the K20 has 13 multiprocessors and two thread blocks of 1,024 threads can reside on each of them, anything less than 26 blocks leaves the hardware utilized. Table 8.1 shows that the Leibniz summing program does not reach its speed with faster than 26 thread blocks. Lots of threads do not slow down the leibnitz() kernel, although the leibnitz() kernel which uses atomic instructions to return a single sum, is slowed considerably (see table 8.1). Summing the Leibniz series on the K20 is nearly 2.5 times faster than the Xeon Phi. The speedup of 2.5 is a little surprising. The speedup is probably due to divisions being handled better on the K20 than the Xeon Phi. The main distinction is the programming model.
