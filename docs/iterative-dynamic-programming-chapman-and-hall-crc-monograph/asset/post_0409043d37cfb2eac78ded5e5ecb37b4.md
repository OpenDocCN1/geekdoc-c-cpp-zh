
**Table 11.1: Effect of the penalty function factor $\theta$ on convergence for Example 1**

| Penalty factor $\theta$ | Deviation from desired state $|x_1(1)-1|$ | Performance index $I=x_2(1)$ | Shifting term $s_1$ | Sensitivity factor $-2\theta s_1$ |
|---:|---:|---:|---:|---:|
| 0.7 | $5.210\times10^{-7}$ | 0.924235 | 0.660319 | −0.92445 |
| 0.8 | $2.585\times10^{-7}$ | 0.924235 | 0.577780 | −0.92445 |
| 1.0 | $2.485\times10^{-8}$ | 0.924235 | 0.462224 | −0.92445 |
| 3.0 | $5.404\times10^{-8}$ | 0.924235 | 0.154075 | −0.92445 |
| 10 | $1.226\times10^{-7}$ | 0.924235 | 0.046223 | −0.92446 |
| 30 | $3.077\times10^{-8}$ | 0.924235 | 0.015407 | −0.92442 |
| 50 | $1.454\times10^{-6}$ | 0.924239 | 0.009243 | −0.92430 |
| 80 | $1.317\times10^{-6}$ | 0.925144 | 0.005847 | −0.93552 |
| 100 | $2.257\times10^{-5}$ | 0.925661 | 0.004719 | −0.94380 |

term $s_1$ was zero. The goal is to choose a piecewise linear control policy to minimize the augmented performance index $J$.

With both $\theta=1$ and $\theta=50$, rapid convergence to the minimum value of $I=0.92424$ resulted with the absolute difference from the desired state of less than $10^{-6}$ in 30 passes, as is shown in Figure 11.1. The computation time for 30 passes was 0.8 s on a Pentium3/500 digital computer. From the further results as given in Table 11.1, it is seen that the product $-2\theta s_1$ is constant and equal to $-I$ in the range $0.7\leq\theta\leq30$. In this range of $\theta$, the minimum value of the performance index is $I=0.924235$. For the penalty function factor greater than 30, the deviation from the desired state is larger and also the performance index is larger than the optimum value.

The control policy and the state trajectory are shown in Figure 11.2.

## *Relationship of the sensitivity factor to the adjoint variable*

Let us now solve this optimal control problem analytically by using Pontryagin’s maximum principle using the approach outlined by Lapidus and Luus [8]. The Hamiltonian for this system is

$$H=z_1u+x_1^2+u^2$$ \hfill (11.15)

where the adjoint variable $z_1$ is defined by

$$\frac{dz_1}{dt}=-\frac{\partial H}{\partial x_1}=-2x_1.$$ \hfill (11.16)

At the minimum value of the performance index $I$, the Hamiltonian is at its minimum value obtained through the stationary condition

$$\frac{\partial H}{\partial u}=z_1+2u=0,$$ \hfill (11.17)

![](img/06ae75163df4fdf5e1eec243d497d393_217_0.png)

Figure 11.1: Effect of the penalty function factor $\theta$ on convergence for Example 1

so that the optimal control is given by

$$u=-0.5z_1.$$  \tag{11.18}

By substituting Eq. (11.18) into Eq. (11.10) and differentiating with respect to $t$, and using Eq. (11.16), we get the second order differential equation

$$\frac{d^2x_1}{dt^2}-x_1=0.$$  \tag{11.19}

Eq. (11.19) with the given boundary conditions $(x_1(0)=x_1(1)=1)$ is easily solved to give

$$x_1=\frac{e^t+e^{(1-t)}}{1+e}.$$  \tag{11.20}

Differentiating Eq. (11.20) with respect to $t$ gives the optimal control from Eq. (11.10), namely,

$$u=\frac{e^t-e^{(1-t)}}{1+e}.$$  \tag{11.21}

The minimum performance index is obtained then by integrating

$$I=\int_0^1(x_1^2+u^2)\,dt$$  \tag{11.22}

giving

$$I=\frac{2(e-1)}{e+1}=0.9242344.$$  \tag{11.23}

![](img/06ae75163df4fdf5e1eec243d497d393_218_0.png)

Figure 11.2: Optimal control policy with 10 piecewise linear sections and the corresponding state trajectory for Example 1, giving I = 0.924235

It is noted that the performance index I = 0.924235 in Table 11.1 is very close to this analytical result.

This example was also used by Luus [10] with P = 20 piecewise constant control policy and a quadratic penalty function without the shifting term and by Dadebo and McAuley [3] with the use of P = 40. Although the value I = 0.92431 obtained by the latter was better than 0.92518 reported by Goh and Teo [4], it comes short of I = 0.9242345 obtained here with P = 10 piecewise linear control sections. The smoothness of the control policy as seen in Figure 11.2 contributes to the excellent agreement with the analytical solution.

From Eq. (11.18) we see that

z₁ = 2(e^(1−t) − e^t) / (1 + e) , (11.24)

so that at the final time t = 1,

z₁ = 2(1 − e) / (1 + e) (11.25)

which is negative of the performance index I. Therefore, as found computationally and reported in the fifth column of Table 11.1, the adjoint variable at the final time, in terms of the shifting term s₁, is equal to −2θ s₁.

## Example 2

Let us consider the first example used by Chen and Mills [1], which was also used by Luus and Storey [19]. The dynamics of the system are described by two state variables, but we introduce the third variable to put the performance index into the standard form for use of IDP:

\[\frac{dx_1}{dt} = x_2 + u_1\]\[\frac{dx_2}{dt} = -x_1 + u_2\]\[\frac{dx_3}{dt} = u_1^2 + u_2^2\]

with **x**(0) = [ -1 1 0 ]^T, and final time t_f = π/2. There are no constraints on the control variables, but there are two equality constraints to be satisfied at the final time

h_1 = x_1(t_f) - 1

and

h_2 = x_2(t_f) + 1.

It is required to find the unconstrained control policy that minimizes the performance index

I = x_3(t_f).

The augmented performance index to be minimized is therefore chosen as

J = I + θ[(h_1 - s_1)^2 + (h_2 - s_2)^2].

To determine how closely the equality constraints are satisfied, we consider the sum of squares of deviations

Q = h_1^2 + h_2^2.

For optimization with IDP, we chose P = 15 stages, each of equal length and sought to find piecewise linear control policy for each of the control variables. We chose the initial control policy **u** = **0**, the initial region size **r**_in = 2, the reduction factor γ = 0.85 and the region restoration factor η = 0.90, R = 5, and allowed 100 passes, each consisting of 30 iterations. We used a range of values for the penalty function factor θ. The computation time for 100 passes was 41 s on a PentiumII/350.

As is shown in Table 11.2, there is a wide range 1 ≤ θ ≤ 500 for which convergence to I = 2.5464796 occurs, the shifting parameter s_1 is very small, and the factor −2θs_2 is constant at 2.54648 which is equal to the optimum value of the performance index. As in Example 1, this is not a numerical coincidence, but can be proven, since this example can also be solved analytically, as we see shortly, to give the optimum value for the performance index I = 8/π = 2.546479. Therefore, the value obtained with 15 stages of piecewise linear control is excellent. The optimal control policy is given in Figure 11.3 and the state trajectories are given in Figure 11.4.

Table 11.2: Effect of the penalty function factor $\theta$ on convergence for Example 2

| Penalty function factor $\theta$ | Sum of squares $Q$ | Performance index $I$ | Shifting terms $s_1$ | $s_2$ |
|---:|---:|---:|---:|---:|
| 0.1 | $7.85 \times 10^{-13}$ | 2.5464773 | 0.00015 | -12.73239 |
| 1.0 | $1.99 \times 10^{-15}$ | 2.5464796 | 0.00000 | -1.27324 |
| 10 | $3.01 \times 10^{-15}$ | 2.5464796 | 0.00000 | -0.12732 |
| 100 | $2.32 \times 10^{-16}$ | 2.5464796 | 0.00000 | -0.01273 |
| 500 | $3.49 \times 10^{-16}$ | 2.5464796 | 0.00000 | -0.00255 |
| 1000 | $1.09 \times 10^{-12}$ | 2.5467489 | 0.00000 | -0.00127 |

## Relationship of the sensitivity factors to the adjoint variables at $t_f$

Let us now solve this optimal control problem analytically by using Pontryagin’s maximum principle. The Hamiltonian for this system is

$$H=z_1(x_2+u_1)+z_2(-x_1+u_2)+u_1^2+u_2^2$$  \tag{11.34}

where the adjoint variables $z_1$ and $z_2$ are defined by

$$\frac{dz_1}{dt}=-\frac{\partial H}{\partial x_1}=z_2$$  \tag{11.35}

and

$$\frac{dz_2}{dt}=-\frac{\partial H}{\partial x_2}=-z_1.$$  \tag{11.36}

At the minimum value of the performance index $I$, the Hamiltonian is at its minimum value obtained through the stationary condition

$$\frac{\partial H}{\partial u_1}=z_1+2u_1=0$$  \tag{11.37}

and

$$\frac{\partial H}{\partial u_2}=z_2+2u_2=0,$$  \tag{11.38}

yielding the optimal control policy

$$u_1=-0.5z_1$$  \tag{11.39}

and

$$u_2=-0.5z_2.$$  \tag{11.40}
