
```cpp
#pragma omp for collapse(3)
for(int i=0; i<Xmax; i++)
  for(int j=0; j<Ymax; j++)
    for(int k=0; k<Zmax; k++) {
      il = (i * Ymax + j) * Zmax + k;
      for (int l=0; l<qdim; l++) {
        for (int m=1; m<=half; m++) {
          nextx = fCppMod(i + lbv[3*m],   Xmax);
          nexty = fCppMod(j + lbv[3*m+1], Ymax);
          nextz = fCppMod(k + lbv[3*m+2], Zmax);
          ilnext = (nextx * Ymax + nexty) * Zmax + nextz;
          fSwapPair(
            lbf[il*lbsitelength + l*lbsy.nq + m + half],
            lbf[ilnext*lbsitelength + l*lbsy.nq + m]);
        }
      }
    }
```

![](img/16cb41208935c5f22dd1044f03f2e31b_504_0.png)

**FIGURE 23.13**  
Code listing—The five-level nested loop in `fPropagationSwap`.

**FIGURE 23.14**  
Why No Vectorization?” in advisor survey.

- Runs for over 12 s.
- Has scalar code.
- Cannot be vectorized due to loop dependencies.

When coming across vector dependencies, your role as a programmer is to confirm whether or not there are really dependencies in the code. It can be quite hard to do this, but fortunately with the help of the “Check Dependencies” feature of Advisor XE the task is much easier.

## Dependency analysis

To run a dependency check, simply:

- Select the loops of interest in the Survey window in column 2 of the Survey window.
- Press the “Check Dependencies” button
- Wait for the results. Only select one loop at a time, as there is a large overhead when running this analysis.

![](img/16cb41208935c5f22dd1044f03f2e31b_505_0.png)

# FIGURE 23.15

Dependency analysis shows there are no loop-carried dependencies.

Running the analysis shows that there are no dependencies—see Figure 23.15.

Now, we are certain that there are no dependencies, so it safe to force vectorization for the given loop.

## Introducing a dependency

A genuine dependency can be seen by artificially modifying fSwapPair function call so that the swapped address ranges become overlapping—see Figure 23.16.

Re-running the Dependency analysis on the modified code will produce a “Write After Read” diagnostic as shown in Figure 23.17.

# EXPLORING POSSIBLE VECTORIZATION STRATEGIES

The “particles move” computational kernel has a slightly more complex structure than the previously considered kernels. Particularly, it has five possible levels where we could consider applying SIMD or threading-type parallelism.

For this kind of nested loop structure, the Advisor Source Views with diagnostics and dynamic data embedded into the code are very useful (Figure 23.18).

Notice that there are only three snippets of information embedded for the five loops. Loop-j and loop-k don’t have any information associated with them. This actually correlates with what the programmer requested when specifying #pragma omp for collapse(3)—which means: “please merge iteration space to a depth of 3 nested loops.” As a result, the three loops have been “collapsed” into a single physical loop (from a control flow graph perspective) and that’s exactly what the tool reports out.

The embedded snippets for two inner loops tell us that they have not been vectorized:

```
fSwapPair(
    lbf[il*lbsitelength + l*lbsy.nq + m],
    lbf[il*lbsitelength + l*lbsy.nq + m + 1]);
```

# FIGURE 23.16

Code listing—the changes in bold will produce a loop dependency.

![](img/16cb41208935c5f22dd1044f03f2e31b_506_0.png)

**FIGURE 23.17**

A dependency is reported in the Correctness Report.

- The m-loop is not vectorized due to conservative compiler assumptions about dependence (already proven by Advisor Correctness to be not the case for given workload).
- The l-loop is not vectorized by default, simply because it’s an outer loop (against the m-loop). The message suggests that we can use simd pragma to force the compiler to vectorize the “outer loop.”

Thus the first natural step here is to enable innermost m-loop SIMD-ization by “forcing” the compiler to vectorize the code either using the OpenMP4.0 standard SIMD pragma or the compiler-specific #pragma ivdep (abbreviated from “Ignore Vector DEPendence”). Surprisingly, after vectorizing the loop in that way and rerunning Advisor Survey analysis, we don’t see any performance speedup at all, even though loop at the lbpSUB:1242 is now reported by Advisor as vectorized.

## Projected gain and efficiency

In order to understand the root cause of our performance issue, we should first of all check “Gain” and “Efficiency” data provided by Advisor.

You can see how efficient the advisor thinks the vector code is by comparing the Estimated Gain against the Vector Length. For perfect efficiency, the two values will be the same. The Estimated gain is not measured, but is calculated by a heuristic in Advisor. In our case, we see:

![](img/16cb41208935c5f22dd1044f03f2e31b_507_0.png)

**FIGURE 23.18**  
Diagnostics embedded in the code.

- A potential speedup of 1.22X.
- The Vector Length is 4, calculated from the fact that an AVX vector register can hold 4 doubles (for Intel Compiler 16.X and higher Advisor can also directly obtain this data from compiler vectorization engine).
- A speedup of 4X would be the optimum.

It may be that a speedup of 1.22 is good enough to justify not putting in any more effort, but we’ll do a deeper exploration anyway.

There is one more clue that should alert you to a potential problem. In the “Performance Traits” column is written the word “Shuffles.” The existence of such memory reorganization instructions indicates that there may be inefficient memory access.

## Memory access patterns analysis

We can use the MAP analysis to see whether there are any inefficient memory access patterns. To do this we:

- Select the loop at line 1242 in the Survey (using the same selection approach as for Dependence Analysis, see Figure 23.19).

![](img/16cb41208935c5f22dd1044f03f2e31b_508_0.png)

# **FIGURE 23.19**

Selecting the loop at 1284.

- Run Memory Access Pattern collection.
- Wait for the results. This analysis is relatively expensive. An analysis that normally takes 30 s to run could run for up to 10 min.

> **Note**
> 
> It’s possible to get MAP results much faster by tracking the Memory Access Pattern log in the Advisor GUI. Once you notice the “site end” diagnostic for your loop of interest—consider manually pressing “Stop” on the Advisor Workflow panel; after “stopping” the analysis there will be an access pattern profile for at least one “instance” of the given loop. You can apply a Memory Access Pattern analysis to scalar or vector loops, but working with an original scalar loop might be slightly easier to investigate.

[Figure 23.20](#) shows the result of the MAP analysis. You can see that:

- The Strides Distribution column shows there is a bad access pattern.
- Colors are used on-screen as indicated in the figure with annotations and arrows, the right two-thirds of the bar is colored red—indicating a poor access pattern.

![](img/16cb41208935c5f22dd1044f03f2e31b_508_1.png)

# **FIGURE 23.20**

Memory Access Patterns Analysis for the innermost loop in `fPropagationSwap`.

# FIGURE 23.21

Memory Access Pattern source view.

Looking at the patterns report in bottom of Figures 23.20 and 23.21 you can see that bad memory access comes from:

- Problems P1, P2, & P3 (colored yellow). Three simultaneous packed loads of three mutually related references at 3*m, 3*m+1, 3*m+2 positions—with additional shift of 3 every next scalar iteration (that’s why it’s classified as stride-3).
- Problem P12 has an “unpredictable” or random stride access coming from the swapping routine. It’s not surprising to find random access here, as the address to be swapped is defined by the value in ilnext (being a complex function of lbv array values and m)—leading to a pure form of indirect referencing.

With such a terrible dynamic memory access pattern, at runtime we don’t achieve the static estimated gain of 1.22; in fact, we don’t experience any performance boost at all.

## A final MAP analysis

Let’s try to investigate vectorization for the “outer loop” now—hoping it proves to be better from memory usage perspective. First, we rerun MAP analysis for the outer loop (1-loop). Surprisingly MAP results are much more promising (see Figure 23.22); the random indirect referencing seems to have

![](img/16cb41208935c5f22dd1044f03f2e31b_509_0.png)

# FIGURE 23.22

Memory Access Patterns Analysis for the outer loop in fPropagationSwap.
