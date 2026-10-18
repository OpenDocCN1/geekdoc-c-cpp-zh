
## CHAPTER 2 NUMERICAL WEATHER PREDICTION OPTIMIZATION

![](img/16cb41208935c5f22dd1044f03f2e31b_58_0.png)

**FIGURE 2.1**

This plot illustrates increases in NWP forecast skill score over time. Installations of new computers at the National Weather Service’s National Centers for Environmental Prediction (NCEP) are shown at the bottom. Increases in forecast skill are well correlated with increases in computing power.

performance tuning. A relatively small number of software engineers support NWP development efforts. Therefore, wholesale change of large NWP codes to different languages or significantly different programming models is not cost effective. NWP codes are large and often evolve rapidly, especially prior to operational implementation. Maintenance of multiple versions of a code optimized for different compute platforms is prohibitively expensive. Performance-portability of a single-source code is a key requirement for NWP. Intel MIC architecture’s ability to be programmed within the same overarching software environment as the Intel Xeon processor family is a good match for the NWP single-source requirement.

### WSM6 IN THE NIM

Performance of any NWP physics package is best evaluated in the context of a dynamical core. For our tests of WSM6, we use the NIM dynamical core. NIM is a recently developed research dynamical core designed for high-resolution global NWP simulations. Here, high resolution means grid spacing that is smaller than 10 km. NIM uses an icosahedral grid that minimizes variation in grid cell sizes when mapped to the globe, as illustrated in Figure 2.2. Since its inception, NIM has been a close collaboration involving NWP domain experts and HPC software engineers. NIM supports serial, MPI, OpenMP, and hybrid MPI+OpenMP build options and has been ported to all major HPC system architectures and software stacks.

![](img/16cb41208935c5f22dd1044f03f2e31b_59_0.png)

**FIGURE 2.2**

The Nonhydrostatic Icosahedral Model (NIM) uses an icosahedral grid as shown above. Except for 12 pentagons, all grid cells are hexagons. Compared to other commonly used discretizations of the sphere, this grid minimizes variation in grid cell spacing across the globe allowing model time step to be maximized.

NIM dynamics computations are performed in single-precision. NIM dynamics arrays are organized with all model columns addressed via a single horizontal dimension, “ipn.” Neighboring columns are located via look-up table. To avoid costs of indirect addressing in the look-up table, the vertical “k” index over each column appears innermost. MPI parallelism is achieved by distributing subsets of model columns across MPI tasks. Dynamically allocated memory maintains global index space on each MPI task and run-time specification of model configuration options (MPI tasks, OpenMP threads, etc.) is preferred wherever possible.

The NIM dynamics is a single-source code that performs well on Intel and AMD CPUs, NVIDIA GPUs, and Intel MIC architecture. The NIM dynamics also exhibits good strong scaling at high resolution. NIM scales from 10,000 cores to 240,000 cores with 96% parallel efficiency on Oak Ridge National Laboratory’s Titan supercomputer at 3 km global resolution. WSM6 is the most expensive physical parameterization in NIM, consuming 18% of total run time. So WSM6 is a logical first target for exploring performance tuning of physics parameterizations on processors and coprocessors.

In contrast to the NIM dynamics, WSM6 computations are performed in double-precision and, for the majority of computations, arrays are stored with the “i” dimension innermost. Due to the differences in storage order and precision, transposition between dynamics arrays and physics arrays is required.

Fortunately, dynamics and physics share a relatively small set of arrays so transposition costs are small (total costs for all physics packages are less than 3% of total run time).

Compared to NIM dynamics, WSM6 computations are somewhat more complex. Some loops contain data-dependent branches that reduce the efficiency of vectorized code. Some computations require calls to intrinsic transcendental functions (e.g., log, power, exponential). Also, some dynamic load imbalance occurs due to uneven distribution of precipitation types across the globe. To avoid excessively skewing performance results due to load imbalance, test runs involve multiple time steps of the dynamical core. To ensure representativeness of our performance results, we repeated many of our experiments using three different input datasets consisting of both real and idealized initial conditions.

Finally, some computations in WSM6 have “k” as the innermost dimension. This “single-column” part of the WSM6 code handles complex data-dependent vertical iterations that start and end at different levels of each column. With significant effort, it is possible to refactor these inner “k” loops to instead have “i” innermost. We will examine tradeoffs related to this refactoring later.

A sample program containing only the WSM6 source code, a simple driver that calls it once, and input and output datasets is downloadable from lotsofcores.com. Code snippets in this chapter are cross-referenced to the sample code whenever possible. All line numbers in this chapter refer to sample code source file src/kernel/wsm6_kernel.F90 unless otherwise noted.

### SHARED-MEMORY PARALLELISM AND CONTROLLING HORIZONTAL VECTOR LENGTH

In NIM, physics packages are threaded by adding OpenMP directives around a single column loop from which all physics packages are called. This approach requires that all code in the entire physics (of which WSM6 is a component) be thread-safe. Unfortunately, some physics packages were not thread-safe. Finding every race condition and performance bug would have been very time consuming and tedious. Fortunately, Intel Inspector largely automates the task of identifying and correcting threading errors. All threading issues were found and fixed in less than 1 week saving us at least 2 weeks of additional laborious and error-prone manual effort.

Our next step was to control vector length by replacing the physics column loop with a loop over “chunks” of columns. Chunk width (number of columns in each chunk) can then be adjusted to tune performance. This technique has been used in many other NWP and climate models such as the Community Atmosphere Model, Integrated Forecast System, and in previous work on WSM5. Since WRF physics routines such as WSM6 already have arrays organized with (i,k,j) ordering, we can use the “i” dimension to loop over a single chunk, “k” to loop over the vertical dimension, and “j” to loop over the chunks. (Recall that in Fortran, the leftmost index is innermost.)

A disadvantage of organizing columns into chunks arises when the total number of columns on each MPI task is not evenly divisible by the chunk width. Since different MPI tasks will almost always be responsible for slightly different numbers of columns, the last “chunk” will nearly always contain unused columns on at least one MPI task. The extra computations are negligible but we must avoid floating-point exceptions from operations on uninitialized data in these unused columns. An “if” mask could be added to every “i” loop but this would require extensive code modifications and could also impede vectorization. Instead, we simply copy the last valid model column into any “empty” columns in the last chunk during the transposition from dynamics-to-physics, as illustrated in Figure 2.3. The extra columns are simply copies of the last valid model column.

```
!$OMP PARALLEL DO PRIVATE ( ij,i,k,j,ipn ) &
!$OMP SCHEDULE(runtime)
    do j = jts,jte
        ij = (j-1)*CHUNK
        ! transpose from dynamics to physics
        do i = its,ite
            ipn = min(ij+i+ips-1,ipe)
            do k = kts,kte
                u_phy(i,k,j) = u_dyn(k,ipn)
                ! transpose other arrays...
            end do  ! k loop
        end do  ! i loop
        ! physics computations on chunk "j", including WSM6
        call nim_mpas_physics_driver(...)
        ! transpose from physics to dynamics
        do i = its,ite
            ipn = ij+i+ips-1
            if ((ips<=ipn).and.(ipn<=ipe)) then
                do k = kts,kte
                    su_dyn(k,ipn) = tend_u_phy(i,k,j)*r_dyn(k,ipn)
                    ! transpose other arrays...
                enddo  ! k loop
            endif
        enddo  ! i loop
    enddo  ! j loop
```

**FIGURE 2.4**

Code to transpose between dynamics and physics data structures. Code additions needed to handle replication of the last dynamics column are highlighted. This code does not appear in the sample code because NIM dynamics is not included.

### ARRAY ALIGNMENT

Alignment of arrays in memory is key to good vector performance on the first generation of Intel Xeon Phi coprocessors. Unaligned arrays can generate inefficient scalar instructions to handle array elements at the beginning and end of each array. The Intel compiler option "-align array64byte" can be used to ensure that every array begins on a vector boundary. In a perfect world, this would be sufficient to ensure that all arrays are really aligned. However, the Intel compiler requires additional assistance in some cases to recognize that some arrays are really aligned. Use of the Intel compiler options "-qopt-report-phase=loop,vec -qopt-report=4" will cause the compiler to complain whenever it is not convinced that an array is really aligned. We use this information to identify opportunities to insert Intel-specific compiler directives "ASSUME_ALIGNED" and "VECTOR ALIGNED" as shown in Figure 2.5. Here the "ASSUME_ALIGNED" directive is used to tell the Intel compiler that the arrays listed are aligned on 64-byte boundaries (e.g., "worka:64"). The "VECTOR_ALIGNED" directive tells the compiler that all the arrays in the immediately following loop are aligned. Note that this optimization is best combined with optional compile-time constants for memory and loop bounds as described below. Telling the compiler that arrays are aligned when they are not will lead to incorrect results or
