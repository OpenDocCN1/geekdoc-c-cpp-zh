

```text
P(At), R(grids ?
    P.createTransfer(nodes1, nodes2,
        nodes3, T(2.) * diagonal(AtA) - AtA)
    :
    0),
```

在此过程中，传递给“createTransfer”函数的局部变量“nodes1”、“nodes2”和“nodes3”通过非常量引用，其新值与粗网格矩阵 RAP 相关：

```text
next(grids&&(R.rowNumber() < .95*A.rowNumber()) ?
    new multigrid(grids - 1,
        R*A*P, nodes1,nodes2,nodes3)
    :
    0){
} // constructor with matrix argument
```

这完成了多重网格类的定义，用于实现第 17.12 节和 31.5 节中 Stokes、Navier–Stokes 或 Maxwell 系统的多重网格版本。

## 参考文献

- [1] Ames, W.F.: Numerical Methods for Partial Differential Equations. Academic Press, London, 1977.
- [2] Bank, R.E., Dupont, T.F., and Yserentant, H.: The Hierarchical Basis Multigrid Method. Numer. Math. 52 (1988), pp. 427–458.
- [3] Baruch, G., Fibich, G., and Tsynkov, S.: High-Order Numerical Solution of the Nonlinear Helmholtz Equation with Axial Symmetry. J. Comput. Appl. Math. 204 (2007), pp. 477–492.
- [4] Baruch, G., Fibich, G., and Tsynkov, S.: High-Order Numerical Method for the Nonlinear Helmholtz Equation with Material Discontinuities in One Space Dimension. J. Comput. Phys. 227 (2007), pp. 820–850.
- [5] Ben-Artzi, M., and Falcovitz, J.: A Second-Order Godunov-Type Scheme for Compressible Fluid Dynamics. J. Comput. Phys. 55 (1984), pp. 1–32.
- [6] Ben-Artzi, M., and Falcovitz, J.: Generalized Riemann Problems in Computational Fluid Dynamics. Cambridge University Press, New York, 2003.
- [7] Bondeson, A., Rylander, T., and Ingelstrom, P.: Computational Electromagnetics. Springer, New York, 2005.
- [8] Bossavit, A.: Most General “Non-Local” Boundary Conditions for the Maxwell Equation in a Bounded Region. In ISEF’99, Proceedings of the 9th International Symposium on Electromagnetic Fields in Electrical Engineering. COMPEL 19 (2000), pp. 239–245.
- [12] Brandt, A., and Yavneh, I.: Inadequacy of First-Order Upwind Difference Schemes for Some Recirculating Flows. J. Comput. Phys. 93 (1991), pp. 128–143.
- [13] Brenner, S.C., and Scott, L.R.: The Mathematical Theory of Finite Element Methods (Third Edition). Springer, New York, 2008.
- [14] Brezis, H.: Functional Analysis, Sobolev Spaces and Partial Differential Equations. Springer, New York, 2011.
- [15] Bridson, R., and Tang, W.: Refining an Approximate Inverse. J. Comput. Appl. Math. 123 (2000), pp. 293–306.
- [16] Bronstein, M.M., Bronstein, A.M., Kimmel, R., and Yavneh, I.: Multigrid Multidimensional Scaling. Numer. Linear Algebra Appl. (2006), pp. 149–171.
- [17] Cai, Z., Lee, C.-O., Manteuffel, T.A., and McCormick, S.F.: First-Order System Least Squares for the Stokes and Linear Elasticity Equations: Further Results. SIAM J. Sci. Comput. 21 (2000), pp. 1728–1739.
- [18] Caselles, V., Kimmel, R., and Sapiro, G.: Geometric Active Contours for Image Segmentation. In Handbook of Image and Video Processing (Second Edition). Elsevier Academic Press, Boston, 2005, pp. 613–627.
- [19] Chan, T.F., and Vanek, P.: Detection of Strong Coupling in Algebraic Multigrid Solvers. In Multigrid Methods VI, Vol. 14. Springer-Verlag, Berlin, 2000, pp. 11–23.
- [20] Chang, Q., and Huang, Z.: Efficient Algebraic Multigrid Algorithms and Their Convergence. SIAM J. Sci. Comput. 24 (2002), pp. 597–618.
- [21] Costabel, M.: A Coercive Bilinear Form for Maxwell’s Equations. J. Math. Anal. Appl. 157 (1991), pp. 527–541.
- [22] Courant, R., and John, F.: Introduction to Calculus and Analysis (Vols. 1 and 2). Springer, New York, 1998–1999.
- [23] Dahlquist, G.: Numerical Methods. Dover Publications, Mineola, NY, 2003.
- [24] D’Azevedo, E.F., Romine, C.H., and Donato, J.H.: Coefficient Adaptive Triangulation for Strongly Anisotropic Problems. In Preproceedings of the 5th Copper Mountain Conference on Iterative Methods, Manteuffel, T.A. and McCormick, S.F. (eds.). 1998. Available online at www.mgnet.org
- [25] Dench, D., and Prior, B.: Introduction to C++. Chapman & Hall, London, 1994.
- [26] Dendy, J.E.: Black Box Multigrid for Nonsymmetric Problems. Appl. Math. Comput. 13 (1983), pp. 261–283.
- [27] Dendy, J.E.: Semicoarsening Multigrid for Systems. Electron. Trans. Numer. Anal. 6 (1997), pp. 97–105.
- [28] Douglas, C.C.: Cache Based Multigrid Algorithms. In MGnet Virtual Proceedings of the 7th Copper Mountain Conference on Multigrid Methods, 1997. Available online at www.mgnet.org.
- [29] Elman, H.C., Ernst, O.G., and O'Leary, D.P.: A Multigrid Method Enhanced by Krylov Subspace Iteration for Discrete Helmholtz Equations. SIAM J. Sci. Comput. 23 (2001), pp. 1291–1315.
- [30] Evans, D.J.: Preconditioning Methods. Gordon and Breach, New York, 1983.
- [31] Fibich, G., Ilan, B., and Tsynkov, S.: Computation of Nonlinear Backscattering Using a High-Order Numerical Method. J. Sci. Comput. 17 (2002), pp. 351–364.
- [32] Fibich, G., and Tsynkov, S.: High Order Two-Way Artificial Boundary Conditions for Nonlinear Wave Propagation with Backscattering. J. Comput. Phys. 171 (2001), pp. 632–677.
- [33] Fox, G.C.: Solving Problems on Concurrent Processors. Prentice-Hall, Englewood Cliffs, NJ, 1988.
- [34] Freund, R.W.: A Transpose-Free Quasi-Minimal Residual Algorithm for Non-Hermitian Linear Systems. SIAM J. Sci. Comput. 14 (1993), pp. 470–482.
- [35] Gottlieb, A., and Almasi, G.S.: Highly Parallel Computing. Benjamin Cummings, Redwood City, CA, 1989.
- [36] Gustafsson, I.: On Modified Incomplete Factorization Methods. In Numerical Integration of Differential Equations and Large Linear Systems, Lecture Notes in Mathematics, 968, Springer, Berlin, 1982, pp. 334–351.
- [37] Haber, E., Ascher, U., and Oldenburg, D.W.: Inversion of 3D Electromagnetic Data in Frequency and Time Domain Using an Inexact All-at-Once Approach. Geophys. 69 (2004), pp. 1216–1228.
- [38] Hansbo, P., and Rylander, T.: A Linear Nonconforming Finite Element Method for Maxwell's Equations in Two Dimensions. Chalmers University of Technology, University of Gothenburg, Sweden, 2008.
- [39] Hartman, P.: Ordinary Differential Equations (Second Edition). Birkhäuser, New York, 1982.
- [40] Hesthaven, J., and Warburton, T.: Nodal Discontinuous Galerkin Methods: Algorithms, Analysis and Applications. Springer, New York, 2008.
- [41] Huang, H., and Ascher, U.: Fast Denoising of Surface Meshes with Intrinsic Texture (preprint). Available online at www.cs.ubc.ca/nascher/papers/huas.pdf.
- [42] Klawonn, A., and Widlund, O.B.: A Domain Decomposition Method with Lagrange Multipliers and Inexact Solvers for Linear Elasticity. SIAM J. Sci. Comput. 22 (2000), pp. 1199–1219.
- [43] Kraus, J.K., and Schicho, J.: Algebraic Multigrid Based on Computational Molecules, I: Scalar Elliptic Problems. RICAM report, Austrian Academy of Sciences, Linz, Austria, March 2005.
- [44] Layton, W., Lee, H.K., and Peterson, J.: Numerical Solution of the Stationary Navier–Stokes Equations Using a Multilevel Finite Element Method. SIAM J. Sci. Comput. 20 (1998), pp. 1–12.
- [45] Lee, B., Manteuffel, T.A., McCormick, S.F., and Ruge, J.: First-Order System Least-Squares for the Helmholtz Equation. SIAM J. Sci. Comput. 21 (2000), pp. 1927–1949.
- [46] Li, J.C., and Chen, Y.T.: Computational Partial Differential Equations Using MATLAB. Chapman & Hall/CRC, Boca Raton, FL, 2009.
- [47] Mavriplis, D.J.: Directional Coarsening and Smoothing for Anisotropic Navier–Stokes Problems. In MGnet Virtual Proceedings of the 7th Copper Mountain Conference on Multigrid Methods, 1997. Available online at www.mgnet.org.
- [48] McCormick, S. F., and Quinlan, D.: Asynchronous Multilevel Adaptive Methods for Solving Partial Differential Equations: Performance Results. Parallel Comput. 12 (1990), pp. 145–156.
- [49] Meijerink, J.A., and Van der Vorst, H.A.: An Iterative Solution Method for Linear Systems of which the Coefficient Matrix is a Symmetric M-matrix. Math. Comp. 31 (1977), pp. 148–162.
- [50] Michelson, D.: Bunsen Flames as Steady Solutions of the Kuramoto–Sivashinsky Equation. SIAM J. Math. Anal. 23 (1992), pp. 364–386.
- [51] Miller, G. L.: Riemann's Hypothesis and Tests for Primality. J. Comput. System Sci. 13 (1976), pp. 300–317.
- [52] Mitchell, W.F.: Optimal Multilevel Iterative Methods for Adaptive Grids. SIAM J. Sci. Stat. Comput. 13 (1992), pp. 146–167.
- [53] Monk, P.: Finite Element Methods for Maxwell's Equations. Oxford University Press, New York, 2003.
- [54] Morton, K.W.: Numerical Solution of Convection-Diffusion Problems. Applied Mathematics and Mathematical Computation, 12. Chapman & Hall, London, 1996.
- [55] Munson, D.C.: A Note on Lena. IEEE Trans. Image Process. 5 (1996).
- [56] Ortega, J.M.: Introduction to Parallel and Vector Solution of Linear Systems. Plenum Press, New York, 1988.
- [57] Perona, P., and Malik, J.: Scale-Space and Edge Detection Using Anisotropic Diffusion. IEEE Trans. Pattern Anal. 12 (1990), pp. 629–639.
- [58] Rabin, M.O.: Probabilistic Algorithm for Testing Primality. J. Number Theory 12 (1980), pp. 128–138.
- [59] Rivest, R., Shamir, A., and Adleman, L.: A Method for Obtaining Digital Signatures and Public-Key Cryptosystems. Comm. ACM 21 (1978), pp. 120–126.

