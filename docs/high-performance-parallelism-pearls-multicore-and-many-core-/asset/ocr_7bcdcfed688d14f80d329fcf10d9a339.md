| Performance metric | Original Goddard code | Optimized Goddard code |
|---|---|---|
| Vectorization intensity | 3.89 | 7.88 |
| L1 compute to data access ratio | 5.83 | 8.62 |
| Estimated latency impact | 222.28 | 98.18 |

# FIGURE 3.15

Performance metrics for the original and optimized Goddard code on the Intel Xeon Phi coprocessor as measured by Intel's profiling tool VTune.

![](bbox=[0.18, 0.33, 0.8, 0.52])

# FIGURE 3.16

MIC processing times for the WRF after code optimizations measured by Intel's profiling tool VTune.

# PERFORMANCE EFFECTS OF THE OPTIMIZATION OF GODDARD MICROPHYSICS SCHEME ON THE WRF

The optimized Goddard microphysics code was incorporated back into the WRF. Intel’s VTune profiles measurements in Figure 3.16 show that after code optimizations, Goddard scheme takes only 7.6% of the total processing time and dynamics is even more dominant at 71.5% share of the total processing time. Thus, it is a natural candidate for further optimization of WRF. In addition, both radiative transfer and PBL are also two physics categories that warrant further optimization efforts as they both take over 7% of the total processing time.

# SUMMARY

We have shown in this chapter that the Intel Xeon Phi coprocessor can be faster than a dual socket Intel Xeon processor system. However, to achieve that, both multi-threading and vectorization have to be utilized. Furthermore, code was optimized for frequent reuse of the cached data to increase computational