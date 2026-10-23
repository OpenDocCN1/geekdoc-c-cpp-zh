
Table 1. The minimizers, listed in a sequential order, found by one ID realization for n = 3 and n = 4 respectively.

| i | n = 3 | n = 4 |
|---|---|---|
| 1 | (−6.96, 5, −7) | (−6.96, 8.99, 8.99, 4.99) |
| 2 | (1, 1, 1) | (1, 1, 1, 1) |
| 3 | (1, 1, 1) | (1, 1, 1, 1) |
| 4 | (9, 5, −3) | (−2.98, −2.98, −2.98, −2.98) |
| 5 | (−10.92, −7, 5) | (−8.96, −2.99, 1, 1) |
| 6 | (−3, 1, 1) | (−2.98, 4.98, −2.98, 1) |
| 7 | (−3, 1, 1) | (−6.96, 1, 1, 1) |
| 8 | (1, 1, 1) | (1, 1, 1, 1) |
| 9 | (9, −7, 1) | (1, 1, 1, 1) |
| 10 | (5, 9, 5) | (1, 1, 1, 1) |

We also compare the ID method with the CDD method studied in [17]. We run both methods on Problem 3 for 100 independent realizations with the final stopping time T = 300 respectively. In each realization, we use the same initial point and Brownian motion path for both methods. We record the number of visits that the ID and the CDD reach a small neighborhood of the unique global minimizer respectively. Our experiments show that the average number of visits in the 100 realizations for the ID method is 7.5. In contrast, it is 0 for the CDD method, which indicates that it has not reached the small neighborhood of the global minimum in most of the realizations because of the slow decay in the cooling rate. This is not surprising since the convergence time for the CDD method is exponentially long, while the convergence time at the non-diffusion step for the ID method is short because the gradient flow drives the trajectories to a small neighborhood of the minimizers.

We also compare the first time of reaching a small neighborhood of the global minimizer for Problem 3 by both methods. The first times that the ID method and the CDD method enter a square neighborhood of the global minimizer with diameters ε = 0.001 and ε = 0.0001 are recorded respectively for 30 independent realizations. Figure 6 shows the log plot of the first arriving time for ε = 0.001. The ID method takes less time to reach the global minimizer than the CDD method does in most realizations. Figure 7 shows the log plot of the first arriving time for a much smaller neighborhood with ε = 0.0001. The ID method takes less time to hit the global minimizer than the CDD method does for all realizations except one, and the time difference is significantly large.

![](img/039e7d3c23390584a66737067db8b75b_489_0.png)

Fig. 6. The log plot of the first time to enter a square neighborhood of the global minimizer with diameter ε = 0.001 by ID and CDD for 30 independent realizations.

![](img/039e7d3c23390584a66737067db8b75b_489_1.png)

Fig. 7. The log plot of the first time to enter a square neighborhood of the global minimizer with diameter ε = 0.0001 by ID and CDD for 30 independent realizations.

## Acknowledgment

The authors would like to thank Luca Dieci, Wen Huang, Liangda Huang and Kening Lu for helpful comments and discussions in this project. The project is partially supported by NSF Faculty Early Career Development (CAREER) Award DMS-0645266 and DMS-1042998.

## References

- [1] F. Aluffi-Pentini, V. Parisi and F. Zirilli, Global optimization and stochastic differential equations, J. Optimiz. Theory App., 47(1), 1–16, 1985.
- [2] A. Arnold, P. Markowich, G. Toscani and A. Unterreiter, On convex Sobolev inequalities and the rate of convergence to equilibrium for Fokker-Planck type equations, Comm. in PDEs, 26(1 & 2), (2001) pp. 43–100.
- [3] L. Arnold, Random Dynamical Systems, Springer-Verlag, Berlin, 1998.
- [4] Bagirov, A. M., and A. M. Rubinov, Cutting angle method and a local search, Journal of Global Optimization, 27 (2003), pp. 193–213.
- [5] A. Bagirov, A. Rubinov and J. Zhang, Local optimization method with global multidimensional search, J. of Global Optimization, 32 (2005), pp. 161–179.
- [6] A. M. Bagirov, A. M. Rubinov, and J. Zhang, A multidimensional descent method for global optimization, Optimization, Vol. 58, No. 5, 2009, pp. 611–625.
- [7] G. Bao and P. J. Li, Inverse medium scattering for the Helmholtz equation at fixed frequency, Inverse Problems, 21 (2005), pp. 1621–1641.
- [8] G. Bao and P. J. Li, Inverse medium scattering problems for electromagnetic waves, SIAM J. Appl. Math., 65 (2005), pp. 2049–2066.
- [9] Battiti, Roberto; Mauro Brunato; Franco Mascia, Reactive Search and Intelligent Optimization, Springer-Verlag, 2008.
- [10] E. Beale, Introduction to Optimization, Wiley, Chichester, 1988.
- [11] S. Boyd and L. Vandenberghe, Convex Optimization, Cambridge University Press, 2004.
- [12] V. Černý, A thermodynamical approach to the travelling salesman problem: an efficient simulation algorithm. J. Optimiz. Theory App., 45(1), 41–51, 1985.
- [13] T.-S. Chiang, C.-R. Hwang and S.-J. Sheu, Diffusion for global optimization in R^n, SIAM J. Control and Optim., 25(3), 737–753, 1986.
- [14] S.-N. Chow, W. P. Li, Z. X. Liu and H. M. Zhou, A natural order in dynamical systems based on Conley-Markov matrices, accepted by J. of Differential Equations.
- [15] S.-N. Chow, J. Lu and H. M. Zhou, A fast algorithm for finding shortest path by solving initial value ODEs, preprint.
- [16] S.-N. Chow, T. S. Yang and H. M. Zhou, Global optimization by intermittent diffusion, UCLA CAM report, 2009.
- [17] S. Geman and C.-R. Hwang, Diffusion for global optimization, SIAM J. Control and Optim., 24(5), 1031–1043, 1986.
- [18] B. Gidas, Metropolis-type Monte Carlo simulation algorithms and simulated annealing, in: J.L. Snell (Ed.), Topics in Contemporary Probability and Its Applications, in: Probability and Stochastics Series, CRC Press, Boca Raton, FL, 1995, pp. 159–232.
- [19] I. V. Girsanov, On transforming a certain class of stochastic processes by absolutely continuous substitution of measures, Theory Probab. Appl., 5, No. 3 (1960), pp. 285–301.
- [20] Jack K. Hale, Asymptotic behavior of dissipative systems (Mathematical Surveys and Monographs, 25), American Mathematical Society.
- [21] J. Holland, Genetic algorithms and the optimal allocation of trials, SIAM J. Computing 2 (1973), pp. 88–105.
- [22] R. Holley, S. Kusuoka and D. Stroock, Asymptotics of the spectral gap with applications to the theory of simulated annealing, J. Func. Anal., 83(2), pp. 333–347, 1989.
- [23] R. Holley and D. Stroock, Logarithmic Sobolev inequalities and stochastic Ising models, J. Stat. Phys., 46, 5–6, 1159–1194, 1987.
- [24] R. Holley and D. Stroock, Simulated annealing via Sobolev inequalities, Commun. Math. Phys., 115(4), 553–569, 1988.
- [25] R. Horst and P.M. Pardalos (eds.), Handbook of Global Optimization, Kluwer, Dordrecht, 1995.
- [26] L. Ingber, Very fast simulated re-annealing. Math. Comput. Modelling, 12(8), 967–973, 1989.
- [27] C. T. Kelley, Iterative Methods for Optimization, SIAM, 1999.
- [28] S. Kirkpatrick, C. D. Gelatt, Jr. and M. P. Vecchi, Optimization by simulated annealing, Science, Vol. 220 No. 4598, pp. 671–680, 1983.
- [29] A.H. Land and A.G. Doig, An automated method for solving discrete programming problems, Econometrica, 28 (1960), 497–520.
- [30] A. Levy and A. Montalvo, The tunneling algorithm for the global minimization of functions, SIAM J. of Scientific and Statistical Computing, 6, 1985, pp. 15–29.
- [31] J.D. Little, K.C. Murty, D.W. Sweeney and C. Karel, An algorithm for the travelling salesman problem, Operations Research, 11 (1963), pp. 972–989.
- [32] H. Lourenço, O. C. Martin and T. Stützle, Iterated Local Search, Handbook of Metaheuristics, Springer, 2003, pp. 320–353.
- [33] P. Markowich and C. Villani, On the trend to equilibrium for the Fokker-Planck equation: an interplay between physics and functional analysis, Mat. Contemp., 19 (2000), pp. 1–29.
- [34] N. Metropolis, A. W. Rosenbluth, M. N. Rosenbluth, A. H. Teller and E. Teller, Equations of state calculations by fast computing machines, J. Chem. Phys., Vol. 21, 1953, pp. 1087–1091.
- [35] J. Mockus, Multiextremal problems in design, Ph.D. Thesis, Nauka, 1966.
- [36] A. Neumaier, Complete search in continuous global optimization and constraint satisfaction, Acta Numerica (A. Iserles, ed.), Cambridge University Press, 2004.
