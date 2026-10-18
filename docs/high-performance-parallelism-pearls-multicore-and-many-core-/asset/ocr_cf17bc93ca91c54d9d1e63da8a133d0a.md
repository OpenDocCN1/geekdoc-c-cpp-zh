```
*MIC* Begin optimization report for:
single_iteration(FLOAT *, FLOAT *, FLOAT *, int,
int, FLOAT, FLOAT, F
LOAT, FLOAT, FLOAT)

Report from: Vector optimizations [vec]

LOOP BEGIN at hotspot_openmp.cpp(337,9)
    remark #15541: outer loop was not auto-vectorized: consider using SIMD directive
    LOOP BEGIN at hotspot_openmp.cpp(338,13)
        remark #15344: loop was not vectorized:
vector dependence prevents vectorization
        remark #15346: vector dependence: assumed
FLOW dependence between result line 340 and temp
line 340
        remark #15346: vector dependence: assumed ANTI
dependence between temp line 340 and result line
340
    LOOP END
LOOP END
```

# FIGURE 20.9

Vectorization report for the single_iteration() function.

Figure 20.9 identifies that the loop in line 338 (also identified as a hotspot) is not vectorized due to assumed dependencies between the temp and the result arrays.

However, based on the code access patterns, we know that there are no dependencies between the temp and result arrays across iterations of the loop. Therefore, the loop can be safely vectorized with no side effects. So, we add a #pragma omp simd to the inner loop out of the two loops over block elements to inform the compiler to ignore the dependency and use vector instructions.

The result rewards us with the vectorization intensity metric value jumping to 10, as reported in VTune, and the computation time reduced to 13 s! This result provides a very favorable comparison to 45.4 s after blocking and 65.9 s for the baseline code.

It is possible to improve the performance even further by explicitly setting the number of loop iterations enabling the compiler to successfully unroll the inner loop. Therefore, we rewrote the inner block processing loop as shown in Figure 20.10 specifying that it has a constant number of iterations equal to the block size.