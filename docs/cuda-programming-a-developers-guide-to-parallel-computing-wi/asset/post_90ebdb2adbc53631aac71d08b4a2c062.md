
As more blocks increase the chance they will not all hit the same resource contention at the same time.

If you are hitting the maximum performance at 16, 32, or 64 threads then this usually indicates there is a contention issue, or that your kernel is highly geared toward ILP and you are using a lot of registers per thread.

Once you have a baseline figure for the ideal number of threads per block, try increasing the amount of work done by each thread to two or four elements using the various vector types (e.g., int2, int4, float2, float4, etc.). You'll typically see this will improve performance further. The easiest way of doing this is to create additional functions with the same name and simply overload the kernel function. CUDA will call the appropriate kernel depending on the type passed to it at runtime.

Using the vector types will increase register usage, which in turn may decrease the number of resident blocks per SM. This in turn may improve cache utilization. Memory throughput will also likely be increased as the overall number of memory transactions falls. However, kernels with synchronization points may suffer as the number of resident blocks drops and the SM has less choice of which warps are available to execute.

As with many optimizations, the outcome is difficult to predict with any degree of certainty, as some factors play in your favor while others don't. The best solution is to try it and see. Then work backwards, to understand what factor(s) are the primary ones and which are secondary. Don't waste your time worrying about secondary factors unless the primary ones are already addressed.

## Sampling performance

The final part of a self-tuning application is sampling. Although you can build a good performance model around compute level and number of SMs, there are many other factors. The same card model may be produced using GDDR3 and GDDR5 memory, the latter having significantly more global memory bandwidth. The same card may be clocked internally at 600 MHz yet also appear as a 900 MHz model. An optimization strategy that works well for a card with 16 SMs may not work well on one with half that number and vice versa. A mobile processor in a laptop may have been put on a PCIe x1 link and may have dedicated or shared memory with the host.

It's impossible to collect every card and address every variation that your product might have to address. Even if you could do this, next week NVIDIA will release another card. This is of course mostly a problem for those people writing consumer applications, rather than the somewhat less diverse Tesla population of cards. Nonetheless, when a new card is released people first expect their existing applications to run on it, and second, if they have upgraded, to see a suitable performance boost.

Sampling is the answer to this issue. Each card will have a peak value in terms of a launch configuration that works best for its particular setup. As we've seen in some of the tests run throughout this book, different cards prefer different setups. The Fermi cards work well with 192 or 256 threads per block, yet the prior GPUs work well with 128 and 192 threads per block. The compute 2.1 cards perform best with 64- or 128-byte memory fetches, mixed with ILP, instead of 32-byte memory fetches and a single element per thread. The earlier cards are hugely sensitive to thread/memory ordering when coalescing. Global memory bandwidth on these cards is a fraction of the newer models, yet they can perform to a similar level with some problems if shared memory is used well. The cache in Fermi can play a big part to the extent that very low thread numbers (32 or 64) can outperform higher occupancy rates if the data is then entirely contained in the cache.

When the program is installed, run a short test suite as part of the installation procedure. Run a loop through all feasible numbers of threads. Try ILP values from one to four elements per thread. Enable and disable shared memory usage. Run a number of experiments, repeating each a number of times, and average the result. Store in a data file or program configuration file the ideal values for and which GPU these relate to. If the user later upgrades the CPU or GPU, then rerun the experiments and update the configuration. As long as you don't do this on every startup, the user will be happy you are tuning the application to make the best possible use of their hardware.

## Section summary

- There are too many factors to say with certainty the effect of a change without actually trying it.
- Some experimentation is often required during development to get the optimal solution.
- The optimal solution will be different on different hardware platforms.
- Write your applications to be aware of the different hardware out there and what works best on each platform, either statically or dynamically.

## CONCLUSION

We've looked in detail at a number of strategies for trying to improve the throughput of your kernels with various examples throughout this chapter. You should be aware of the factors that affect performance and their relative importance (primary ones are transfers, memory/data patterns, and finally SM utilization). Correctness is a key issue in optimizing code. You cannot reliably optimize code without automatic regression testing. This doesn't have to be hugely complex. A back-to-back run against a known working version with several known datasets is entirely sufficient. You should aim to spot 95% plus of the errors before any program leaves your desk. Testing is not the job of some test group, but your responsibility as a professional to produce reliable and working code. Optimization often breaks code and breaks it many times. The wrong answer in one minute instead of the correct answer in one hour is no use to anyone. Always test for correctness after every change and you'll see the errors there and then, as and when they are introduced. You should also be aware that optimization is a time-consuming and iterative process that will grow your understanding of your code and how the hardware functions. This in turn will lead you to design and write better code from the outset as you become more familiar with what does and what does not work well on GPUs.

## Questions on Optimization

- 1. Take an existing program that has one or more GPU kernels. Run the Visual Profiler and Parallel Nsight to analyze the kernels. What are the key indicators you need to look for? How would you optimize this program?
- 2. A colleague brings a printout of a GPU kernel to you and asks your advice about how to make it run faster. What would be your advice?
- 3. Another colleague proposes to implement a web server using CUDA. Do you think this is a good idea? What issues, if any, would you expect with such a program?
- 4. Implement a shared memory version of the odd-even sort, which produces a single sorted list. What issues might you expect to deal with?

## Answers

- 1. You should be looking first to the execution time of each kernel. If one or more kernels dominate the timing, then, until these are optimized, trying to optimize the others is a waste of your time. Second, you should be looking to the timeline, specifically concerning transfers. Are they overlapped with kernel operations and are they using pinned memory or not? Is the GPU busy all the time or only periodically given work by the host? Of the two longest executing kernels, what is causing them to take this time? Is there a sufficient number of threads overall? Are there enough blocks to populate all the SMs? Are there any peaks on one SM, and if so, why? What is the thread to memory pattern and can this be coalesced by the hardware? Are there any serialization points, for example, shared memory bank conflicts, atomics, synchronization points?

- 2. First, you need to understand the problem before looking at specifics. The “look at the code” optimization strategy can be hit or miss. Sure you can probably optimize the code on the paper in some way, but you need much more information to provide a good answer to the question the person is really asking. Probably the best answer would be to tell your colleague to profile the application, including the host timeline, and then come back with the results. In doing this they will likely see what the problems are and these may well not even be related to the original kernel printout.

- 3. Applications that are highly data parallel are well suited to GPUs. Applications that are highly task parallel with lots of divergence threads are not. The typical implementation of a web server on a CPU is to spawn one thread per N connections and to distribute connections dynamically over a cluster of servers to prevent overloading any single node.

GPUs execute code in groups of 32 warps, effectively a vector processor with the ability to follow single-thread control flow when necessary, but at a large performance penalty. Constructing in real time a dynamic web page is very expensive in terms of control flow, a significant amount of which will diverge on a per-user basis. PCIe transfers would be small and not efficient.

A GPU would not be a good choice, with the CPU host being a much better choice. However, the GPU may be able to be used in the back-end operations of the server, performing some analytical work, churning through the user-generated data to make sense of it, etc.

- 4. This is a useful exercise to think about how to solve some open-ended problems. First, the question does not specify how to combine the output of N blocks.

The quickest solution for largest datasets should be the sample sort method as it completely eliminates the merge sort step. The framework for sample sort is provided in the text, but is nonetheless quite a complex sort. However, it suffers from a variable number of elements per bin. A prefix sum that padded the bins to 128-byte boundaries would help significantly. Merge sort is much easier to implement, allows for fixed block sizes, and is what I’d expect most implementations to opt for.

In terms of odd-even sort, the coalescing problems with global memory are largely hidden by the cache in Fermi due to the locality being extremely high. A compute 1.x implementation would need to use shared memory/registers for the sort. It would need to access the global memory in a coalesced manner in terms of loading and writing back.
