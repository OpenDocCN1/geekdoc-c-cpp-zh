You can also directly observe warp divergence using the nvprof profiler to collect metrics from the GPU. Here, nvprof's branch_efficiency metric is calculated for a sample execution of simpleDivergence

```
$ nvprof --metrics branch_efficiency ./simpleDivergence
```

The following results are reported by nvprof.

| Kernel: mathKernel2(void) | | 100.00% | 100.00% | 100.00% |
| 1 branch_efficiency Branch Efficiency | | 100.00% | 100.00% | 100.00% |

Branch Efficiency is defined as the ratio of non-divergent branches to total branches, and can be calculated using the following formula:

> Branch Efficiency = 100 × \frac{\# Divergent Branches}{\# Branches}

It is odd that no divergence is reported (if, branch efficiency is at 100%). This oddity is caused by a CUDA compiler optimization that replaces branch instructions (which cause actual control to diverge) with predicted instructions for short, conditional code segments.

In branch prediction, a predicate variable for each thread is set to 1 or 0 according to a condition. Conditional flow paths are fully executed, but only instructions with a predicate of 1 are executed. With instructions with a predicate of 0 do not, the corresponding thread does not still execute. The difference between this and actual branch instructions is subtle, but important to understand. The compiler replaces a branch instruction with predicted instructions only if the number of instructions in the body of a conditional statement is less than a certain threshold. Therefore, a long code path will certainly result in warp divergence.

You can rewrite the mathKernel to directly expose branch prediction in the kernel code as follows:

```
__global void mathKernel2(float *c) {
int tid = blockIdx.x * blockDim.x + threadIdx.x;
float ia, ib;
ia = ib = 0.0f;

bool ipred = (tid % 2 == 0);
if (ipred) {
    ia = 100.0f;
}
if (!ipred) {
    ib = 200.0f;
}
c[tid] = ia + ib;
}
```

Compile and run the simpleDivergence cu again with mathKernel added, and the following performance is reported:

```
Warmingup elapsed 0.105021 sec
mathKernel elapsed 0.000017 sec
```