![](bbox=[0.112, 0.116, 0.868, 0.283])

# FIGURE 9.46 Parallel Nsight “Instruction Statistics.”

![](bbox=[0.112, 0.368, 0.868, 0.533])

# FIGURE 9.47 Parallel Nsight “Branch Statistics.”

2 taking a very long time to execute, it was actually only given a small number of warps to execute. This confirms that it was likely that one of the blocks given to it contained much more work than the other blocks. We also have a very low level of “Eligible Warps per Active Cycle,” which may in turn suggest the SMs are stalling at some point (Figure 9.48).

Looking at the next tab we see the distribution of instruction dependencies (Figure 9.49). Instruction dependencies are caused by the output of one operation feeding into the input of the next. As the GPU uses a lazy evaluation model, the GPU operates best with long instruction dependencies. The graph in Figure 9.49 shows there are too many immediate dependencies. The easiest method to solve this is by introducing some ILP on the thread level. As we in fact have very few blocks, we have a significant number of unused registers that could be used to introduce ILP. We could do this via the vector types or by expanding the loop to process N elements per iteration. We could also use one or more registers to prefetch the values from the next iteration.

The next tab confirms what we saw in the “Eligible Warps” tab, that the SMs are in fact hitting a stall condition. The first pie chart in Figure 9.50 shows that in 69% of the time, the SM has no eligible warp to execute, meaning it will stall or idle, which is of course not good. The second pie chart in Figure 9.50 shows the reason for the stall, which we can see is 85% of the time related to execution dependencies.