# FIGURE 15.16

4 × 4 tiling of matrix for tiled Cholesky factorization. The tiles are colored according to the BLAS operations that are applied to them in the first pass of the outer-loop for the algorithm in Figure 15.17.

two operations. For the inner most loop, this requires: 2 * (i − (k + 1) + 1) or 2 * (i − k) operations. Thus total complexity is written as:

```
∑_{k=1}^m ∑_{i=k+1}^m 2(i − k) = 2∑_{k=1}^m (m − k + 1)(m − k)/2 ≈ ∑_{k=1}^m k² ≈ m³/3. (15.4)
```

To make use of the high-performance BLAS level-3 functions of the MKL library, we next show a tiled version of the Cholesky factorization algorithm. For this, the matrix is divided into square tiles as shown in Figure 15.16. The algorithm is given in Figure 15.17. The matrix is divided into T tiles for each side.

In Figure 15.16, each tile color corresponds to an MKL BLAS operation, namely, dpotrf, dtrsm, dsyrk, and dgemm. The actual MKL function names for the C-interface for these functions are LAPACKE_dpotrf, cblas_dtrsm, cblas_dsyrk, and cblas_dgemm, respectively. For details on these MKL functions, the reader is referred to the MKL reference manual. The colored tiles in the figure are the ones which are processed in the first iteration of the outer k-loop of the algorithm. In a right-looking algorithm, these colors (and corresponding BLAS operations) move to the right for each outer-loop iteration. The tiles in

```
1: for k = 1, T do
2:   A_{k,k} ← LAPACKE_dpotrf(A_{k,k})
3:   for m = k + 1, T do
4:     A_{m,k} ← cblas_dtrsm(A_{k,k}, A_{m,k})
5:   end for
6:   for n = k + 1, T do
7:     A_{n,n} ← cblas_dsyrk(A_{n,k}, A_{n,n})
8:     for m = n + 1, T do
9:       A_{m,n} ← cblas_dgemm(A_{m,k}, A_{n,k}, A_{m,n})
10:    end for
11:  end for
12: end for
```

# FIGURE 15.17

Tiled Cholesky factorization algorithm.