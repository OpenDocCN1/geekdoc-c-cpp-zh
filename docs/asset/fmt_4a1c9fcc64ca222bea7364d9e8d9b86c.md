
在本章中，我们提出了一种求解非线性方程的带记忆的两步迭代方法族。由于我们的目标是在不增加额外计算的情况下构造更高阶收敛的方法，我们使用了由四阶方法中牛顿插值多项式设计的自校正参数的两种近似，以在不进行任何额外计算的情况下实现更高阶的收敛。新带记忆迭代方法的 R-阶收敛从 4 提高到 6 和 7。数值结果已给出以证实理论结果的有效性。

#### 表 6.4

所提方法与其他方案的评估函数和效率指数比较

$f_1(x)=x\log(1+x\sin(x))+e^{-1+x^2\cos(x)}\sin(x)$，$\alpha=0, x_0=0.3$

| 无记忆方法 | EF | Iter | COC | EI | 带记忆方法 | EF | Iter | COC | EI |
|---|---|---|---|---|---|---|---|---|---|
| AM | 3 | 5 | 3.0000 | 1.44225 | TrM, $\lambda_0=0.1$ | 2 | 4 | 2.4282 | 1.55827 |
| NM | 2 | 7 | 2.0000 | 1.41421 | SecM, $x_1=0.6$ | 2 | 15 | 1.6181 | 1.61808 |
| MM | 3 | 5 | 4.0000 | 1.58740 | WM, $\lambda_0=1$ | 3 | 5 | 4.2361 | 1.61803 |
| CNM, $\alpha_0=\gamma_0=A_0=1$ | 4 | 3 | 8.0000 | 1.68179 | PIDM $\beta_0=0.1$ | 3 | 5 | 4.4513 | 1.64499 |
| GKM | 5 | 3 | 16.0000 | 1.74110 | DPPM, $\gamma_0=-0.1$ | 4 | 3 | 1.0000 | 1.00000 |
| RWBM, $\beta_0=1$ | 3 | 4 | 4.0000 | 1.58740 | TKM, $\gamma_0=\lambda_0=0.1$ | 3 | 5 | 7.0000 | 1.91293 |

$f_2(x)=\sin(5x)^x-2,$ $\alpha=1.36, x_1=1$

| 无记忆方法 | EF | Iter | COC | EI | 带记忆方法 | EF | Iter | COC | EI |
|---|---|---|---|---|---|---|---|---|---|
| AM | 3 | 1000 | 1.0000 | 1.00000 | TrM, $\lambda_0=0.1$ | 2 | 5 | 0.0000 | 0.00000 |
| NM | 2 | 15 | 2.0000 | 1.41421 | SecM, $x_1=1.2$ | 2 | 17 | 1.6181 | 1.61808 |
| MM | 3 | 4 | 4.0000 | 1.58740 | WM, $\lambda_0=0.1$ | 3 | 5 | 4.2361 | 1.61803 |
| CNM, $\alpha_0=\gamma_0=A_0=1$ | 4 | 6 | 8.0000 | 1.68179 | PIDM $\beta_0=0.1$ | 3 | 5 | 4.4314 | 1.64253 |
| GKM | 5 | 3 | 0.000 | 0.00000 | DPPM, $\gamma_0=-0.1$ | 4 | 3 | 1.0000 | 1.00000 |
| RWBM, $\beta_0=1$ | 3 | 4 | 0.0000 | 0.00000 | TKM, $\gamma_0=\lambda_0=0.1$ | 3 | 4 | 7.0000 | 1.91293 |

$f_3(x)=1+\dfrac{1}{x^4}-\dfrac{1}{x}-x^2,$ $\alpha=1, x_0=1.4$

| 无记忆方法 | EF | Iter | COC | EI | 带记忆方法 | EF | Iter | COC | EI |
|---|---|---|---|---|---|---|---|---|---|
| AM | 3 | 6 | 3.0000 | 1.44225 | TrM, $\lambda_0=0.1$ | 2 | 4 | 2.4062 | 1.55120 |
| NM | 2 | 5 | 2.0000 | 1.41421 | SecM, $x_1=1.5$ | 2 | 16 | 1.6181 | 1.61808 |
| MM | 3 | 4 | 4.0000 | 1.58740 | WM, $\lambda_0=1$ | 3 | 5 | 4.2361 | 1.61804 |
| CNM, $\alpha_0=\gamma_0=A_0=1$ | 4 | 3 | 8.0000 | 1.68179 | PIDM $\beta_0=0.1$ | 3 | 5 | 4.4661 | 1.64681 |
| GKM | 5 | 3 | 16.0000 | 1.74110 | DPPM, $\gamma_0=-0.1$ | 4 | 3 | 10.0000 | 1.77828 |
| RWBM, $\beta_0=1$ | 3 | 4 | 4.0000 | 1.58740 | TKM, $\gamma_0=\lambda_0=0.1$ | 3 | 3 | 7.0000 | 1.91293 |

(续)

#### 表 6.4 （续）

所提方法与其他方案的评估函数和效率指数比较

$f_4(x) = (x-2)(2+x^{10}) + x + 2e^{-5x}$,  $\alpha=2, \gamma_0=2.3$

| 无记忆方法 | EF | Iter | COC | EI | 带记忆方法 | EF | Iter | COC | EI |
|---|---|---|---|---|---|---|---|---|---|
| AM | 3 | 1500 | 3.0000 | 1.44225 | TrM, $\lambda_0=0.1$ | 2 | 4 | 2.4681 | 1.57100 |
| NM | 2 | 5 | 2.0000 | 1.41421 | SecM, $x_i=1.8$ | 2 | 17 | 1.6181 | 1.61808 |
| MM | 3 | 4 | 4.0000 | 1.58740 | WM, $\gamma_0=1$ | 3 | 6 | 4.2361 | 1.61803 |
| CNM, $\alpha_0=\gamma_0=A_0=1$ | 4 | 5 | 8.0000 | 1.68179 | PIDM $\beta_0=0.1$ | 3 | 4 | 4.3019 | 1.62637 |
| GKM | 5 | 3 | 16.0000 | 1.74110 | DPPM, $\gamma_0=-0.1$ | 4 | 3 | 1.0000 | 1.00000 |
| RWBM, $\beta_0=1$ | 3 | 4 | 4.0000 | 1.58740 | TKM, $\gamma_0=0.1$ | 3 | 4 | 7.0000 | 1.91293 |

$f_5(x)=e^{-x^3-x} - \cos(x^2-1)+x^3+1$, $\alpha=-1, x_0=-1.3$

| 无记忆方法 | EF | Iter | COC | EI | 带记忆方法 | EF | Iter | COC | EI |
|---|---|---|---|---|---|---|---|---|---|
| AM | 3 | 5 | 3.0000 | 1.44225 | TrM, $\lambda_0=0.1$ | 2 | 4 | 2.4520 | 1.56549 |
| NM | 2 | 5 | 2.0000 | 1.41421 | SecM, $x_i=-1.6$ | 2 | 18 | 1.6181 | 1.61808 |
| MM | 3 | 4 | 4.0000 | 1.58740 | WM, $\gamma_0=1$ | 3 | 5 | 4.2361 | 1.61803 |
| CNM, $\alpha_0=\gamma_0=A_0=1$ | 4 | 3 | 8.0000 | 1.68179 | PIDM $\beta_0=-0.1$ | 3 | 4 | 4.4517 | 1.64504 |
| GKM | 5 | 3 | 16.0000 | 1.74110 | DPPM, $\gamma_0=-0.1$ | 4 | 4 | 1.0000 | 1.00000 |
| RWBM, $\beta_0=1$ | 3 | 4 | 4.0000 | 1.58740 | TKM, $\gamma_0=0.1$ | 3 | 4 | 7.0000 | 1.91293 |

## 参考文献

- Abbasbandy, S. 2006. Modified homotopy perturbation method for nonlinear equations and comparison with Adomian decomposition method. Applied Mathematics and Computation 172:431–438.
- Chun, C., and Neta, B. 2014. An analysis of a new family of eighth-order optimal methods. Applied Mathematics and Computation 245:86–107.
- Cordero, A., Hueso, J.L., Martinez, E., and Torregrosa, J.R. 2013. A new technique to obtain derivative-free optimal iterative methods for solving nonlinear equations. Journal of Computational and Applied Mathematics 252:95–102.
- Cordero, A., Lotfi, T., Bakhtiari, P., and Torregrosa, J.R. 2014. An efficient two-parametric family with memory for nonlinear equations. Numerical Algorithms 68(2):323–335.
- Cordero, A., Lotfi, T., Khoshandi, A., and Torregrosa, J.R. 2015. An efficient Steffensen-like iterative method with memory. Bulletin mathematique de la Societe des Sciences Mathematiques de Roumanie Nouvelle Serie 58(106):49–58.
- Cordero, A., Lotfi, T., Torregrosa, J.R., Assari, P., and Mahdiani, K. 2016. Some new bi-accelarator two-point methods for solving nonlinear equations. Computational and Applied Mathematics 35(1):251–267.
- Dehghan, M., and Hajarian, M. 2010. New iterative method for solving non-linear equations with fourth-order convergence. International Journal of Computer Mathematics 87(4):834–839.
- Dzunic, J., Petkovic, M.S., and Petkovic, L.D. 2012. Three-point methods with and without memory for solving nonlinear equations. Applied Mathematics and Computation 218:4917–4927.
- Geum, Y.H., and Kim, Y.I. 2011. A biparametric family optimally convergent sixteenth-order multipoint methods with their fourth-step weighting function as a sum of a rational and a generic two-variable function. Journal of Computational and Applied Mathematics 235:3178–3188.
- Guo, Q.W., and Qian, Y.H. 2015. New efficient optimal derivative-free method for solving nonlinear equations. International Journal of Mathematics and Computational Science 1(3):102–110.
- Hansen, E., and Patrick, M. 1977. A family of root finding methods. Numerische Mathematik 27:257–269.
- Jarratt, P. 1966. Some fourth order multipoint methods for solving equations. Mathematics of Computation 20:434–437.
- Kansal, M., Kanwar, V., and Bhatia, S. 2016. Efficient derivative-free variants of Hansen-Patrick's family with memory for solving nonlinear equations. Numerical Algorithms 73:1017–1036.
- Kou, J., and Li, Y. 2007. The improvements of Chebyshev-Halley methods with fifth-order convergence. Applied Mathematics and Computation 188:143–147.
- Kung, H.T., and Traub, J.F. 1974. Optimal order of one-point and multipoint iteration. Journal of the ACM (JACM) 21:634–651.
- Li, X., Mu, C., Ma, J., and Wang, C. 2010. Sixteenth-order method for nonlinear equations. Applied Mathematics and Computation 215(10):3754–3758.
- Lotfi, T., Mahdiani, K., Noori, Z., Khaksar Haghani, F., and Shateyi, S. 2014. On a new three-step class of methods and its acceleration for nonlinear equations. The Scientific World Journal 2014:134673.
- Maheshwari, A.K. 2009. A fourth order iterative method for solving nonlinear equations. Applied Mathematics and Computation 211:383–391.
- Ortega, J.M., and Rheinboldt, W.C. 1970. Iterative solutions of nonlinear equations in several variables, Academic Press, New York.
- Ostrowski, A.M. 1960. Solution of equations and systems of equations, Academic Press, New York.
- Petkovic, M.S., Dzunic, J., and Neta, B. 2011. Interpolatory multipoint methods with memory for solving nonlinear equations. Applied Mathematics and Computation 218:2533–2541.
- Petkovic, M.S., Neta, B., Petkovic, L.D., and Dzunic, J. 2013. Multipoint methods for solving nonlinear equations, Elsevier, Amsterdam.
- Petkovic, M.S., Ilic, S., and Dzunic, J. 2010. Derivative free two-point methods with and without memory for solving nonlinear equations. Applied Mathematics and Computation 217:1887–1895.
- Ren, H., Wu, Q., and Bi, W. 2009. A class of two-step Steffensen type methods with fourth-order convergence. Applied Mathematics and Computation 209:206–210.
