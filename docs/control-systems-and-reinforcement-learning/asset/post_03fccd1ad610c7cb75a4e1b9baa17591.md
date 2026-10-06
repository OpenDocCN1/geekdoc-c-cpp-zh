
## Control Crash Course

- (a) Obtain a linearized state model with equilibrium $(x^s, u^s)$ for each equilibrium (you will find that $x_i^s = 0$ is required). Comment on the challenge for $x_i^s = \pm t/2$.
- (b) Obtain a linear feedback law that results in $x = 0$ asymptotically stable (locally). You will obtain a control solution that is globally asymptotically stable in Exercise 3.10 after you learn a few concepts from optimal control in the next chapter.
- (c) Find $u^0$ such that $x^0 = (r,0)^T$ is an equilibrium: $f(x^0, u^0) = 0$. Based on the linearization (2.62), find a linear control law for (2.62), of the form

$\tilde{u} = -\tilde{K}\tilde{x} = K_1\tilde{x}_1 - K_2\tilde{x}_2$

- (b) With this difficulty is that $u^d$ depends on $c/m$, which may not be known. Modify your design as follows:

$\hat{u} = -K^a\tilde{x}^a, \quad \text{where} \quad \tilde{x}^a = (\tilde{x}_1^a, \tilde{x}_2^a)^T, \quad z_l^a = \int_{0}^{t} \tilde{x}_1 \, dr \quad (2.73)$

with $K = [K_1, K_2, K_3]$. This is known as proportional-integral-derivative (PID) control. Obtain a third-order linear state model, and $K_i > 0$ for the $3 \times 3$ matrix remains Hurwitz, and the transient behavior remains "good" (or define what that means). Observe the equilibrium condition $\frac{d}{dt}x^a=0$ implies that $x_1^a = r$.
- (c) Simulate in Exercise 2.16 to estimate the region of attraction (which may restrict the simulation to initial conditions with zero velocity).

2.18 Feedback Linearization for MagBall. For systems with some nonlinearities, there is a "brute-force" approach to obtain a linear model. For MagBall, you may view $v = u^2/x_1$ as an input, from which we obtain a linear system by (2.60):

``` $\frac{d}{dt}x=x^2,\frac{d}{dt}v=g-\frac{\kappa}{m}$ ```

- (a) As in the previous exercise, obtain a control law $u = -K\tilde{x}$, where $K_1$ and $K_2$ are parameters chosen for stability and robust response.
- (b) Obtain an expression for the equilibrium $x^s$ for the closed-loop system using the gain $\frac{d}{dt}x_i=0$ for $i=1,2$.
- (c) Modify your design in (2.73): $v = -K^a\tilde{x}$. Find $K_3 > 0$ so that the transient behavior remains "good".
- (d) You will need to modify your policy in (c) so that $v$ is nonnegative, say $v = \Phi(\tilde{x}^a) = \max(0, K_0\tilde{x}^a + K_3\tilde{x}^a)$. The current applied to the magnet is this

``` $u = x_1\sqrt{\Phi(\tilde{x}^a)}. \quad$ (2.74) ```

Simulate, and estimate the region of attraction. You may restrict the simulation to zero initial velocity. How the region of attraction change when $k$ is divided by 2? Do not change your policy! The point is to check if your solution is robust to an inaccurate model.
Warning: Recall that it is not possible to achieve convergence from any initial condition.
Note: See [199] for a survey on feedback linearization - a topic that has far more depth than obvious from this example.

## 2.9 Notes

## Matrix Algebra

2.20 Let $A$ be an $n \times n$ matrix, and suppose that the following infinite sum exists:

$U = I+A+A^2+A^3+\dots$

where $I$ denotes the identity matrix. Verify that $U$ is an inverse of the matrix $I-A$.
Note that this coincides with the Taylor series expansion of $f(x) = 1/(1-x)$ when $n=1$.

2.21 Two square matrices $A$ and $\tilde{A}$ are called similar if there is an invertible matrix $M$ such that

$A = M^{-1}AM$.

Obtain the following for two similar matrices $A$ and $\tilde{A}$.

$A^1 = A, \quad\quad \tilde{A}^m = A(\tilde{A}^{m-1}), \quad\quad\quad m \ge 1$.

- (b) Show that $v$ is an eigenvector for $A$ if and only if $Mv$ is an eigenvector for $\tilde{A}$.
- (c) Suppose that $A$ is diagonal $(\tilde{A}_{ij} = 0$ if $i \neq j)$. Suppose moreover that $|\tilde{A}_{ii}| < 1$ for each $i$. Conclude that $I-\tilde{A}$ admits an inverse by applying Exercise 2.20.
2.22 Matrix Exponential. Compute $e^{At}$ for all $t \in \{0, 1\}$ for $2 \times 2$ matrix

$e^{At} = \begin{bmatrix} a & b \\ 0 & a \end{bmatrix}, \quad I = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}, \quad J = \begin{bmatrix} 0 & 1 \\ 0 & 0 \end{bmatrix}$.

It is not difficult to obtain $e^{At} = e^{at}(I + btJ)$. For $3 \times 3$ matrix

$A = \begin{bmatrix} a & b & c \\ 0 & a & b \\ 0 & 0 & a \end{bmatrix}, \quad e^{At} = e^{at}(I + btJ + \frac{b^2t^2}{2}J^2)$.

Note that $J^2 = 0$ and $J^3 = 0$. In general, the matrix exponential of a matrix is:

$e^A = I + A + A^2 + A^3 + \dots$

## 3 Optimal Control

The chapter surveys optimization techniques for design of feedback loops in Figure 2.1. The feedforward component is often designed based on optimization, but the dynamic programming equations are the focus of this chapter. Keep the larger feedback loops in mind when you apply RL to real-world.

### 3.1 Value Function for Total Cost

To begin, we recall some notation: $x(k)$ is the state at time $k$, which evolves in state space $X$; $u(k)$ is input at time $k$, which evolves in input (or action) space $U$ (the sets $X$ and $U$ may be Euclidean, a finite set, or something exotic). There may also be an output $y$ as shown in Figure 2.1, but it is usually ignored in this chapter. The input and state are related through the dynamical system (2.6a)

``` $x(k+1) = F(x(k), u(k)), ```

(3.1)

Design of a state feedback policy $u(k) = \phi(x(k))$ is based on a cost function $c$. It is assumed that it takes nonnegative values:

``` $c: X \times U \rightarrow \mathbb{R}_+$. ```

The total cost $J$ associated with a particular control input $u \overset{\text{def}}{=} u_{[0, \infty)}$ is defined by the

``` $J(u) = \sum_{k=0}^{\infty} c(x(k), u(k)). ```

The value function is defined to be the minimum over all inputs, which is a function of the initial condition:

``` $J^*(x) = \min_{k=0}^{\infty} c(x(k), u(k)), \quad x(0) = x \in \mathbb{X}$. ```

(3.2)

The goal of optimal control is to find an input sequence that achieves the minimum in (3.2). We settle for an approximation in the majority of cases.
