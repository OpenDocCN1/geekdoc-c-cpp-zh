64-bit words . . . [i], respectively, . . . [i+16]. The latter results in two-way bank conflicts, and lowers the effective local memory bandwidth.

For the Hexiton kernel, we load both the Hamiltonian and the input σ-matrices into the local memory. All matrix elements c_ij ∈ ℂ thereby are split into 64-bit real and imaginary part, and are stored in separate fields . . . real[N*N] and . . . imag[N*N] in local memory. Placing both real and imaginary part of c_ij to local memory one after another would result in four-way bank conflicts. With the 64-bit splitting, we hence take the lesser evil—two-way bank conflicts.

Our final local memory layout, e.g., for d_y = 2, incorporating the point that each work-item processes two matrices at once using the double2 built-in vector data type, is shown in Figure 19.10.

The amount of local memory consumed by that kernel is M = (2 + 4 · d_y) · 8 · N² bytes per work-group. In case of N = 7 and work-group size {64,2}, it takes M = 3920 bytes of the local memory. The maximum number of concurrent work-groups on each of the GPGPU’s CUs then is ⌊(48 · 1024 bytes)/(3920 bytes)⌋ = 12, which corresponds to 1536 work-items per CU, and hence 75% maximum device occupancy. Our final GPGPU kernel consumes 40 registers (32-bit) per work-item, or at most 61,440 registers overall per CU. The total register count of 65,536 per CU thus is not exceeded, and the stated maximum device occupancy hence remains the same. By not using the double2 built-in vector data type for internal computation, we can achieve 100% device occupancy instead. However, the increased per-work-item instruction-level parallelism when using double2 processing overcompensates the reduced occupancy.

```
__local double h_real[N*N];
__local double h_imag[N*N];
__local double sin_real[2][DY][N*N]; // input sigma
__local double sin_imag[2][DY][N*N]; // matrices

// load Hamiltonian -> h_real, h_imag
// load input sigma matrices -> sin_real, sin_imag
int dy=get_local_id(1);

double2 sout1_ij=0.0; // Output sigma
double2 sout2_ij=0.0; // matrices: element (i,j)
for (int k=0; k<N; ++k)
{
  // compute commutator sout<x>=[h, sin<x>] (x=1,2)
  // *** h_ik*sin_kj ***
  double2 s_kj_real=(double2)(sin_real[0][dy][k*N+j],
                              sin_real[1][dy][k*N+j]);
  double2 s_kj_imag=(double2)(sin_imag[0][dy][k*N+j],
                              sin_imag[1][dy][k*N+j]);

  sout1_ij+=h_real[i*N+k]*s_kj_real;
  sout2_ij+=h_imag[i*N+k]*s_kj_imag;
  sout1_ij+=.
  // *** sin_ik*h_kj ***
  double2 s_ik_real=(double2)(sin_real[0][dy][i*N+k],
                              sin_real[1][dy][i*N+k]);
  // ...
```

# FIGURE 19.10

Part of the Nvidia K40m optimized OpenCL Hexiciton Kernel. The entire kernel can be found in the downloadable examples. See the Readme for a mapping of figures and source files.