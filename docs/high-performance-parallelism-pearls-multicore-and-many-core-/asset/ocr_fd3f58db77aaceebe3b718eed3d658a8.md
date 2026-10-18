![](bbox=[0.14, 0.117, 0.845, 0.499])

**FIGURE 23.17**

A dependency is reported in the Correctness Report.

+   - The m-loop is not vectorized due to conservative compiler assumptions about dependence (already proven by Advisor Correctness to be not the case for given workload).
+   - The l-loop is not vectorized by default, simply because it’s an outer loop (against the m-loop). The message suggests that we can use simd pragma to force the compiler to vectorize the “outer loop.”

Thus the first natural step here is to enable innermost m-loop SIMD-ization by “forcing” the compiler to vectorize the code either using the OpenMP4.0 standard SIMD pragma or the compiler-specific #pragma ivdep (abbreviated from “Ignore Vector DEPendence”). Surprisingly, after vectorizing the loop in that way and rerunning Advisor Survey analysis, we don’t see any performance speedup at all, even though loop at the lbpSUB:1242 is now reported by Advisor as vectorized.

# Projected gain and efficiency

In order to understand the root cause of our performance issue, we should first of all check “Gain” and “Efficiency” data provided by Advisor.

You can see how efficient the advisor thinks the vector code is by comparing the Estimated Gain against the Vector Length. For perfect efficiency, the two values will be the same. The Estimated gain is not measured, but is calculated by a heuristic in Advisor. In our case, we see: