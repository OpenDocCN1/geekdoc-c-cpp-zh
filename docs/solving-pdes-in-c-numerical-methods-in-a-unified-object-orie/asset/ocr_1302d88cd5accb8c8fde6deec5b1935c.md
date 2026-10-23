in P by the standard unit row e^(i), of which all components vanish except the i th one, which is equal to 1.

5. For every i and j that are both in f and satisfy i ≠ j and P_{i,j} ≠ 0, define

W_{i,j} ≡ Σ_{k∈c, P_{i,k}≠0} B_{j,k}.

6. For every i and j that are both in f and satisfy i ≠ j and P_{i,j} ≠ 0, add a fraction of P_{i,j} to every nonzero element P_{i,k} that lies in the same row and in column k ∈ c as follows:

P_{i,k} ← P_{i,k} + (B_{j,k} / W_{i,j}) P_{i,j}.

7. For every j ∈ f, drop the corresponding column from P. (In this step, P becomes rectangular.)

8. For every i ∈ f, divide the i th row in P by its row-sum. (After this step, the row-sums in P are all equal to 1.)

This completes the definition of the prolongation matrix P. The rest of the details of the definition are as in Section 17.8: that is, R = P^T and Q = R A P. The coarse-grid equation Q e = r is solved approximately by one AMG iteration, called recursively.

Because AMG has no theoretical background, it is not clear whether it works for special diagonally dominant examples such as the one in Figure 12.8 above. Still, the present numerical examples show practically no difference between the multigrid versions.

# 17.10 Implementation of Multigrid

As we’ve seen in Section 17.8, the multigrid iteration relies strongly on recursion. The coarse-grid system of the form Q e = r is solved approximately by one multigrid iteration (V-cycle), which is applied to it recursively. This recursive call requires an even coarser grid, and the recursive process continues until the coarsest grid is reached, where a small system is solved (see Figure 17.1). Naturally, these matrices should thus be stored in a recursively defined object.

The "multigrid" class is indeed defined recursively. It contains not only the "sparseMatrix" objects required to store the fine-grid coefficient matrix and transfer operators to and from the coarse grid, but also a pointer-to-multigrid field that contains the address of the next (coarser) "multigrid" object.

This recursive structure is useful not only in the multigrid V-cycle but also in basic member functions of the "multigrid" class, such as constructors and assignment operators.

The structure of the "multigrid" object is displayed schematically in Figure 17.2. The "multigrid" object contains five "sparseMatrix" objects: 'A', 'U', 'L', 'P', and 'R'. The function "createTransfer" constructs the rectangular matrices 'P' and 'R', which transfer information between the fine and coarse grids. (The complete definition of this function is deferred to Section A.18 in the Appendix.) More precisely, 'R' transforms fine-grid vectors