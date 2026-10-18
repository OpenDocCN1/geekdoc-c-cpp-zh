The computation at each k is independent at each self-consistent field method (SCF) step and the number of SCF cycles vary from a few to hundreds depending upon the chosen algorithm and materials properties. To accelerate the convergence to the solution, extra bands are employed and N_band^tot denotes the total number of bands used in the figure computations.

The representation of Ψ is arbitrary and any nonsingular basis set can be used, for example, δ-functions on a regular spatial 3D grid or Gaussian orbitals centered at the ions. The computational details of Ĥ_k Ψ depend on Ψ. For the concreteness of our discussions, we will use plane-wave basis sets to represent each Ψ as

Ψ_i^k(r) = Σ_G C_{i,k}^G exp(i r · G). (18.2)

where G denote the plane-wave basis set. For an orthorhombic cell of L_x × L_y × L_z, G = (n_x 2π/L_x, n_y 2π/L_y, n_z 2π/L_z) where n_x, n_y, and n_z are integers. The coefficients C_{i,k}^G are the variables to be updated during the SCF cycles. In the plane-wave basis set, a part of Ĥ_k Ψ is performed in the spectral space, while some terms are computed in r on the spatial grid, thus requiring a 3D Fast Fourier transform (FFT) of the bands during an SCF cycle.

There are important characteristics of the ES simulations that will impact how we parallelize these applications with OpenMP as well as with MPI.

+   - The number of electrons N varies from few to 10^4.
+   - The number of N_k ranges from 1 to 10^6 depending upon the desired accuracy and the intended use of these bands.
+   - Fewer N_k are used for bigger N. For large-scale simulations or molecular systems, N_k = 1.
+   - The size of the plane-wave basis set, N_G, increases as N (the volume of the unit cell) and the target accuracy of the solution. Typically, N_G > 10^3.

# PARALLELISM IN ES APPLICATIONS

Equation (18.1) manifests the inherent parallel opportunities that exist in the DFT methods. The loosely coupled computations at each k-point are carried out independently and the reduction over the k-points is performed after the completion of the computations. MPI supports process grouping capability to form a virtual communicator (MPI Group) consisting of a subset of MPI tasks. Using these MPI Group routines, an application can map each k-point or a set of k-points onto an MPI group of N_MPI tasks and distribute N_band^tot bands over the tasks. The tasks within an MPI group are tightly coupled as the double loop Σ_i Σ_j implies. The shaded block in Figure 18.2 represents the data owned by an MPI task. This data partition is commonly used by ES applications and will be the baseline of our experiments.

Each band can be further broken into multiple tasks, necessitating a distributed memory (cluster) FFT with all-to-all transpose. The optimal data distribution will depend on many factors. For large problems N_G ≫ 1, it may not be feasible for a task to own a complete band. Also, there are algorithms that can benefit from distributing the bands over the tasks. These are the implementation details of a real application that need to be addressed by the developers at the design stage to optimize the use of MPI and will not be discussed further here. However, the principal findings of this chapter that show the advantage of OpenMP within an SMP node are applicable to any data-partition scheme at the MPI level.