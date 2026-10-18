# COPROCESSOR-SIDE RESULTS

Figures 13.9 through 13.12 visualize results from the 192 simulations performed on the coprocessor-side. Below are notes regarding coprocessor-side results:

+   - Marks correspond to the average elapsed execution time per compute timestep (in seconds).
+   - TPPC corresponds to the number of hardware threads utilized per physical core.
+   - Reserved core usage (RCU) corresponds to number of hardware threads utilized on the reserved core. For clarity, each value of RCU has been enumerated below:
+     - RCU = 0 corresponds to use of 120, 180, and 240 threads facilitating 2, 3, and 4 hardware TPPC, respectively.
+     - RCU = 1 corresponds to use of 121, 181, and 241 threads facilitating 2, 3, and 4 hardware TPPC, respectively.
+     - RCU = 2 corresponds to use of 122, 182, and 242 threads facilitating 2, 3, and 4 hardware TPPC, respectively.
+     - RCU = 3 corresponds to use of 183 and 243 threads facilitating 3 and 4 hardware TPPC, respectively.
+     - RCU = 4 corresponds to use of 244 threads facilitating 4 hardware TPPC.
+   - PPT corresponds to the ratio of mesh patches to threads. Note that each thread is not guaranteed to compute this number of mesh patches.
+   - Over 10 identical coprocessor-side simulations, there existed not more than a 4.29% difference in performance between two identical runs.
+   - At 2, 3, and 4 hardware TPPC, there existed 30.14%, 42.60%, and 149.33% differences in performance, respectively, between the fastest and slowest run configurations.

![](bbox=[0.12, 0.56, 0.83, 0.83])

# FIGURE 13.9

Coprocessor-side results for the Compact affinity pattern.