# 6.3. MPI examples

# 427

mately 16 bytes of data are accessed for every set of four arithmetic operations, and the figure is 32 bytes if we include the cost of copying from b[] to a(). The cost of this computation will be determined by memory accesses. The bandwidth to memory realized on a 3.33 GHz machine is between 12 and 14 GB/s.

The realized bandwidth to memory and the speed of this program can be improved considerably. In fact, the running time of this program can be nearly half. This program spends much of its time within the nested for-loop on lines 2 through 10 in the member function update(). That loop, unfortunately, has too many inefficiencies in it. The body of the inner loop contains two conditional expressions, and the loop does not use blocking.

It is amusing that although the communication pattern and OpenMP level parallelism have a big impact on the structure of this program, its speed is determined by a single nested and sequential for-loop. To improve the speed of this program, the conditional assignments must be removed from the body of the program. The forloops must be rewritten to implement the Jacobi iteration in blocks to improve cache and TLB usage. Yet another optimization is to use restrict qualifiers.

All timings were obtained on the Lonestar cluster at the Texas Advanced Computing Center. The recommended MPI on that cluster is MVAPICH2. The Jacobi2 class was slower by a factor of four using mpicxx, which is the compilation/linking command of MVAPICH2.¹ OpenMP constructs are recognized by mpicxx. So the C/C++ compiler invokes it generating suboptimal code for the member function update(). The tendency of MPI implementations to subsume compilation/linking within commands as mpicxx, mpiCC, mipc is one we do not endorse. In many programs such this optimization of C/C++ compilation is of greater consequence than MPI message passing. The user's access to the compiler should not be obscured by hiding the compiler beneath another layer. MPI is a library, and one should be able to include it and link it to any library.

# 6.3.3 Matrix transpose

So far in this chapter, we have considered data exchange between two MPI processes and cyclic transfer of data between several MPI processes. Both of these are especially

> ¹A similar slowdown by a factor of 4 was observed on the most recent Stampede cluster using the recommended MVAPICH2.