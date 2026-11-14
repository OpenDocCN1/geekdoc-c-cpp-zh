
The second difference is that r-space must be sampled at a higher resolution, at least by a factor of 2, to faithfully represent the potential. These two differences lead to an overall inverse transformation that has three steps: pad, transform, interpolate. Note that the r-space representation is thus about $(2)^3/6\pi \approx 15$ times larger than g-space.

To take advantage of the reduced number of g-vectors, many PWDF codes have implemented their own parallel 3D FFTs on top of 1D and 2D standard library calls. That way, the unused corners of g-space do not need to be communicated during the transpose steps. If targeting a single-socket system, it is recommended that full 3D FFTs are used instead, and many codes will fall back to it automatically. For parallel FFTs across many GPU nodes, the behavior of the CPU implementation can be mimicked, but scalability will suffer because of the relatively strong compute performance of the GPU-enabled nodes. To mitigate this, one should set up the run to process each band on the smallest possible number of nodes, which may require reducing the number of bands that are concurrently processed. Putting different bands from the same k-point in different memory spaces can also cause problems because of the need for inner products between test functions, which will be discussed shortly.

## 7.3.1.2 Projection

Projection is the process of computing the inner products $\langle \beta(k) | \phi_{ak} \rangle$, where $\beta$ are the pseudopotential projectors, and $k$ is a k-point. The projectors connect to a space of pseudo-wavefunctions, $\tilde{\theta}$, with the completeness relation:

$I_i = \sum_I \langle \tilde{\theta}_i | \rho_I \rangle_j$ (7.38)

where $I_i$ denotes identity only in the pseudo-wave space of ion $i$, and $I$ indexes angular momentum. Projection can be done in either r-space or g-space. In g-space, the projection is computed as:

$\langle \beta(k) | \phi_{ak} \rangle = \sum_g \langle \beta(k) | g \rangle \langle g | \phi_{ak} \rangle$ (7.39)

The matrix representation $\langle g | \beta(k) \rangle$ is dense, so projection is a matrix-vector product. Technically, this corresponds to a LAPACK call of the ZGEMM ( 'C' , ... ) function, that has been ported to the GPU [34].

In r-space, each projector is nonzero only within a sphere centered at an ionic center. Let those r-space basis vectors for which the projector is non-zero be $\{ r' \}$. Including the ion and angular momentum indices

$\langle \beta(k_i) | \phi_{ak} \rangle = \sum_{r_i, r'} \langle \beta_i | 0 \rangle (r') | e^{i(k+r)} (r | \phi_{ak} \rangle$ (7.40)

where the sums over $r_i$ are independent of total system size, and $\exp [ i(k \cdot r) ]$ is included because the real-space projectors are defined at $k=0$. The transformation described by $\langle r | r' \rangle$ is best described as a gather operation, as it collects r-space data that is distributed contiguously in memory. The angular momentum components on each atom share r-space subsets, so the number of gathers is the number of ions, not the total number of projectors. An example kernel implementing the projection is found in Listing 1.

The inverse transformation in r-space has a similar form:

$\langle r | \tilde{\phi}_{ak} \rangle = \sum_{k_i, r'} e^{-i(k+r')} \langle r | r' \rangle \langle r' | \tilde{\theta}_i | \tilde{\phi}_{ak} \rangle$ (7.41)

Here, the transformation $\langle r | r' \rangle$ is a scatter operation, with similar issues to the gather. An example kernel implementing the inverse projection can be found in Listing 2.

Both methods of projection are equally valid methodologically, so the choice is purely based on performance. The advantage of the more complex r-space projection is the independence on total system size. The disadvantages are that (1) r-space is about 15 times larger to begin with, and (2) gather operations can be inefficient on memory designed for sequential access.

## 7.3.2 Functionals

For nontrivially sized systems, the construction of the potentials V^loc and V^nl are not performance-critical. They consist of O(n) operations applied to the charge density and two Fourier transforms used for a Poisson solve. Section 7.6 provides an indirect treatment under the constraint a = b, which specifies the two particle potential in exact exchange to a single particle Coulomb potential. It omits the exchange-correlation functional.

## 7.3.3 Diagonalization

The Hamiltonian is block-diagonal with respect to the index k, as seen in Eq. (7.6). Each k-point is an independent eigenproblem, and can be parallelized over freely. In the rest of this subsection, we will omit the k label.

Only the n << N eigenfunctions corresponding to the lowest eigenvalues are generally required, as only they will correspond to nonzero occupancies. Implementing fast iterative matrix diagonalization is one of the key points to attaining a high performance and robust computation. Common choices were described in Section 7.2.5.

All solvers require the implementation of the action H(|phi>) and an inner product <phi'|H|phi>, for arbitrary test functions |phi>, |phi'>. In some cases, it may be easier to compute <phi'|H|phi> in a single step, rather than <phi'|H(|phi>)>, so we will treat this as a special case.

In PWDF codes, the test functions are generally stored in the g-space, <g|phi>. Evaluating the action of the Hamiltonian further requires the r-space, <r|phi>, and beta-space representations, <beta|phi>. If there is sufficient memory, these quantities can be computed once per test function and stored for reuse. This is frequently done for |beta>, because it is much smaller than <g|phi>. The r-space representation can be a factor of $48/\pi$ larger than the g-space representation, so it is less frequently stored. The r-space and g-space representations are complete, so inner products can be computed in either r-space or g-space. Because of the larger size of r-space, g-space is always preferable. Inner products should be blocked together into matrix-matrix products whenever possible.

### 7.3.3.1 Kinetic Energy

The action of the kinetic energy T consists in a simple multiplication of the test function by the vector |g + k|^2. If the g-vectors are in order, this can be easily done by computing |g + k|^2 in the kernel based on the indices. If the g-vectors are out of order, then one should first precompute a vector |g + k|^2, and then perform an element-wise vector product.

As element-wise products are bandwidth-bound, it should be used carefully to reduce loads. For example, when computing the kinetic energy of a set of test functions |phi>, then a loop over products will reload the prefactors and thus reduce the performance. A better approach is to cast this operation into a matrix-matrix multiplication, where the first matrix is diagonal. Although BLAS does not include such an operation, cuBLAS does as ZDGMM [34]. Furthermore, the prefactor here is real while the test function is complex. Thus, a custom kernel can load reals for half the bandwidth. Finally, the operation can be performed in-place. Such a kernel is found in Listing 3. This functionality is not currently available in standard libraries.

### 7.3.3.2 Local Potential

To compute the action of the local potential, $\langle r | V^{loc} | \phi \rangle$, the same operation is performed in $r$-space, with $V(r)$ replacing $|g + k|^2$ as the prefactor. Again, a single test function corresponds to an element-wise product while with a set of test functions, a ZDGMM call or custom kernel. As in the kinetic energy case, the prefactors are real. If the desired result is in $g$-space, then the $r$-space action should be Fourier-transformed.

### 7.3.3.3 Nonlocal Potential

The nonlocal potential in the projector space is either diagonal, in the case of NCPP, or block-diagonal, in the case of USPP. For NCPP, the action of the nonlocal potential proceeds as for the kinetic and local terms, but with a sum over the projections. For USPP, the blocks correspond to atoms, so the action looks like $\langle \tilde{p}_{i,j} | V^{nl} | \phi \rangle = \sum_{i'} \langle \tilde{p}_{i,j} | V^{nl} | \tilde{p}_{i',j} \rangle \langle \tilde{p}_{i',j} | \phi \rangle$. (7.42)

The $l,l'$ angular momentum indices take a small set of values, about 10, so these matrix products are very small and simply looping over matrix-matrix calls is likely to be kernel-launch-bound. If batched calls, discussed in greater depth in Chapter 2, are available, they should be used. Otherwise, a custom kernel can achieve moderate performance, such as the one given in Listing 4.

As with the kinetic and local potential, the nonlocal potential is real. If the desired result is in $g$-space but the $r$-space projection was used, the result can be added to $\langle r | V | \phi \rangle$ prior to the Fourier transformation back to $g$-space, removing the need for an additional Fourier transform.

In the case of USPPs, the action of the overlap matrix, $S|\phi\rangle$, is needed. This is computed as the nonlocal potential, but for an overlap operator $Q_{LL'}$, and then added to the identity: $S|\phi\rangle = |\phi\rangle + \sum_{LL'} |\beta_L\rangle Q_{LL'} \langle \beta_{L'} | \phi \rangle$. (7.43)

where $Q$ has the same structure as $V^{nl}$. If both $H|\phi\rangle$ and $S|\phi\rangle$ must be computed, the projections $\langle \beta | \phi \rangle$ can be reused to great effect.

**Expansion-set techniques.** In all the iterative methods, there will be direct solutions of small eigenproblems expressed in the expansion set. They can be solved on the GPU using libraries, such as MAGMA [35]. When their size is small, they can be low performance. Fortunately, in that case, they contribute little to the overall run time of the method.

For RMM-DIIS, the final orthonormalization can be performed efficiently using a Cholesky decomposition. First, the overlap matrix $S(i,j) = \langle \varphi_i | \varphi_j \rangle$ is computed. Next, the overlap matrix is decomposed as $S = LU$, which can be performed using LAPACK or MAGMA. Finally, the orthonormalized orbitals are given by $|\varphi\rangle = U^{-1}|\varphi\rangle$, where the inverse can also be evaluated using LAPACK or MAGMA.

The eigenproblems in subspace methods are built with the matrix elements $\langle \phi' | H | \phi \rangle$ and, in the case of USPP and PAW, $\langle \phi' | S | \phi \rangle$. In this case, the inner product can be split into different bases: $\langle \phi' | H | \phi \rangle = \sum_k \langle \phi' | g \rangle \langle g | T | g \rangle \langle g | \phi \rangle + \sum_r \langle \phi' | r \rangle \langle r | V^{loc} | r \rangle \langle r | \phi \rangle + \sum_{ij} \langle \phi' | \tilde{p}_i \rangle \langle \tilde{p}_i | V^{nl} | \tilde{p}_j \rangle \langle \tilde{p}_j | \phi \rangle$. (7.44)
