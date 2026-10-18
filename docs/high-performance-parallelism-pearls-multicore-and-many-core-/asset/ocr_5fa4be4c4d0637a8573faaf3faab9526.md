![](bbox=[0.22, 0.11, 0.79, 0.22])

# FIGURE 23.15

Dependency analysis shows there are no loop-carried dependencies.

Running the analysis shows that there are no dependencies—see Figure 23.15.

Now, we are certain that there are no dependencies, so it safe to force vectorization for the given loop.

# Introducing a dependency

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