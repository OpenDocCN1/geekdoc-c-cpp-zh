ext_in, and as are the OpenMP parallel regions in the “halo-exchange” routines in each of the three directions (north-south, east-west, up-down). In a typical “fine-grained” fashion, the set of parallel threads is created and destroyed multiple times, with the number of threads in each set determined by the value of OMP_NUM_THREADS.

A key question of interest now is: how easy and how worthwhile is it to merge all those distinct OpenMP-parallel loops into a single large (i.e., coarse-grained) OpenMP parallel region?

In the case of this simple stencil-test, the answer to the first part of that question is that it is quite easy to do. The strategy (which is quite generic and applicable to other applications too) is to let any large arrays (i.e., ext_in and ext_out in the stencil case) remain “shared” (in the OpenMP sense). That means that for each MPI process, only a single copy of each array exists and is accessible by all OpenMP threads. In practice, of course, each thread should access only its own well-defined section of each “shared” array and take care not to step on the toes of any other thread accessing the same array! If possible, only scalars and small work-arrays should be declared “private” (in the OpenMP sense), so each thread has its own separate copy (usually with different values in each). The approach is shown schematically in Figure 17.2 for the stencil case.

Although Figure 17.2 is just schematic, here are some points to note:

+   - There is only one OpenMP parallel section, which encloses pretty much the entire rest of the code, including any I/O, any subroutine calls, and any MPI message-passing.

+   - Loops parallelized with “!$OMP PARALLEL DO” in Figure 17.1 just need the directive “!$OMP DO” in Figure 17.2.

+   - It usually makes sense to use only a single thread to do any I/O, hence the I/O section in Figure 17.2 is enclosed in an “OMP SINGLE” section.

+   - Usually (but not always) it also makes sense to use only a single thread for any message-passing, so the MPI calls in the “halo_exchange” subroutine are also enclosed in an “OMP SINGLE” section (not shown in Figure 17.2).

In a sense, the “fine-grained” OpenMP implementation (as in Figure 17.1) is a single-threaded program interspersed with multi-threaded parallel regions, in each of which a set of multiple threads are created and later destroyed. The more “coarse-grained” implementation shown schematically in Figure 17.2 is more of a multi-threaded program interspersed with single-threaded regions for operations such as I/O or message-passing. The set of multiple threads is only created once near the beginning and destroyed near the end.

The differences in the “halo_exchange” between the “fine-grained” and “coarse-grained” versions are essentially the same as listed above. Any “!$OMP PARALLEL DO” directives are replaced with the simpler “!$OMP DO,” and all the calls to MPI functions are done within a new “!$OMP SINGLE” region in the “coarse-grained” version.

# FULLY COARSE-GRAINED OpenMP CODE

The code shown schematically in Figure 17.2 is coarse-grained in the sense that it contains only one large OpenMP parallel section that starts at the top of the call-tree and encloses the entire working code. However, it may need further modification to make it as fully coarse-grained as it really should be. A hint as to the extra changes needed is provided by the bold-font of the variables nx_loc passed in the