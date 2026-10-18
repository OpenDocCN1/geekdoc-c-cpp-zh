![](bbox=[0.194, 0.119, 0.777, 0.461])

# **FIGURE 20.16**

Performance results.

computations to the Intel Xeon Phi coprocessor and achieve the same or better performance versus its OpenCL counterpart. Figures 5.16 and 5.17 show the relative and absolute performance numbers.

The baseline performance gaps were caused, to a great extent, by the differences in the algorithms or data access patterns implemented in the OpenCL and OpenMP codes. After extending the OpenMP versions with the optimizations that were implemented in the OpenCL code, similar or better performance was reached. OpenMP versions with better performance may suggest opportunities to further optimize the OpenCL versions.

We also observed that the OpenCL programming model constrain users to write kernel code that vectorized out of the box. Data decomposition into work groups, implied by the OpenCL model, inspires implementation of algorithms directed toward exploiting data locality.

While the OpenMP programming model does not impose such constrains, implementing an OpenMP code exhibiting vectorization and locality properties (with right algorithm in hands) is not difficult. Applying the OpenMP `pragma omp simd` to the inner loops known to have no dependencies helps vectorize OpenMP code. Exploiting data locality is governed by the algorithm (which is independent on programming model) and data access patterns.

The parallel work scheduling is another factor that should be taken into account when comparing programming models. We saw differences in the performance due to the OpenCL and OpenMP schedulers. However, to make definitive conclusions, the examined benchmarks do not suffice—more benchmarks with imbalanced tasks are required.

Through this case study, we have learned that similar performance can be achieved with either programming model: OpenMP or OpenCL, with similar efforts. The most important factors that repeatedly impacted performance were (1) algorithm choice, (2) memory layout, and (3) data access patterns.