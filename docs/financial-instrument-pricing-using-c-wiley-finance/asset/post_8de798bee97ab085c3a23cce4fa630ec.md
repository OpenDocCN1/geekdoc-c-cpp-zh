
Finally, we note that the need to compute the exponential of a matrix and to approximate the solution of matrix differential equations is of universal interest in many branches of science, engineering and finance. For example, in credit rating (Wilmott, 2006, Vol. 2, pp. 665–668), estimating transition matrices from observed data (Inamura, 2006) and the matrix Riccati equation (Boyle and Guan, 2002). We discuss this equation in short for completeness. Given are the n state variables X1, …, Xn satisfying the vector SDE:

dX = (K0 + K1 X) dt + σ(X) dW
where:
X = (X1, …, Xn)T, K0 ∈ ℝn, K1 ∈ ℝn×n, σ : ℝn → ℝn×n
W(t) = (W1(t), …, Wn(t))T (n-dimensional Brownian motion). (25.9)

The short rate is given by:
r(t) = Σ_{j=1}^n Xj(t). (25.10)

Then the price of a zero-coupon bond at time t that matures at time T is given by:
P(t, T) = exp(A(t, T) − B(t, T) X) (25.11)

The corresponding matrix Riccati equation is given by:
dB/dt = 1/2 Bᵀ H B − K1ᵀ B − a
dA/dt = K0 B
where:
{ B = B(t, T), A = A(t, T)
a = (1, …, 1)ᵀ
H = (Hij) ∈ ℝn×n and Hij(x) = (σ(x) σ(x)ᵀ)ij, 1 ≤ i, j ≤ n. } (25.12)

This system of equations can be solved numerically using odeint.

## 25.5 THE METHOD OF LINES: WHAT IS IT AND WHAT ARE ITS ADVANTAGES?

In Chapters 20 to 23 we introduced the finite difference method (FDM) for time-dependent convection–diffusion–reaction PDEs. The approach was to discretise the PDE in space and time simultaneously and then solve the resulting linear or nonlinear system of equations at each time step. This is a generally accepted practice in computational finance. In this section we take a different approach by discretising in the space direction using only standard centred

- 2. The resulting system of ODEs is amenable to analysis, including existence and uniqueness results and qualitative properties of the ODE system.
- 3. High-accuracy, professional and robust open-source and commercial ODE solvers are available. There is no need to create your own home-grown solvers. Most developers are not full-time numerical analysts working on the numerical solution of ODEs, and it is better to outsource this part of the project rather than create your own solvers.
- 4. The MOL can be applied to nonlinear PDEs and PDEs with discontinuous initial conditions (payoff). In particular, special ODE solvers can be used to solve *stiff* ODEs.
- 5. The MOL is a competitor to the ADI and ‘Soviet Splitting’ methods in the sense that splitting an *n*-dimensional PDE into a sequence of one-dimensional PDEs may be redundant. ADI and splitting methods are more difficult to apply than the MOL to nonlinear and stiff problems.
- 6. Time-to-market and time-to-develop: it takes less time to write and debug code that uses the MOL and ODE solvers than handcrafted code. This is what we have found compared with the amount of time it took us to write the solvers in Chapters 20 to 23.
- 7. For PDE novices it is easier to apply the finite difference method by delegating to ODE solvers rather than trying to handcraft, test and debug your own Crank–Nicolson solver, at least in the short term.

We mention that the MOL in the current context is the VMOL (*Vertical MOL*) because discretisation takes place in a vertical direction. This is in contrast to the HMOL (*Horizontal MOL*, also known as *Rothe’s method*) where discretisation takes place in a horizontal direction. A discussion of this method can be found in Ladyženskaja, Solonnikov and Ural’ceva (1988) and Meyer (2015). For completeness, we show how to discretise system (25.13) using the HMOL. We discretise in time using the BTCS (implicit Euler) scheme. This leads to a *two-point boundary value problem* at each time level for the function $u^n \equiv u^n(x)$:

\begin{align*}
\frac{u^{n+1} - u^n}{\Delta t} &= \frac{d^2 u^{n+1}}{dx^2}, \quad n = 0, \dots, N-1 \\
u^{n+1}(0) = u^{n+1}(1) = 0 \\
u^0(x) = f(x), \ 0 \le x \le 1.
\end{align*}
(25.16)

We can now approximate the solution of (25.16) using the finite difference method, matrix solvers and interpolators that we introduced in Chapter 13.

## 25.6 INITIAL FORAY IN COMPUTATIONAL FINANCE: MOL FOR ONE-FACTOR BLACK–SCHOLES PDE

Having discussed Boost *odeint* and the MOL, we now turn our attention to creating our first option pricing code using these techniques. We reduce the scope by pricing a put option with early-exercise features. We deliberately avoid trying to over-engineer the solution and we produce a solution using global data and functions. The goal is to get accurate prices in the short term. For this problem, we can take it that the price P = 6.2995968 is the reference price which the various solvers should emulate.

Concerning the early-exercise constraint we add a *penalty term* to the PDE. The approach is based on optimisation methods. More generally, consider the *constrained optimisation* problem:

min f(x), f : ℝⁿ → ℝ, x ∈ ℝⁿ
subject to
gⱼ(x) ≥ 0,   j = 1, …, m.  (25.17)

The penalty method allows us to introduce a new parameter μ → ∞ and we get a new *unconstrained optimisation* problem:

minₓ ( f(x) + μ Σⱼ=1ᵐ |gⱼ(x)|² ).  (25.18)

Moving to the Black–Scholes PDE, the equivalent early-exercise constraint is:

V ≥ φ where φ = φ(x) is the option payoff and V is the option price  (25.19)

which can be written in the more generic form to produce a penalty term:

g(V, x) = V − φ(x) ≥ 0  (25.20)

where V is the option price. All this mathematics led us to the C++ code for the penalty term:

```
// For American options
value_type penalty(value_type x, value_type u)
{
    // The rationale is that if correction < 0 the
    // constraint is satisfied and the penalty = 0.
    // Otherise, we have to include a non-zero penalty

    value_type correction = payoff(x) - u;

    // Constraint already satisfied
    if (correction <= 0.0)
        return 0.0;

    // A. (Courant) quadratic barrier function
    value_type lambda = 1.0e+12;
    value_type penalty = lambda*correction*correction;
    return penalty;
}
```

In general, we have replaced the *differential inequality*:

∂V/∂t ≥ ½ σ² S² ∂²V/∂S² + r S ∂V/∂S − r V  (25.21)

by the *semi-linear* PDE:

$$\frac{\partial V}{\partial t}=\frac{1}{2}\sigma^2S^2\frac{\partial^2V}{\partial S^2}+rS\frac{\partial V}{\partial S}-rV+\lambda g(V,S)=0 \tag{25.22}$$

and this is the equation that we approximate. We choose a large value for $\lambda$. In other words, we carry out a *semi-discretisation* in space and the resulting set of equations is encapsulated in a class:

```cpp
class OdeBlackScholes
{ // Basic ODE class for plain Black Scholes

    std::vector<value_type> mesh;
    double h;

public:
    OdeBlackScholes(std::size_t NX, double meshSize)
        :mesh(std::vector<value_type>(NX+1,0.0)), h(meshSize)
    {
        mesh[0] = 0.0;
        for (std::size_t j = 1; j < mesh.size(); ++j)
        {
            mesh[j] = mesh[j - 1] + h;
        }
    }

    void operator() (const state_type& U, state_type& dUdt,
                     const value_type t)
    {
        double xval, diff, con;

        value_type h2 = 1.0 / (h*h);
        value_type hm1 = 1.0 / (2.0*h);

        // Boundaries

        // Left boundary (j = 1)
        std::size_t index = 1;
        xval = mesh[index];
        dUdt[index]
            = diffusion(xval,t)*h2*(U[index + 1]-2.0*U[index] + bcl(t))
            + 0.5*convection(xval, t)*(U[index + 1] - bcl(t)) / h
            + reaction(xval, t)*U[index]
            + penalty(mesh[index], U[index]);

        // Right boundary (j = J-1)
        index = U.size() - 2;
```

```cpp
xval = mesh[index];
dUdt[index]
    = diffusion(xval,t)*h2*(bcr(t) - 2.0*U[index] + U[index - 1])
    + 0.5*convection(xval, t)*(bcr(t) - U[index - 1]) / h
    + reaction(xval, t)*U[index]
    +penalty(mesh[index], U[index]);

// Interior of domain (1 < j < J-1)
for (std::size_t index = 2; index < U.size() - 2; ++index)
{

    xval = mesh[index];
    diff = diffusion(xval, t)*h2;
    con = convection(xval, t)*hm1;
    dUdt[index] =
        (diff + con) *U[index + 1]
        + (-2.0*diff + reaction(xval, t))*U[index]
        + (diff - con) *U[index - 1]
        + penalty(mesh[index], U[index]);
}
}

void operator () (const state_type& U, const value_type t)
{
    if (t >= T)
    { // To avoid explosion of output at the moment

        // Your code here

    }
}
};

void write_out(const state_type& U, const value_type t)
{

    if (t >= T)
    { // To avoid explosion of output at the moment

        std::cout << "\nTime: " << t << std::endl;
        for (std::size_t j = 0; j < U.size(); ++j)
        {
            std::cout << "[" << j << "," << U[j] << "] ";
        }
    }
}
```
