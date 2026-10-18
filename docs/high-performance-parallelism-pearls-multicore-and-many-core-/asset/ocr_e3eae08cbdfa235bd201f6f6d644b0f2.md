| Benchmark | Benchmark Parameters | Optimized OpenCL time, sec | Original OpenMP time, sec | Optimized OpenMP time, sec |
|---|---|---|---|---|
| HotSpot | Grid size: 2048 X 2048 # of iterations: 4800 | 22.2 | 65.9 | 8.11 |
| LUD | predefined well-conditioned matrix, size: 8000 X 8000 | 3.32 | 368 | 3.24 |
| NW | sequence length: 16384 penalty value: 10 | 5.52 | 11.3 | 3.63 |
| CFD | pre-generated file with 193K elements | 9.36 | 28.3 | 9.03 |
| BFS | pre-generated file with 16M nodes and 100M edges | 1.59 | 1.03 | 0.71 |

# FIGURE 20.1

Benchmarks used in the case study, the benchmark parameters, and timing of the OpenCL and baseline OpenMP implementation. All benchmarks are run in offload mode from an Intel® Xeon® processor host to an Intel Xeon Phi coprocessor.

First, we extended the OpenMP code with target pragmas to enable the code to utilize the Intel Xeon Phi coprocessor. The OpenCL code ran on the Intel Xeon Phi coprocessor out of the box. Then, we successively modified the OpenMP code and used the Intel® VTune™ Amplifier XE which helped us to explore inefficiencies and identify where to apply our optimization effort.

In this chapter, we look at the optimization of the HotSpot benchmark in depth; explaining the optimization techniques used and presenting the results. We review other benchmarks where similar optimization techniques have been applied and present their results. We conclude with a summary of results and a discussion of the particularly performance-sensitive differences between the OpenMP and OpenCL standards.

# EXPERIMENTAL SETUP AND TIME MEASUREMENTS

We use the following system in our case study:

+   - Intel® Xeon® E5 processor @ 3.10 GHz: two sockets with eight cores per socket and two hardware threads per core, 32 Gb RAM as a host connected via PCI-E.
+   - Intel Xeon Phi 7120P coprocessor (formerly code named Knights Corner) with 61 cores where each one runs 4 hardware threads, for total of (61 × 4 =) 244 threads. OpenMP and OpenCL