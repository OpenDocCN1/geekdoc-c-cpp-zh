
The time optimal control problem is to find the control policy $\mathbf{u}(t)$ in the time interval $0 \le t < t_f$ that minimizes the performance index

$$
I = t_f. \tag{12.4}
$$

Numerically, it is required that in finding a minimum value of the final time $t_f$, we satisfy the constraint

$$
|x_i(t_f) - x_i^d| \le \varepsilon_i, \quad i = 1, 2, \cdots, n, \tag{12.5}
$$

where $\varepsilon_i$ is some tolerance, such as the measurement error.

## 12.3 Direct approach to time optimal control

To solve this optimal control problem, we follow the suggestion of Luus [10] to choose the augmented performance index to be minimized as

$$
J = t_f + \theta \sum_{i=1}^{n} (x_i(t_f) - x_i^d - s_i)^2, \tag{12.6}
$$

and update the shifting terms $s_i$ after every pass of IDP according to

$$
s_i^{q+1} = s_i^q - (x_i(t_f) - x_i^d), \tag{12.7}
$$

where $q$ is the pass number in IDP.

To measure the closeness of the final states to the desired states we use the norm of the sum of absolute deviations from the desired state, namely

$$
S = \sum_{i=1}^{n} |x_i(t_f) - x_i^d|. \tag{12.8}
$$

In order to solve the time optimal control problem by IDP, we transform the continuous control policy into a piecewise constant control problem by dividing the time interval $[0, t_f]$ into $P$ stages, each of variable length,

$$
v(k) = t_k - t_{k-1}, \quad k = 1, 2, \cdots, P. \tag{12.9}
$$

Computationally, we impose the condition

$$
v(k) > 0, \quad k = 1, 2, \cdots, P, \tag{12.10}
$$

so that we do not deal with negative stage lengths.

As we did in Chapter 9, based on the idea of Bojkov and Luus [3], we transform the time variable through the relationship

$$
dt = v(k) P d\tau, \tag{12.11}
$$

so that in normalized time all the time stages are of equal length

$$
\tau_k = \frac{k}{P}, \quad k = 1, 2, \cdots, P. \tag{12.12}
$$

The differential equation in the time interval $\tau_{k-1} \le \tau < \tau_k$ becomes

$$
\frac{d\mathbf{x}}{d\tau} = v(k) P f(\mathbf{x}, \mathbf{u}). \tag{12.13}
$$

With this transformation, at $t = t_f$, the transformed time variable $\tau = 1$, and the time to reach the desired state is

$$
t_f = \sum_{k=1}^{P} v(k). \tag{12.14}
$$

Minimization of the augmented performance index in Eq. (12.6) should give the minimum value of $t_f$ and ensure that the state variables at the final time are close to the desired values. In order to test the computational viability of this approach, we consider several examples. In all the examples we used the DVERK [7] subroutine, listed in Appendix E, to integrate the differential equations.

## 12.4 Examples

### 12.4.1 Example 1: Bridge crane system

Let us consider the bridge crane system used by Moon and VanLandingham [13], where the system is described by four differential equations

$$
\frac{dx_1}{dt} = x_2 \tag{12.15}
$$

$$
\frac{dx_2}{dt} = u \tag{12.16}
$$

$$
\frac{dx_3}{dt} = x_4 \tag{12.17}
$$

$$
\frac{dx_4}{dt} = -0.98 x_3 + 0.1 u \tag{12.18}
$$

with $\mathbf{x}^T(0) = \mathbf{0}$, and the desired final state is $\mathbf{x}^d = [15 \ 0 \ 0 \ 0]^T$. The constraints on the control are

$$
-1 \le u \le 1. \tag{12.19}
$$

It is required to find the control policy that minimizes the performance index

$$
I = t_f. \tag{12.20}
$$

We therefore choose the augmented performance index

$$
J = t_f + \theta\left[(x_1(t_f) - 15 - s_1)^2 + (x_2(t_f) - s_2)^2 + (x_3(t_f) - s_3)^2 + (x_4(t_f) - s_4)^2\right], \tag{12.21}
$$

where $\theta$ is a positive penalty function factor and the shifting terms $s_i$ are updated after every pass of IDP according to Eq. (12.7).

To solve this problem, we made two preliminary runs with $P = 5$ time stages, each chosen initially to be of length 1.0. We chose the initial control policy to be zero, and initial region sizes for both control and stage lengths to be 1.0. The penalty function factor $\theta$ was chosen to be 10, $R = 50$, region contraction factor $\gamma = 0.80$, region restoration factor $\eta = 0.95$, and 100 passes each consisting of 30 iterations were performed. The runs were made with $N = 3$ grid points, and with $N = 5$. The convergence profiles of these runs were very similar, but a smaller value for $t_f$ was obtained with $N = 5$, namely, 8.58012 versus $t_f = 8.58162$ with $N = 3$. The convergence profile with $N = 5$ is shown in Figure 12.1. The resulting control policy consisted of 4 stages with $u(0) = 1.0$, $u(1) = -1.0$, $u(2) = 1.0$, and $u(3) = -1.0$, with the length of the stages 2.98534, 1.30471, 1.30394, and 2.98492 respectively. There was also a very short stage of length 0.00119 with a control value of 0.2963 before the last stage. The shifting terms were $s_1 = 0.0090816$, $s_2 = -0.038988$, $s_3 = 0.054761$, and $s_4 = -0.110204$.

To refine these results, we dropped the very short stage, and used the results of this preliminary run as the initial conditions, including the values for the shifting terms, and performed a run with $R = 25$, putting the region size for control to zero, and reducing the value of the region size for stage lengths to 0.1. After 100 passes, the final time was reduced to $t_f = 8.58010$ and the sum of absolute value norm of deviations was $1.098 \times 10^{-7}$. The stage lengths converged to $v(1) = 2.98534$, $v(2) = 1.30471$, $v(3) = 1.30471$, and $v(4) = 2.98534$. It is interesting to note the symmetry where $v(1) = v(4)$ with $u(0) = 1$, $u(3) = -1$, and $v(2) = v(3)$ with $u(1) = -1$, $u(2) = 1$. The run was repeated with $\theta = 1$ and $\theta = 100$.

Convergence patterns for all three values of $\theta$ were very similar, as is shown for $\theta = 1$ and $\theta = 10$ in Figure 12.2. Identical values were obtained for the stage lengths. However, the shifting terms, given in Table 12.1, for the three cases are different, yielding the same value for the sensitivity, as given in the fifth column. In fact, the factor $-2\theta s_i$ gives the adjoint variable at the final time, corresponding to the variable $i$, and should be the same for all the values of $\theta$. It should be noted that the values for the sensitivity in the fifth column of Table 12.1 are close to the final values of the adjoint variables obtained by Moon and VanLandingham [13], given in the sixth column of Table 12.1.

The time optimal control policy is shown in Figure 12.3.

**Table 12.1:** Shifting terms and sensitivity for Example 1

| Variable | Shifting terms, $s_i$: $\theta=1$ / $\theta=10$ / $\theta=100$ | Sensitivity $-2\theta s_i$ | Adjoint variable at $t_f = 8.5801$ [13] |
|---|---:|---:|---:|
| 1 | $0.090861$ / $0.009086$ / $0.0009086$ | $-0.182$ | $-0.182$ |
| 2 | $-0.389797$ / $-0.038980$ / $-0.0038981$ | $0.780$ | $0.782$ |
| 3 | $0.547945$ / $0.054793$ / $0.0054782$ | $-1.096$ | $-1.086$ |
| 4 | $-1.102032$ / $-0.110203$ / $-0.0110194$ | $2.204$ | $2.216$ |

![](img/06ae75163df4fdf5e1eec243d497d393_254_0.png)

Figure 12.1: Sum of absolute deviations of the final state variables from the desired values for the preliminary run $N = 5$ grid points for Example 1

### 12.4.2 Example 2: Two-link robotic arm

Let us consider the minimum time control of a two-link robotic arm as considered by Weinreb and Bryson [17], Lee [8], Bojkov and Luus [1], and Luus [10], where the equations are given by

$$
\frac{dx_1}{dt} = \frac{(\sin x_3)\left[\frac{9}{4}(\cos x_3)x_1^2 + 2x_2^2\right] + \frac{4}{3}(u_1 - u_2) - \frac{3}{2}(\cos x_3)u_2}{\frac{31}{36} + \frac{9}{4}\sin^2 x_3} \tag{12.22}
$$

$$
\frac{dx_2}{dt} = -\frac{(\sin x_3)\left[\frac{7}{2}x_1^2 + \frac{9}{4}(\cos x_3)x_2\right] - \frac{7}{3}u_2 + \frac{3}{2}(\cos x_3)(u_1 - u_2)}{\frac{31}{36} + \frac{9}{4}\sin^2 x_3} \tag{12.23}
$$

$$
\frac{dx_3}{dt} = x_2 - x_1 \tag{12.24}
$$

![](img/06ae75163df4fdf5e1eec243d497d393_255_0.png)

Figure 12.2: Sum of absolute deviations of the final state variables from the desired values for two values of the penalty function factor for Example 1

$$
\frac{dx_4}{dt} = x_1 \tag{12.25}
$$

where $x_1$ and $x_2$ are the inertial velocities of the shoulder and elbow links, and $x_3$ and $x_4$ are the angles. The initial state is $\mathbf{x}(0) = [0 \ 0 \ 0.5 \ 0]^T$, and the desired final state is $\mathbf{x}^d = [0 \ 0 \ 0.5 \ 0.522]^T$. The constraints on the control are

$$
-1 \le u_j \le 1, \quad j = 1, 2. \tag{12.26}
$$

It is required to find the control policy that minimizes the performance index

$$
I = t_f. \tag{12.27}
$$

We therefore choose the augmented performance index

$$
J = t_f + \theta\left[(x_1(t_f) - s_1)^2 + (x_2(t_f) - s_2)^2 + (x_3(t_f) - 0.5 - s_3)^2 + (x_4(t_f) - 0.522 - s_4)^2\right], \tag{12.28}
$$

where $\theta$ is a positive penalty function factor and the shifting terms $s_i$ are updated after every pass of IDP. To keep track of the convergence, we record after every pass the norm of the absolute value deviations of the final state from the desired state

$$
S = |x_1(t_f)| + |x_2(t_f)| + |x_3(t_f) - 0.5| + |x_4(t_f) - 0.522|. \tag{12.29}
$$
