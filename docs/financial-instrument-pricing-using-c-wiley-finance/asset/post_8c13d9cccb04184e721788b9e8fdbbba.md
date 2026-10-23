
We thus see that the Fichera function is zero at the end points \(y = 0\) and \(y = 1\), and then no boundary conditions need be prescribed at these points. Instead, the PDE degenerates to the following ordinary differential equation at these points:

\[
\frac{\partial V}{\partial t} + rV = 0 \quad \text{at } y = 0,\ y = 1. \tag{20.43}
\]

The solution to (20.43) is given by:

\[
V(y, t) = C(y)e^{-rt} \quad \text{at } y = 0,\ y = 1. \tag{20.44}
\]
where the factor \(C(y)\) can be found by demanding compatibility between the solution (20.44) and the initial condition corresponding to the PDE at the points \(y = 0,\ y = 1\). Doing this will lead to the well-known boundary conditions for the Black–Scholes equation. For example, in the case of a put option \(C(y) = K\).

## 20.6 FINITE DIFFERENCE SCHEMES: PROPERTIES AND REQUIREMENTS

Let us review what we have achieved in this chapter. We have described an initial boundary value problem (IBVP) consisting of the following components:

- A1: A PDE of convection–diffusion–reaction type.
- A2: The bounded or unbounded region (domain) of \((x, t)\) space in which the PDE is defined.
- A3: The boundary conditions that the solution of the PDE satisfies.
- A4: The solution’s initial condition at \(t = 0\) (we are using forward time from \(t = 0\) up to expiration).

It is advantageous to know something about the qualitative properties of the IBVP before we jump into the coding of the finite difference scheme that will approximate the IBVP. We need to have a good idea of how to analyse the following attention points before we start designing algorithms:

- A5: Initialising the coefficients of the PDE (there may be an analytical formula or we may need to calibrate them). Special attention to be paid to small diffusion or large convection terms (convection dominance).
- A6: Transforming an unbounded domain to a bounded/truncated domain.
- A7: Determining what the boundary conditions should be (if it is possible at this stage; we may have to wait until we can define numerical boundary conditions). The boundary conditions can be of Dirichlet, Neumann or Robin types. It is even possible that no boundary condition is needed or allowed (see Section 20.5) and we may end up with the challenge of solving a PDE or ODE on a boundary.
- A8: How to handle discontinuities in the initial condition (payoff function). We may need to perform a smoothing operation on the initial condition.

It is possible to understand the complexities of these points by studying the relevant literature and attempting to implement them as part of an FDM algorithm. To this end, we address the following steps when mapping the PDE to the FDM:

- A9: Creating a *discrete domain* in \((x, t)\) space; do we choose constant meshes or adaptive meshes?
- A10: Approximating the time, diffusion and convection derivatives by *divided differences*.
- A11: *Numerical boundary conditions*, for example the numerical approximations of the boundary conditions in point A7.
- A12: Computing discrete variants of the initial condition taking points of discontinuity into consideration.

We are not there yet! Approximating derivatives by divided differences introduces errors and this leads us to a discussion of the stability and accuracy of the finite difference scheme that we propose to use. More detailed attention points are:

- A13: Do we use *one-step* or *multistep* methods in time?
- A14: The kind of marching scheme from \(t = 0\) to \(t = T\) to use (*explicit or implicit methods*).
- A15: Do we create our own solvers to march in the time direction (for example, Crank-Nicolson) or do we use a commercial or open source ODE (ordinary differential equation) solver, for example the Boost C++ *odeint* library.
- A16: Accuracy requirements (*first order, second order, higher order*).
- A17: Improving accuracy by using *extrapolation methods*, for example.
- A18: Assembling the discrete system of equations to form a matrix system or nonlinear system of equations.

These 18 attention points form a reasonably complete description of what skills and action points are needed when approximating linear initial boundary value problems using finite difference methods. We shall see examples in this and succeeding chapters.

The above steps and action points are also applicable to two-factor and to nonlinear problems.

## 20.7 EXAMPLE: A LINEAR TWO-POINT BOUNDARY VALUE PROBLEM

We begin our journey into the land of FDM by examining *time-independent second-order two-point boundary value problems* (TPBVPs) with Dirichlet boundary conditions defined on a bounded interval. TPBVPs are interesting for a number of reasons:

- We can approximate TPBVPs by the finite difference method, assemble the system of equations and solve the system using the Thomas or Double Sweep algorithms that we introduced in Chapter 13. This can be seen as preparation for our treatment of finite difference methods for the Black–Scholes PDE (see Exercise 5). It helps us gain insight into the numerical issues that arise with larger problems.

**Horizontal Method of Lines (Rothe’s Method):** we can reduce an initial boundary value problem to a TPBVP by discretising in the \(t\) direction (Ladyženskaja, Solonnikov and Ural’ceva, 1988, p. 241; Meyer, 2015, p. 61; Rothe, 1930). For example, we can discretise equation (20.13) in time by the fully implicit method (BTCS) (for notation, see Chapter 13) to produce the system of second-order ordinary differential equations:

\[
-\frac{u^{n+1} - u^n}{\Delta t} + \sigma(x, t_{n+1}) \frac{d^2 u^{n+1}}{dx^2} + \mu(x, t_{n+1}) \frac{d u^{n+1}}{dx} + b(x, t_{n+1}) u^{n+1} = f(x, t_{n+1}), \quad 0 \leq n \leq N - 1.
\]

In this case we use first-order backward divided differences to approximate the time derivative (another choice is the second-order Crank–Nicolson method based on centred differencing). We augment these ODEs with appropriate boundary and initial conditions.

- Rothe’s method is useful for problems with discontinuous payoffs, early-exercise features and problems with jumps and solutions of the Black–Scholes equation that change rapidly with respect to the underlying \(S\) at any given time (Meyer, 2015).
- The example shows how some finite difference methods lead to non-monotone schemes and how they can be made monotone by applying the exponential fitting method (Duffy, 1980, 2006). For a detailed discussion of numerical methods for two-point boundary value problems, see Keller (1968).

### 20.7.1 The Example

Our aim is to approximate the initial boundary value problem (20.14)–(20.16) by finite difference schemes. We first define some notation. To this end, we divide the interval \([A, B]\) into \(J\) equal subintervals:

\[
A = x_0 < x_1 < \ldots < x_J = B
\]

and we assume for convenience that the mesh points \(\{x_j\}_{j=0}^{J}\) are equidistant, that is:

\[
x_j = x_{j-1} + h, \quad j = 1, \ldots, J \quad (h = (B-A)/J).
\]

Furthermore, we divide the interval \([0, T]\) into \(N\) equal subintervals:

\[
0 = t_0 < t_1 < \ldots < t_N = T
\]

The essence of the finite difference approach lies in replacing the derivatives in equation (20.14) by divided differences at the mesh points \((x_j, t_n)\). We thus define the difference operators in the \(x\) direction as follows:

\[
D_+ u_j = \frac{u_{j+1} - u_j}{h}, \qquad
D_- u_j = \frac{u_j - u_{j-1}}{h}
\]

\[
D_0 u_j = \frac{u_{j+1} - u_{j-1}}{2h}, \qquad
D_+ D_- u_j = \frac{u_{j+1} - 2u_j + u_{j-1}}{h^2}.
\]

It can be shown by Taylor expansion that \(D_+\) and \(D_-\) are first-order approximations to \(\frac{\partial}{\partial x}\) while \(D_0\) is a second-order approximation to \(\frac{\partial}{\partial x}\). Finally, \(D_+D_-\) is a second-order approximation to \(\frac{\partial^2}{\partial x^2}\).

We first consider the following simple TPBVP. We find a function \(u\) such that:

\[
\sigma \frac{d^2 u}{dx^2} + 2 \frac{du}{dx} = 0 \quad \text{in } (0,1) \tag{20.45}
\]

\[
u(0) = 1, \quad u(1) = 0.
\]

We assume that \(\sigma\) is a positive constant. We now replace the derivatives in (20.45) by their corresponding centred differences to produce the following finite difference method. We find a mesh function \(\{U_j\}_{j=1}^{J-1}\) such that:

\[
\sigma D_+ D_- U_j + 2D_0 U_j = 0, \quad j = 1, \ldots, J-1 \tag{20.46}
\]

\[
U_0 = 1, \quad U_J = 0.
\]

Scheme (20.46) is sometimes called the *centred difference scheme* and it is a popular way to approximate convection–diffusion equations.

It can be checked that the exact solution of (20.45) is given by:

\[
u(x) = \frac{e^{-2x/\sigma} - e^{-2/\sigma}}{1 - e^{-2/\sigma}}. \tag{20.47}
\]

It can also be checked that the exact solution of (20.46) is given by:

\[
U_j = \frac{\lambda^j - \lambda^J}{1 - \lambda^J}, \quad \text{where } \lambda = \frac{1 - h/\sigma}{1 + h/\sigma}. \tag{20.48}
\]

Let us now assume that \(\sigma < h\) in equation (20.48). This means that \(\lambda < 0\) and thus

\[
U_j - u(x_j) = \frac{\lambda^j - \lambda^J}{1 - \lambda^J} - \frac{r^j - r^J}{1 - r^J}, \qquad r = e^{-2h/\sigma}
\]

is positive or negative depending on whether \(j\) is even or odd. Furthermore,

\[
\lim_{\sigma \to 0} U_j = \frac{(-1)^j + 1}{2} \quad \text{if } J \text{ is odd}.
\]

Hence \(U_j\) oscillates in a bounded fashion for all \(\sigma\) satisfying \(\sigma < h\). We thus conclude that centred finite difference schemes are unsuitable for the numerical solution of problem (20.45) when \(\sigma < h\). It can even be shown that this difference scheme produces a solution that goes to
