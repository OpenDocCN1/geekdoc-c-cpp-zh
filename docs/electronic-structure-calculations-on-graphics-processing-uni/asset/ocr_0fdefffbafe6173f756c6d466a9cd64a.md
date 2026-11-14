The most time-consuming part in the SCF iterations is the construction of the Fock matrix. The Fock matrix elements are calculated via three-dimensional (3D) numerical integration [14] using (5.1), with \(\{\phi\}\) representing the basis set and \(V(r_i)\) representing the potential energy operator containing both the Coulomb and exchange-correlation potential:

\(F_{\mu\nu} = -\int \phi_\mu(r_i)V(r_i)\phi_\nu(r_i)dr_i \approx \sum_k^N W_k \phi_\mu(r_i)V(r_i)\phi_\nu(r_i).\) (5.1)

Because the number of matrix elements \(F_{\mu\nu}\) scales quadratically with the number of atomic orbitals \(N_{ao}\), and the number of integration points \(N_G\) scales linearly, the cost of this step formally increases cubically with system size. Neglecting integration grid points in which one or more of the contributors to the integrand become negligibly small reduces this unfavorably high scaling. While this approximation can strongly reduce the number of floating-point operations that should be carried out, and ideally reduce the scaling with system size to linear in the asymptotic limit, it also introduces checking and branching in the algorithm, thereby possibly affecting the peak performance that can be attained. Such undesired side effects are minimized by operating as much as possible on entire batches of grid points, keeping an easy-to-optimize simple algorithm in the innermost parts of the code.

To reduce the number of operations as much as possible, we can rewrite the second part of Eq. (5.1) by combining the weighting factors \(W_k\) and the value of the potential \(V_i\) into a weighted potential value \(O_i = W_i V(r_i)\). These weighted potential values can be reused for every combination of \(\mu\) and \(\nu\), simplifying the integration to

\(F_{\mu\nu} = -\sum_k \phi_{\mu k} O_k \phi_{\nu k}.\) (5.2)

Equation (5.2) can be rewritten as a matrix-matrix multiplication by introducing an auxiliary matrix \(A_{i,k} = O_i \phi_{i,k}\). Use of this auxiliary matrix then also reduces the number of operations needed to evaluate the full Fock matrix to \(N_{ao}N_G + 2N_{ao}^2N_G\); this is demonstrated in Example 5.1.

# Example 5.1 Using a temporary array to reduce the operations needed to create the Fock matrix.

```
do iBasis = 1, naos ! naos is the number of basis functions
    ! prepare the temporary array by multiplying the operator with basis function i
    do kGrid = 1, nGrid ! nGrid is the number of grid points
        temp(kGrid) = operat(kGrid)*basval(kGrid,iBasis)
    end do
    do jBasis = 1, naos
        ! loop over all gridpoints, and multiply temp with basis function j
        do kGrid = 1, nGrid
            FockMat(Basis,iBasis) += temp(kGrid) * basval(kGrid,Basis)
        end do
    end do
end do
```

# 5.2.2 CPU Code SCF Performance

A common element shared by the many different types of calculations possible with the ADF program is the determination of the Kohn-Sham orbitals for a given fixed molecular structure. For these so-called single-point calculations, the computational cost can be split into three major parts: preparation for the SCF (~5–15%), the SCF cycles (70–80%), and the total bonding energy calculation (~15%).