![](bbox=[0.32, 0.12, 0.66, 0.42])

# FIGURE 2.2

The Nonhydrostatic Icosahedral Model (NIM) uses an icosahedral grid as shown above. Except for 12 pentagons, all grid cells are hexagons. Compared to other commonly used discretizations of the sphere, this grid minimizes variation in grid cell spacing across the globe allowing model time step to be maximized.

smaller than 10 km. NIM uses an icosahedral grid that minimizes variation in grid cell sizes when mapped to the globe, as illustrated in Figure 2.2. Since its inception, NIM has been a close collaboration involving NWP domain experts and HPC software engineers. NIM supports serial, MPI, OpenMP, and hybrid MPI+OpenMP build options and has been ported to all major HPC system architectures and software stacks.

NIM dynamics computations are performed in single-precision. NIM dynamics arrays are organized with all model columns addressed via a single horizontal dimension, “ipn.” Neighboring columns are located via look-up table. To avoid costs of indirect addressing in the look-up table, the vertical “k” index over each column appears innermost. MPI parallelism is achieved by distributing subsets of model columns across MPI tasks. Dynamically allocated memory maintains global index space on each MPI task and run-time specification of model configuration options (MPI tasks, OpenMP threads, etc.) is preferred wherever possible.

The NIM dynamics is a single-source code that performs well on Intel and AMD CPUs, NVIDIA GPUs, and Intel MIC architecture. The NIM dynamics also exhibits good strong scaling at high resolution. NIM scales from 10,000 cores to 240,000 cores with 96% parallel efficiency on Oak Ridge National Laboratory’s Titan supercomputer at 3 km global resolution. WSM6, it is the most expensive physical parameterization in NIM, consuming 18% of total run time. So WSM6 is a logical first target for exploring performance tuning of physics parameterizations on processors and coprocessors.

In contrast to the NIM dynamics, WSM6 computations are performed in double-precision and, for the majority of computations, arrays are stored with the “i” dimension innermost. Due to the differences in storage order and precision, transposition between dynamics arrays and physics arrays is required.