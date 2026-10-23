![](bbox=[0.24, 0.16, 0.79, 0.49])

Figure 17.1. The multigrid iteration has the shape of the letter V: first, relaxation is used at the fine grid; then, the residual is transferred to the next, coarser, grid, where a smaller V-cycle is used recursively to produce a correction term, which is transferred back to the fine grid; finally, relaxation is used again at the fine grid.

# 17.9 Algebraic Multigrid (AMG)

The prolongation matrix P of Section 17.8 is particularly suitable for diagonally dominant matrices, for which the theory in Chapters 12 and 15 in [68] applies. For more general systems, the multigrid iteration may still converge well, even though no theory applies.

Other multigrid versions may differ from the above method in the way they define the prolongation operator P. The AMG method in [20], [61] differs from the above version in one detail only: before columns are dropped from P, as in Algorithm 17.3 in Section 17.8, the elements in them are distributed among the remaining elements in the same row. (This is in the spirit of [36].)

The algorithm to construct P is as follows. (The algorithm uses some small predetermined threshold, say 0.05.)

# Algorithm 17.4.

+   1. Initialize P by P = A.

+   2. For every i ∈ f and 0 ≤ j < N, if i ≠ j and
+   
+   P_{i,j} / P_{i,i} > -threshold,
+   
+   then drop P_{i,j} from P and replace it by 0:
+   
+   P_{i,j} ← 0.

+   3. Define the matrix B by B = P.

+   4. For every index i ∈ c, replace the ith row
+   
+   (P_{i,0}, P_{i,1}, ..., P_{i,N-1})