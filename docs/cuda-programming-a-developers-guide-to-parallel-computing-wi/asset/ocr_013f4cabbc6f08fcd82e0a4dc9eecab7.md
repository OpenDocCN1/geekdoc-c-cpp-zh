most likely it will be the kernel invocation or the first call into the CUDA API after the kernel invocation.

If you identify the issue as within the kernel, switch to a GPU debugger such as Parallel Nsight or CUDA-GDB. Then simply repeat the process following a single thread through the kernel execution process. This should allow you to see the top-level call that triggers the fault. If not, the cause may be a thread other than the one you are tracking. Typically the “interesting” threads are threads 0 and 32 within any given block. Most CUDA kernel errors that are not otherwise detected are either to do with interwarp or interblock behavior not working as the programmer imagined they would work.

Single step through the code and check that the answer for every calculation is what it is expected to be. As soon as you have one wrong answer, you simply have to understand why it’s wrong and often the solution is then clear. What you are attempting to do is a very high level binary search. By stepping over the code until you hit the failure point, you are eliminating a single level of functionality. You can then very quickly identify the problem function/code line.

You can also use this approach without a debugger if for whatever reason you have no access to such a debugger within your environment or the debugger is in some way interfering with the visibility of the problem. Simply place `#if 0` and `#endif` preprocessor directives around the code you wish to remove for this run. Compile and run the kernel and check the results. When the code runs error free, the error is likely to be somewhere within the section that is removed. Gradually reduce the size of this section until it breaks again. The point it breaks is a clear indicator of the likely source of the issue.

You may also wish to try the approach of seeing if the program runs with the following:

+   - One block of 1 thread.
+   - One block of 32 threads.
+   - One block of 64 threads.
+   - Two blocks of 1 thread.
+   - Two blocks of 32 threads.
+   - Two blocks of 64 threads.
+   - Sixteen blocks of 1 thread.
+   - Sixteen blocks of 32 threads.
+   - Sixteen blocks of 64 threads.

If one or more of these tests fail, it tells you there is some interaction of either the threads within a warp, threads within a block, or blocks within a kernel launch that is causing the issue. It provides a pointer as to what to look for in the code.

# Assertions and defensive programming

Defensive programming is programming that assumes the caller will do something wrong. For example, what is wrong with the following code?

```
char * ptr = malloc(1024);
free(ptr);
```

The code assumes that malloc will return a valid pointer to 1024 bytes of memory. Given the small amount of memory we’re requesting, it’s unlikely in reality to fail. If it fails, malloc returns a null