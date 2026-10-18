run-times leave one core for offload runtime services (aka “the COI demon”), providing up to 240 threads available for a user application.

+   - Red Hat Enterprise Linux Server release 6.5 as a host OS.
+   - Intel® Manycore Platform Software Stack (Intel® MPSS) version 3.4.2.

We built the benchmarks with Intel® C++ Compiler version 15.0 and used Intel® OpenCL™ Runtime 14.2 for Intel® CPU and Intel® Xeon Phi™ Coprocessor for Linux.

We used the same approach and implementation as Rodinia for time measurement. The times reported out and compared with for the benchmarks and their versions include the data transfers time, to and from, the coprocessor, the execution time on the coprocessor and, host time required to offload code fragments to the coprocessor when used by the runtime. Data initialization read from files and OpenCL kernel compilation are not included into the measured time. Timestamps are captured using the gettimeofday() function.

# HotSpot BENCHMARK OPTIMIZATION

HotSpot is a 2D-transient thermal modeling kernel that computes the final state of a grid of cells from a given set of initial conditions (temperature and power dissipation per cell). The application iteratively updates the temperature values in all cells in parallel and stops simulation after a fixed number of iterations. The OpenMP version of the workload is located in the openmp/hotspot/hotspot_openmp.cpp source file. The compilation command is:

```
icc -g -fopenmp -O2 hotspot_openmp.cpp -o hotspot_offload
```

The OpenCL program is located in the opencl/hotspot/ directory. There you can find hotspot.c that is the source for the program submitting work to the device and hotspot_kernel.cl that is the OpenCL device kernel. The OpenCL kernel is compiled with compiler default options and only the work group size is given via the definition in the OpenCL compilation command: -DBLOCK_SIZE=16.

The benchmark takes seven input parameters:

+   1. the size of the grid (two parameters),
+   2. the number of iterations,
+   3. the number of OpenMP threads to use,
+   4. the files containing initial temperature and power values, and
+   5. the output file into which to store the result temperature values.

In our case study, we use a 2048 × 2048 grid, 4800 iterations, and 240 threads.

In the OpenMP code, the computations are made within the compute_tran_temp() function that calls the single_iteration() function in the iteration loop.

As a first step, we extended the code of the benchmark with OpenMP target pragmas to run a computation on the Intel Xeon Phi coprocessor. We modified the compute_tran_temp() function as shown in Figure 20.2 and placed an OpenMP target pragma before the iteration loop. This version takes 65.9 s to run (shown in Figure 20.1).

To understand the performance characteristics of HotSpot, we ran the VTune Amplifier’s General Exploration Analysis on the OpenCL and baseline OpenMP versions of the code and compared their results as shown in Figure 20.3. The key differences are marked in Figure 20.3 with numbers 1, 2, and 3: