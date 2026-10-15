
Table 6.2: Control policies for the best 5 local optima

| Local optimum | 1 (global) | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| Performance index | 10.0942 | 10.0527 | 10.0395 | 9.9047 | 9.8805 |
| u(0) | 0.6661 | 0.6651 | 0.6671 | 0.6637 | 0.9000 |
| u(1) | 0.6734 | 0.6721 | 0.6744 | 0.9000 | 0.6724 |
| u(2) | 0.6764 | 0.9000 | 0.6777 | 0.9000 | 0.6755 |
| u(3) | 0.9000 | 0.9000 | 0.6796 | 0.9000 | 0.9000 |
| u(4) | 0.9000 | 0.9000 | 0.9000 | 0.9000 | 0.9000 |
| u(5) | 0.9000 | 0.9000 | 0.9000 | 0.9000 | 0.9000 |
| u(6) | 0.9000 | 0.9000 | 0.9000 | 0.9000 | 0.9000 |
| u(7) | 0.9000 | 0.9000 | 0.9000 | 0.9000 | 0.9000 |
| u(8) | 0.9000 | 0.9000 | 0.9000 | 0.9000 | 0.9000 |
| u(9) | 0.9000 | 0.9000 | 0.9000 | 0.9000 | 0.9000 |

Table 6.3: Value of the performance index I with N = 1, and M = 3, showing the effects of the region contraction factor γ and the initial region size r^(0); the number of iterations required to get the global optimum is shown in parentheses

| Reduction factor | Initial region size r^(0) | | | |
|---|---|---|---|---|
| γ | 0.27 | 0.30 | 0.40 | 0.50 |
| 0.70 | 10.0527 | 10.0942 (18) | 10.0942 (19) | 10.0942 (20) |
| 0.72 | 10.0527 | 10.0942 (20) | 10.0942 (21) | 10.0527 |
| 0.74 | 10.0942 (22) | 10.0942 (22) | 10.0942 (23) | 10.0942 (24) |
| 0.76 | 10.0942 (23) | 10.0942 (24) | 10.0942 (25) | 10.0942 (26) |
| 0.78 | 10.0942 (26) | 10.0942 (26) | 10.0942 (28) | 10.0942 (29) |
| 0.80 | 10.0942 (29) | 10.0942 (29) | 10.0942 (31) | 10.0942 (32) |
| 0.82 | 10.0942 (32) | 10.0942 (32) | 10.0942 (34) | 10.0942 (36) |
| 0.84 | 10.0942 (36) | 10.0942 (38) | 10.0942 (39) | 10.0942 (40) |
| 0.86 | 10.0941 | 10.0941 | 10.0941 | 10.0941 |
| 0.88 | 10.0940 | 10.0940 | 10.0939 | 10.0937 |
| 0.90 | 10.0933 | 10.0930 | 10.0925 | 10.0913 |

## Table 6.4: Value of the performance index $I$ with $N = 1$, and $M = 9$, showing the effects of the region contraction factor $\gamma$ and the initial region size $r^{(0)}$; the number of iterations required to get the global optimum is shown in parentheses

| Reduction factor | Initial region size $r^{(0)}$ | | | |
|---|---|---|---|---|
| $\gamma$ | 0.27 | 0.30 | 0.40 | 0.50 |
| 0.70 | 10.0395 | **10.0942** (15) | 10.0527 | **10.0942** (17) |
| 0.72 | 10.0395 | **10.0942** (16) | **10.0942** (17) | 10.0527 |
| 0.74 | 10.0395 | **10.0942** (17) | **10.0942** (18) | **10.0942** (19) |
| 0.76 | **10.0942** (19) | **10.0942** (19) | **10.0942** (20) | **10.0942** (21) |
| 0.78 | **10.0942** (21) | **10.0942** (21) | **10.0942** (22) | **10.0942** (23) |
| 0.80 | **10.0942** (22) | **10.0942** (23) | **10.0942** (24) | **10.0942** (25) |
| 0.82 | **10.0942** (25) | **10.0942** (26) | **10.0942** (27) | **10.0942** (28) |
| 0.84 | **10.0942** (28) | **10.0942** (29) | **10.0942** (30) | **10.0942** (32) |
| 0.86 | **10.0942** (33) | **10.0942** (34) | **10.0942** (36) | **10.0942** (37) |
| 0.88 | **10.0942** (39) | **10.0942** (39) | 10.0941 | 10.0941 |
| 0.90 | 10.0941 | 10.0941 | 10.0940 | 10.0940 |

maximum of 40 iterations were allowed. As can be seen, the number of iterations to reach the global optimum is reduced when using $M = 9$, rather than $M = 3$. In each case, the global optimum was obtained in almost every case when the initial region size was chosen greater than 0.27. Of the 44 runs, the local optimum was obtained 3 times with the use of $M = 3$. With $M = 9$, local optima were obtained 5 times in the 44 runs. Therefore, the use of a larger number of allowable values for control does not necessarily improve the chances of avoiding local optima.

As expected, with $M = 9$ we can have a larger value for the region contraction factor $\gamma$ and still get convergence to the global optimum to 6 figures within 40 iterations. However, it must be remembered that the use of $M = 9$ instead of $M = 3$ requires three times as much computational effort per iteration. Further results on this system are given by Luus and Bojkov [6], who showed, in addition, that instead of choosing the candidates for control in uniform fashion, the random choice gives essentially the same results. The computation time on a PentiumII/350 for 20 iterations with $M = 3$ was 6 s.

### 6.2.2 Photochemical CSTR

Let us consider the photochemical continuous stirred tank reactor (CSTR) used by Lapidus and Luus [5], which we considered in Chapter 5 to examine the effect of the number of grid points. Here, we consider the reactor with 4 control variables:

$$
\begin{aligned}
\frac{dx_1}{dt} &= u_4-qx_1-17.6x_1x_2-23x_1x_6u_3 \tag{6.15}\\
\frac{dx_2}{dt} &= u_1-qx_2-17.6x_1x_2-146x_2x_3 \tag{6.16}\\
\frac{dx_3}{dt} &= -u_2-qx_3-73x_2x_3 \tag{6.17}\\
\frac{dx_4}{dt} &= -qx_4+35.2x_1x_2-51.3x_4x_5 \tag{6.18}\\
\frac{dx_5}{dt} &= -qx_5+219x_2x_3-51.3x_4x_5 \tag{6.19}\\
\frac{dx_6}{dt} &= -qx_6+102.6x_4x_5-23x_1x_6u_3 \tag{6.20}\\
\frac{dx_7}{dt} &= -qx_7+46x_1x_6u_3 \tag{6.21}\\
\frac{dx_8}{dt} &= 5.8(qx_1-q_1)-3.7u_1-4.1u_2+q(23x_4+11x_5+28x_6+35x_7)-5u_3^2-0.099 \tag{6.22}
\end{aligned}
$$

where the total inlet flow rate is given by $q=u_1+u_2+u_4$. The last differential equation is introduced to give the performance index. The problem is to maximize

$$
I=x_8(t_f) \tag{6.23}
$$

where the final time $t_f$ is specified as 0.2. The initial state is specified as $\mathbf{x}(0)=[0.1883\ \ 0.2507\ \ 0.0467\ \ 0.0899\ \ 0.1804\ \ 0.1394\ \ 0.1046\ \ 0]^T$. The control variables are constrained by

+   $$\begin{aligned}
+   0\leq u_1\leq 20 &&\tag{6.24}\\
+   0\leq u_2\leq 6 &&\tag{6.25}\\
+   0\leq u_3\leq 4 &&\tag{6.26}\\
+   0\leq u_4\leq 20 &&\tag{6.27}
+   \end{aligned}$$

In Chapter 5 we saw that with $P=11$ time stages of equal length, over which piecewise constant control was used, the maximum value for the performance index was found to be 21.75722. Here we wish to illustrate how the number of grid points affects our capability of getting this optimum. As we did in Chapter 5, we choose as initial values for the control to be in the middle of the allowable region, i.e., $u_1^{(0)}=10$, $u_2^{(0)}=3$, $u_3^{(0)}=2$, and $u_4^{(0)}=10$, and let the initial region sizes be $r_1^{(0)}=10$, $r_2^{(0)}=3$, $r_3^{(0)}=2$, and $r_4^{(0)}=10$. By choosing $R=81$ allowable values at random inside the allowable region that was contracted by the reduction factor $\gamma$ after every iteration, the problem was solved for different values of $\gamma$ and the number of grid points $N$. For each case 100 iterations were allowed. The results are given in Table 6.5. It is clear that there is a range for the region contraction factor $0.90\leq\gamma\leq0.96$

## Table 6.5: Effect of the number of grid points on convergence with R = 81; the numbers in the parentheses give the number of iterations required for convergence

|  | Number of grid points at each time stage | | | |
|---|---|---|---|---|
| γ | N = 1 | N = 5 | N = 11 | N = 27 |
| 0.80 | 21.4649 | 21.5476 | 21.6894 | 21.6575 |
| 0.81 | 21.6019 | 21.6621 | 21.5686 | 21.6263 |
| 0.82 | 21.6145 | 21.6624 | 21.6782 | 21.5847 |
| 0.83 | 21.6222 | 21.6729 | 21.7415 | 21.7272 |
| 0.84 | 21.6350 | 21.7276 | 21.6931 | 21.7547 |
| 0.85 | 21.6286 | 21.7370 | 21.6141 | 21.7360 |
| 0.86 | 21.6293 | 21.7085 | 21.4995 | 21.7353 |
| 0.87 | 21.6427 | 21.7522 | 21.7331 | 21.7329 |
| 0.88 | 21.6556 | 21.7572 (32) | 21.7572 (34) | 21.7572 (30) |
| 0.89 | 21.6603 | 21.7572 (37) | 21.7072 | 21.7572 (32) |
| 0.90 | 21.7506 | 21.7572 (39) | 21.7572 (39) | 21.7572 (32) |
| 0.91 | 21.7572 (61) | 21.7572 (44) | 21.7572 (38) | 21.7572 (39) |
| 0.92 | 21.7572 (53) | 21.7572 (43) | 21.7572 (41) | 21.7572 (34) |
| 0.93 | 21.7572 (58) | 21.7572 (49) | 21.7572 (43) | 21.7572 (46) |
| 0.94 | 21.7572 (67) | 21.7572 (55) | 21.7572 (51) | 21.7572 (51) |
| 0.95 | 21.7572 (75) | 21.7572 (72) | 21.7572 (44) | 21.7572 (52) |
| 0.96 | 21.7572 (96) | 21.7572 (100) | 21.7572 (75) | 21.7572 (68) |
| 0.97 | 21.7571 | 21.7572 (70) | 21.5007 | 21.7572 (95) |
| 0.98 | 21.7554 | 21.7554 | 21.7565 | 21.7569 |
| 0.99 | 21.7559 | 21.7554 | 21.7552 | 21.5105 |

over which the global optimum is obtained, regardless of the number of grid points. Where the optimum was obtained, the number of iterations required to reach the optimum is given in parentheses. The reduction in the number of iterations required for convergence is only marginally reduced when N is increased. However, the range is increased for larger values of N. For example, with N = 27 the range for convergence to the global optimum is 0.88 ≤ γ ≤ 0.97. It is obvious that for this optimal control problem, a larger number of grid points than N = 1 is not justified.

### 6.3 Multi-pass approach

One method of preventing the collapse of the search region is to use the iterative dynamic programming in a multi-pass fashion, so that the region is restored to a fraction of its size at the beginning of the previous pass. The question that arises is, what should the restoration factor be and how sensitive are the results to that
