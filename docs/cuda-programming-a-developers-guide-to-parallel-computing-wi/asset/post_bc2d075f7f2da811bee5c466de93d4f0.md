
### FIGURE 9.38 Visual Profiler timeline.

### FIGURE 9.39 Visual Profiler, multi-GPU.

## Parallel Nsight

Visual Profiler can, unfortunately, only tell you so much. A much better level of detail can be found with the Parallel Nsight tool, which is a Windows-only visual analyzer and debugger. Even if Windows is not your primary development environment, it’s worth dedicating a spare PC to this tool for its analysis features alone.

Parallel Nsight is a far more in-depth tool than Visual Profiler. It will tell you a lot more about the kernels and what they are doing. However, as with any more complex tool, it takes a little time to learn how to use it well. The Visual Profiler tool is far simpler to set up and use. It’s a beginner’s tool, whereas Parallel Nsight is more of an intermediate to advanced tool. Parallel Nsight will be best set up with a single PC using one or more compute 2.x (Fermi) graphics cards. Parallel Nsight will also run remotely using two PCs, each of which has a NVIDIA graphics card. However, you’ll find it much easier to have one PC, rather than wait whilst data is copied to/from a remote machine. Parallel Nsight presents a number of options for debugging and profiling. The two main choices are “Application Trace” and “Profile.” The “Application Trace” feature allows you to generate a timeline as with Visual Profiler. This is particularly useful for seeing how the CPU interacts with the GPU and shows the times taken for host/device interaction. You should also use the timeline to verify correct operation of streams and overlapping kernel/memory copy operations.

Multiple concurrent GPU timelines are also supported. For example, the timeline in Figure 9.40 shows we’re failing to provide enough work to keep all GPUs busy. Only the computation parts are shown. The Fermi GPUs are shown in red as the first and last context, while the older GPUs are shown in green as the middle two bars. Each red square represents one kernel invocation on a given stream. You can see the first set of kernels end prior to the next set running. We have a huge time period where the first GPU is idle. It’s only through using tools such as Parallel Nsight you can see issues such as this. It’s difficult to see this using host/GPU timers alone.

The next useful feature is the “Profile” option under the Activity Type menu (Figure 9.41). This allows us to profile the CUDA kernels. However, as many of the experiments require multiple runs of the kernel, no timeline can be produced when selecting this option.

Selecting Experiments to Run as “All” from the dropdown box is the simplest option. As you can see from the list of experiments in Figure 9.42, they are quite extensive. To start acquiring data, simply press the “Launch” button in the application control panel (Figure 9.43). Note the green Connection Status circle. This tells you the Parallel Nsight monitor has successfully connected with the target devices. This needs to be green before any other options work. See the help options for details about setting up the monitor.

Once you press the “Launch” button your application will run until such time as it exits. You then will have a number of options in a dropdown box on the top of the screen, the last of which is “GPU Devices” (Figure 9.44). Select this and you will see an overview of the GPU devices in the system.

This is a useful dialog if you are not sure exactly what the properties of a particular device in your system are. Next, change the dropdown menu from “GPU Devices” to “CUDA Launches.” You’ll then see a list of kernels that were executed and various statistics. You’ll also find “Experimental Results” in the panel below the expandable list.

### FIGURE 9.40 Parallel Nsight, multi-GPU timeline.

### FIGURE 9.41 Parallel Nsight Activity Type selection.

In this particular example, we have six kernels. We can see from the results a number of issues. First, none of the kernels achieve a theoretical occupancy above 33% (Figure 9.45). In the case of the first kernel, this is caused by the block limit (8) being hit before we've achieved the maximum of 48 warps that can be resident on the device. Also note that the first kernel does not set the cache configuration and the CUDA runtime uses the PREFER_SHARED option, allocating 48 K to shared memory instead of the cache. As the kernel does not use shared memory, this is pointless. We're missing a call in the host code to set to cache configuration to PREFER_L1 prior to the first kernel call.

### FIGURE 9.42 Parallel Nsight Experiments.

### FIGURE 9.43 Parallel Nsight application Launch control.

### FIGURE 9.44 Parallel Nsight, GPU devices present.

| Device Name | Function Name | Start Time | Duration | Occupancy | Registers/Thread | Grid Size | Block Size | Threads | Cache Configuration | Shared Memory Configuration |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| GeForce GTX 470 | count_gmem_768_kernel | 4,801,264 | 4,340.76 | 0.24 | 10 | (634, 1, 1) | (64, 1, 1) | 1048576 | PREFER_L1 | PREFER_L1_NONE |
| GeForce GTX 470 | count_gmem_768_kernel | 8,213,646 | 1323.28 | 0.17 | 14 | (4, 1, 1) | (64, 1, 1) | 256 | PREFER_L1 | PREFER_L1_L1 |
| GeForce GTX 470 | count_gmem_768_kernel | 1,056,920 | 4796 | 0.02 | 8 | (16, 1, 1) | (64, 1, 1) | 1024 | PREFER_L1 | PREFER_L1_L1 |
| GeForce GTX 470 | count_gmem_768_kernel | 1,056,920 | 3117.204 | 0.23 | 11 | (256, 1, 1) | (64, 1, 1) | 16384 | PREFER_L1 | PREFER_L1_L1 |
| GeForce GTX 470 | count_gmem_768_kernel | 10,068,726 | 3117.204 | 0.23 | 11 | (1034, 1, 1) | (64, 1, 1) | 14080 | PREFER_L1 | PREFER_L1_L1 |
| GeForce GTX 470 | count_gmem_768_kernel | 70,840,965 | 4264.0246 | 0.22 | 22 | (256, 1, 1) | (64, 1, 1) | 16384 | PREFER_L1 | PREFER_L1_L1 |

### FIGURE 9.45 Parallel Nsight occupancy.

The next experiment to look at is the “Instruction Statistics” (Figure 9.46). Here we see a few issues. There is a very high level of instructions that are being issued but not executed. This is indicative of the SM having to serialize and thus reissue the same instructions. We also see a huge spike of activity on SM 2. This is in fact very bad, as it means one of the blocks that we were allocated to this SM performed a huge amount of additional work compared with the other blocks. This indicates the blocks are not equally distributed in terms of work per block, and this is something we need to solve at the algorithm level. Some balancing of the work per block is needed.

The next experiment is the “Branch Statistics,” which tells us how much the execution within a warp diverges (Figure 9.47). We ideally want a very small if not zero value for branch divergence. Here we see 16% of the branches diverge, which contributes to the reissuing of instructions we saw in the “Instruction Statistics” experiment. This too originates from the algorithm in that the amount of work per thread varies. It points to the need to balance the workload between the work blocks.

The next experiment looks at the ability of the SM to issue and execute instructions. We’d expect to see a roughly equal distribute in terms of the “Active Warps per Cycle” chart. It shows that despite SM 2 taking a very long time to execute, it was actually only given a small number of warps to execute. This confirms that it was likely that one of the blocks given to it contained much more work than the other blocks. We also have a very low level of “Eligible Warps per Active Cycle,” which may in turn suggest the SMs are stalling at some point (Figure 9.48).

Looking at the next tab we see the distribution of instruction dependencies (Figure 9.49). Instruction dependencies are caused by the output of one operation feeding into the input of the next. As the GPU uses a lazy evaluation model, the GPU operates best with long instruction dependencies. The graph in Figure 9.49 shows there are too many immediate dependencies. The easiest method to solve this is by introducing some ILP on the thread level. As we in fact have very few blocks, we have a significant number of unused registers that could be used to introduce ILP. We could do this via the vector types or by expanding the loop to process N elements per iteration. We could also use one or more registers to prefetch the values from the next iteration.

The next tab confirms what we saw in the “Eligible Warps” tab, that the SMs are in fact hitting a stall condition. The first pie chart in Figure 9.50 shows that in 69% of the time, the SM has no eligible warp to execute, meaning it will stall or idle, which is of course not good. The second pie chart in Figure 9.50 shows the reason for the stall, which we can see is 85% of the time related to execution dependencies.

### FIGURE 9.46 Parallel Nsight “Instruction Statistics.”

### FIGURE 9.47 Parallel Nsight “Branch Statistics.”
