```
mathKernel2 elapsed 0.000014 sec
mathKernel3 elapsed 0.000014 sec
```

You can force the CUDA compiler to not optimize your kernel using branch predication with the following command:

```
$ nvcc -g -arch=sm_20 simpleDivergence.cu -o simpleDivergence
```

Check the divergence of the unoptimized kernels with nvprof as:

```
$ nvprof --metrics branch_efficiency ./simpleDivergence
```

The results are summarized as follows:

```
mathKernel1: Branch Efficiency      83.33%
mathKernel2: Branch Efficiency      100.00%
mathKernel3: Branch Efficiency      71.43%
```

You can also obtain the event counters for branch and divergent branch using nvprof as:

```
$ nvprof --events divergent_branch,divergent_branch ./simpleDivergence
```

The results are summarized as follows:

```
mathKernel1: branch 12 divergent_branch 2
mathKernel2: branch 12 divergent_branch 0
mathKernel3: branch 14 divergent_branch 4
```

The CUDA compiler still performed limited optimizations on mathKernel and mathKernel3 to keep their branch efficiencies above 50 percent. Note that the only reason mathKernel2 does not report branch divergence is that its granularity is a multiple of warp size. Also, separating a single if...else statement in mathKernel into multiple statements in mathKernel3 doubled the number of divergent branches.

> KEY REMINDERS
Divergence occurs when threads within a warp take different code paths.
Different if-then-else branches are executed serially.
Try to adjust branch granularity to be a multiple of warp size to avoid divergence.
D warps can execute different code with no penalty on performance.

# Resource Partitioning

The local execution context of a warp mainly consists of the following resources:

+   * Program counters
* Registers
* Shared memory

The execution context of each warp processed by an SM is maintained on-chip during the entire lifetime of the warp. Therefore, switching from one execution context to another has no cost.