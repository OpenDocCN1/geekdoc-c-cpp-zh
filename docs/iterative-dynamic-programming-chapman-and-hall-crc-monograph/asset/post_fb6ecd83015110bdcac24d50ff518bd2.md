

**Table 5.2:** Piecewise constant optimal control policy with four control variables giving the maximum $I = 21.75722$

| Stage | Time | $u_1$ | $u_2$ | $u_3$ | $u_4$ |
|---:|---:|---:|---:|---:|---:|
| 1 | 0.0000 | 0.00000 | 0.00000 | 1.64594 | 20.00000 |
| 2 | 0.0182 | 14.17009 | 0.00000 | 1.49448 | 20.00000 |
| 3 | 0.0364 | 19.30869 | 0.00000 | 0.71145 | 20.00000 |
| 4 | 0.0546 | 12.21929 | 6.00000 | 0.27487 | 0.00000 |
| 5 | 0.0727 | 3.61857 | 3.99978 | 0.24286 | 0.00000 |
| 6 | 0.0909 | 0.00000 | 0.00000 | 0.49520 | 0.00000 |
| 7 | 0.1091 | 0.00000 | 0.00000 | 0.98515 | 0.00000 |
| 8 | 0.1273 | 0.00000 | 0.00000 | 1.89196 | 20.00000 |
| 9 | 0.1455 | 11.67268 | 0.00000 | 1.91146 | 20.00000 |
| 10 | 0.1636 | 20.00000 | 6.00000 | 0.95895 | 20.00000 |
| 11 | 0.1818 | 20.00000 | 6.00000 | 0.26054 | 20.00000 |

![](img/06ae75163df4fdf5e1eec243d497d393_110_0.png)

**Figure 5.3:** Convergence profile showing the effect of the number of randomly chosen candidates for control with $\gamma = 0.85$

**Table 5.3:** Effect of the number of randomly chosen candidates for control at each grid point with $N = 3$ grid points

| Reduction factor $\gamma$ | $R = 25$: Performance index, $I$ | $R = 25$: Number of iterations | $R = 50$: Performance index, $I$ | $R = 50$: Number of iterations |
|---:|---:|---:|---:|---:|
| 0.90 | 21.6564 | 150 | 21.6149 | 150 |
| 0.91 | 21.6555 | 150 | 21.5067 | 150 |
| 0.92 | 21.7044 | 150 | **21.7572** | 69 |
| 0.93 | 21.6770 | 150 | **21.7572** | 68 |
| 0.94 | 21.7375 | 150 | 21.5115 | 150 |
| 0.95 | **21.7572** | 93 | 21.5115 | 150 |
| 0.96 | **21.7572** | 118 | **21.7572** | 96 |
| 0.97 | 21.7555 | 150 | **21.7572** | 138 |
| 0.98 | 21.7565 | 150 | 21.7570 | 150 |
| 0.99 | 21.7535 | 150 | 21.7505 | 150 |

![](img/06ae75163df4fdf5e1eec243d497d393_111_0.png)

**Figure 5.4:** Convergence profile showing the effect of the number of randomly chosen candidates for control with $\gamma = 0.90$

## Chapter 6: Evaluation of parameters in IDP

### 6.1 Introduction

In iterative dynamic programming there are numerous parameters that can be varied. Already in Chapter 5 we saw the different ways of choosing candidates for control and the effects of the number of such values chosen at each grid point, and also the effect of the region contraction factor $\gamma$. If $\gamma$ is too small, we get premature collapse of the region, and if $\gamma$ is too large then either the convergence rate may be rather slow or convergence may not be obtained at all. Fortunately there is generally a wide range over which acceptable values for $\gamma$ may be chosen to yield convergence to the optimum. There is a balance between the number of allowable values for control $R$ and the region contraction factor $\gamma$. If $R$ is chosen to be sufficiently large, then $\gamma$ can be chosen to be quite small such as 0.7 without fear of premature region collapse. However, if a small value for $R$ is used, then $\gamma$ must be increased to a value closer to 0.9. Normally we would like to choose $R$ as small as possible to reduce computational effort.

The choice for the number of grid points, however, is not quite as clear. In a very difficult nonlinear optimal control problem involving the determination of the optimal catalyst blend along a tubular reactor [7], convergence to the global optimum was readily obtained by using a single grid point at each time stage [6]. A straightforward fed-batch reactor optimization problem, on the other hand, required a minimum of 23 grid points for convergence to the global optimum [3]. Bojkov and Luus [2] studied the effects of the parameters in IDP and concluded that for many typical chemical engineering systems the region contraction factor $\gamma$ should be in the range 0.75 to 0.95, and the use of more than 3 grid points does not increase the likelihood of getting the global optimum nor improve the convergence rate. Although surprising, with the exception of a few reactor problems such as the fed-batch reactor considered by Hartig et al. [3] and the two-stage CSTR we consider later in this chapter, the requirement of only a small number of grid points appears to be generally true for many optimal control problems. Therefore, we may use a single grid point at each time stage for many problems and still obtain fast and accurate convergence to the global optimum.

The goal here is to illustrate the effects of the parameters used in IDP, such as the region reduction factor $\gamma$ used after every iteration to reduce the size of the region, the region restoration factor $\eta$ which is used to restore the region size after every pass, the initial region size, number of allowable values for control, and the number of grid points used at each time step. The use of several examples is the best way to show the relationship among the parameters used in IDP.

### 6.2 Number of grid points

In the early work with iterative dynamic programming, the number of grid points used was chosen to be quite large, usually greater than 20. The motivation for the use of large number of grid points was due to the vectorization capability of the CRAY supercomputer that was used, enabling the calculations to be done in parallel fashion. When calculations were switched from the CRAY to personal computers, the need to examine the effect of the number of grid points became necessary, since doubling the number of grid points more than doubled the computation time. The investigation of Bojkov and Luus [2] made it clear that a large number of grid points is not always necessary. Furthermore, it is obvious that if the number of grid points can be reduced without sacrificing convergence rate, then we should use the minimum number, namely $N = 1$, whenever possible.

The choice of the initial region size over which candidates for control are chosen is also very important, especially when numerous local optima are present. To illustrate the effects of grid points, the choice of the initial region size, and the relationship of other parameters, we choose two examples from chemical engineering. In the first example we use a single grid point, since convergence to the global optimum is so readily obtained that there is no need to examine the use of a larger number of grid points. In the second example, the effect of the use of a different number of grid points is illustrated. In Section 6.3 we examine the multi-pass approach and present another example for which we need several grid points to get accurate convergence.

### 6.2.1 Bifunctional catalyst blend optimization problem

In the optimization of the blend of a bifunctional catalyst in converting methylcyclopentane to benzene in a tubular reactor, the blend of two monofunctional catalyst components involving hydrogenation and isomerization is characterized by the mass fraction $u$ given by

$$u = \frac{\text{mass of hydrogenation component}}{\text{total mass of the catalyst}}. \quad (6.1)$$

**Table 6.1:** Coefficients for the rate constants $k_i$ used in bifunctional catalyst problem

| $i$ | $c_{i0}$ | $c_{i1}$ | $c_{i2}$ | $c_{i3}$ |
|---|---:|---:|---:|---:|
| 1 | 0.2918487D-02 | -0.8045787D-02 | 0.6749947D-02 | -0.1416647D-02 |
| 2 | 0.9509977D+01 | -0.3500994D+02 | 0.4283329D+02 | -0.1733333D+02 |
| 3 | 0.2682093D+02 | -0.9556079D+02 | 0.1130398D+03 | -0.4429997D+02 |
| 4 | 0.2087241D+03 | -0.7198052D+03 | 0.8277466D+03 | -0.3166655D+03 |
| 5 | 0.1350005D+01 | -0.6850027D+01 | 0.1216671D+02 | -0.6666689D+01 |
| 6 | 0.1921995D-01 | -0.7945320D-01 | 0.1105666D+00 | -0.5033333D-01 |
| 7 | 0.1323596D+00 | -0.4696255D+00 | 0.5539323D+00 | -0.2166664D+00 |
| 8 | 0.7339981D+01 | -0.2527328D+02 | 0.2993329D+02 | -0.1199999D+02 |
| 9 | -0.3950534D+00 | 0.1679353D+01 | -0.1777829D+01 | 0.4974987D+00 |
| 10 | -0.2504665D-04 | 0.1005854D-01 | -0.1986696D-01 | 0.9833470D-02 |

As was done by Luus et al. [7], to solve this optimal control problem, we divide the given time interval into 10 equal sections, each of length 200 g h/mol, and determine the piecewise constant values for control in each section $u(0), u(1), \cdots, u(9)$ to maximize the performance index given in Eq. (6.13). For integration we used the integration subroutine DVERK of Hull et al. [4] with local error tolerance of $10^{-6}$. There are numerous local optima. By using sequential quadratic programming as suggested by Rosen and Luus [12], from 100 initial points chosen at random 25 local optima were obtained, with the following values of the performance index: 10.053, 9.905, 9.881, 9.866, 9.815, 9.786, 9.722, 9.641, 9.628, 9.608, 9.582, 9.534, 9.501, 9.463, 9.439, 9.343, 9.293, 9.246, 9.148, 9.037, 8.673, 8.645, 8.490, 8.402, and 8.113. However, none of these is the global optimum.

The global optimal control policy and the next four best ones are given in Table 6.2. As was pointed out by Luus et al. [7], there are numerous local optima for this problem, many of which are not listed above. The aim is to get the global optimum. From the initial control policy $u^{(0)}(k)=0.75,\ k=0,1,\cdots,9$ and initial region size $r^{(0)}(k)=0.3,\ k=0,1,\cdots,9$ with the region contraction factor $\gamma=0.70$, the number of grid points $N=21$ and $M=5$ uniformly chosen values for control, Luus et al. [7] obtained the global optimum with the use of IDP in 16 iterations. The $M$ candidates for control were chosen from the uniform distribution around the best value, i.e., $u^*,\ u^* \pm \left[\frac{2j}{M-1}\right]r,\quad j=1,2,\cdots,(M-1)/2$, where $u^*$ is the best value for the catalyst blend from the previous iteration.

Luus and Bojkov [6] showed that the global optimum could be obtained with a single grid point, $N=1$, if the initial region is chosen to be sufficiently large. In Tables 6.3 and 6.4 we show the effect of the region contraction factor $\gamma$, the initial region size $r^{(0)}$, and the number of uniformly chosen candidates for control $M$. The number of iterations to reach the global optimum to six figures is shown in parentheses.

