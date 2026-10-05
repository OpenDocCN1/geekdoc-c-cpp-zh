# 8.1. Graphics coprocessor architecture

![](bbox=[0.168, 0.146, 0.831, 0.532])

Figure 8.3: Warps, thread blocks, and grids.

Divergence within a warp can incur heavy penalties. Because a K20 multiprocessor has a limit of 2,048 threads, at most 64 warps can be resident on a single multiprocessor.

In the Kepler microarchitecture, a multiprocessor selects up to four warps to execute during each cycle. Double-precision instructions use two 32-bit registers. Therefore, only two of the four warps can be executing double-precision instructions. Kepler has the ability to dispatch two instructions per warp during every cycle. Because the 755 MHz K20's cycles are so long, the ability to dispatch two instructions per cycle is probably essential.

If threads are grouped into warps, warps are in turn grouped into thread blocks, as shown in figure 8.3. On the K20, a thread block can have at most 1,024 threads or 32 warps. Threads are scheduled onto multiprocessors one thread block at a time. Switching between warps that are already resident on a multiprocessor has zero overhead. However, scheduling a new thread block will incur overhead.

In figure 8.3, the thread block shown is one dimensional. In general, the threads