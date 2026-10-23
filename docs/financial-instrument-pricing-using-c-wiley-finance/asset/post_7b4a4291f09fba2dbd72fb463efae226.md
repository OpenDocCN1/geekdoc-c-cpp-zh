
Let B be a region of n + 1-dimensional space and let f be continuously differentiable with respect to t and with respect to all the components of y at all points of B. We assume that the following inequalities hold:

$$\left|\frac{\partial f}{\partial y_j}(t,y)\right| \le K \text{ for some } K > 0 \quad j = 1,\dots,n \tag{24.25}$$

and

$$|f(t,y)| \le M \text{ for some } M > 0. \tag{24.26}$$

## Theorem 24.2

Let f and $\frac{\partial f}{\partial y_j} (j = 1,\dots,n)$ be continuous in the box $B = \{(t,y) : |t - t_0| \le a, |y - \eta| \le b\}$ where $a$ and $b$ are positive numbers, satisfying the bounds (24.25) and (24.26) for $(t,y)$ in $B$. Let $\alpha$ be the smaller of the numbers $a$ and $b/M$ and define the successive approximations:

$$\phi_0(t) = \eta$$ $$\phi_n(t) = \eta + \int_{t_0}^{t} f(s, \phi_{n-1}(s)) ds, n \ge 1. \tag{24.27}$$

Then the sequence $\{\phi_j\}$ of successive approximations $(j \ge 0)$ converges (uniformly) on the interval $|t - t_0| \le a$ to a solution $\phi(t)$ of (24.24), satisfying the initial condition $\phi(t_0) = \eta$.

The method (24.27) is called the Peano iterative method and it is used to prove existence of the solution of systems of ODEs (24.24). It is mainly of theoretical value as it should not necessarily be seen as a practical way to construct a solution. On the other hand, it is a useful exercise to construct the sequence of iterates in equation (24.27) for some simple (mostly scalar linear) cases.

## 24.5.1 A Test Case

We take the autonomous nonlinear scalar ODE:

$$y' = f(y) = y^2, y(t_0) = a \tag{24.28}$$

whose solution is given by:

$$y(t) = \frac{a}{1 - a(t - t_0)}. \tag{24.29}$$

universal function wrappers to achieve the same end in a more elegant way. We have decided to use `std::vector` as the underlying array structure. In a later version we could take a more generic approach, including one that also supports `std::array`.

The two classes of functions that we support in this chapter are real-valued and vector-valued functions. We reduce the scope by focusing on double but it can easily be generalised to other arithmetic types. The data types have aliases to make client code more readable:

```
using RealValuedFunction = std::function
        <double (double x, const std::vector<double>& y)>;

using VectorValuedFunction
        = std::vector< RealValuedFunction >;
```

In other words, RealValuedFunction maps arrays to scalars while VectorValuedFunction is an array of RealValuedFunction instances. The first example is:

```
auto f = [](double t, const std::vector<double>& y)
    { return t + y[0]*(1.0 - y[1]); };

double t = 1.0;
std::vector<double> y(2); y[0] = 0.5; y[1] = 0.5;
RealValuedFunction rvf = f;
std::cout << "Real-valued function: " << rvf(t, y) << '\n';
```

The second example comes from equation (24.51), as we shall see in Section 24.6.6:

```
double lambda1 = -100.1; double lambda2 = -0.1;
double a = (lambda1 + lambda2) / 2; double b = (lambda1 - lambda2) / 2;
VectorValuedFunction func(2);

// Component functions of fun
RealValuedFunction f1 = [=](double x, std::vector<double> y)
        { return a*y[0] + b*y[1]; };
RealValuedFunction f2 = [=](double x, std::vector<double> y)
        { return b*y[0] + a*y[1]; };
func[0] = f1; func[1] = f2;
```

This approach is similar to that taken in the Boost C++ *odeint* library that we shall discuss in Chapter 25.

We have written some code to compute the *max norm* of an array and the maximum distance between two arrays. These *utility functions* are useful when employing iterative methods such as the predictor–corrector method when we wish to test for convergence, for example:

```
// Utilities
double LInfinityNorm(const std::vector<double>& arr)
{
```

where:

k₁ = f(t, y)
k₂ = f(t + h/2, y + ½ h k₁)
k₃ = f(t + h/2, y + ½ h k₂)
k₄ = f(x + h, y + h k₃).

Other methods are:

## Second-order Ralston method:

yₙ₊₁ = yₙ + ¼(k₁ + 3k₂)
k₁ = h f(tₙ, yₙ)    (24.34)
k₂ = h f(tₙ + 2h/3, yₙ + 2k₁/3).

## Heun’s (improved Euler) method:

ỹₙ₊₁ = yₙ + h f(tₙ, yₙ)
yₙ₊₁ = yₙ + h/2 [f(tₙ, yₙ) + f(tₙ₊₁, ỹₙ₊₁)].    (24.35)

This is a predictor–corrector method that also has applications to stochastic differential equations.

In general, explicit Runge–Kutta methods are unsuitable for stiff ODEs.

## 24.6.3 Richardson Extrapolation Methods

Extrapolation procedures are usually applied to partial differential equations but they can also be applied to Runge–Kutta methods for ODE systems. Let us assume that we are using a Runge–Kutta method to approximate the solution of system (24.24). Then on meshes of size h and h/2 we have the following error estimates:

yʰ = y + M hᵖ⁺¹ + O(hᵖ⁺²)
yʰ/² = y + M (h/2)ᵖ⁺¹ + O(hᵖ⁺²).    (24.36)

In (24.36) the constant M is independent of h but depends on y.

Some basic mathematics allows us to improve the accuracy. We define the mesh function wʰ/² by:

wʰ/² = [2ᵖ⁺¹ uʰ/² − uʰ] / [2ᵖ⁺¹ − 1] = u + O(hᵖ⁺²).    (24.37)

For example, extrapolation can be applied to the Ralston method (24.34) in the case ρ = 1.

## 24.6.4 Embedded Runge–Kutta Methods

These are Runge–Kutta methods that contain another method and together they produce an estimate of the local truncation error of a single Runge–Kutta step. Popular embedded methods are Fehlberg, Cash–Karp (Cash and Karp, 1990) and Dormand–Prince, which are supported in the Boost C++ odeint library. In particular, the Cash–Karp method is suitable for ODEs having solutions with sharp fronts or discontinuities where a low-order solution often has very good accuracy while a higher-order solution has very poor accuracy.

## 24.6.5 Implicit Runge–Kutta Methods

The Runge–Kutta method (24.33) is explicit in the sense that all unknown terms are on the left-hand side of the equations and all terms on the right-hand side are known. Thus, the solution can be computed without the need to solve a matrix or nonlinear system. Implicit methods do not enjoy this feature.

It can be shown that the solution of system (24.24) satisfies the nonlinear Volterra integral equation of the second kind (Haaser and Sullivan, 1991) defined by:

y(t) = y(t₀) + ∫ₜ₀ᵗ f(s, y(s)) ds,   t ∈ I   (24.38)

where I is some interval.

We can use the mean-value theorem for integrals (Widder, 1989) to show that there is a point (t̃, ỹ), t₀ < t̃ < t, y(t₀) < ỹ < y(t) such that:

y(t) = y(t₀) + h f(t̃, ỹ)   (24.39)

where h = t − t₀ or in parametric form:

y(t) = y(t₀) + h f(t₀ + θ h, y(t₀) + ψ (y(t) − y(t₀))),   0 ≤ θ, ψ ≤ 1.   (24.40)

Some examples are the implicit Euler method θ = ψ = 1:

y(t) = y(t₀) + h f(t, y(t)), h = t − t₀   (24.41)

We use quadratic interpolation to produce the scheme:

$$y\left(t_0+\frac{2}{3}h\right)\approx\frac{5}{9}y(t_0)+\frac{4}{5}y(t)+\frac{2}{9}hf\left(t_0,y(t_0)\right). \tag{24.44}$$

resulting in the Hammer and Hollingsworth scheme:

$$\begin{aligned}
k_1 &= f(t_0,y_0),\\
k_2 &= f\left(t_0+\frac{2}{3}h,t_0+\frac{h}{3}(k_1+k_2)\right),\\
y_1 &= y(t_0)+\frac{h}{4}(k_1+3k_2).
\end{aligned} \tag{24.45}$$

A detailed discussion of implicit and semi-implicit methods can be found in Lambert (1991). These methods are expensive to implement and they cannot rival predictor–corrector or explicit Runge–Kutta methods when the problem to be solved is not stiff.

## 24.6.6  Stiff ODEs: An Overview

What is a *stiff* ODE? Before we define the term, let us give some examples of *nasty* ODEs; that is, ODEs that cause problems for standard finite difference schemes.

The presence of different time scales in ODEs leads to a number of challenges when approximating them using standard finite difference schemes. In particular, schemes such as explicit and implicit Euler, Crank–Nicolson and predictor–corrector do not approximate these systems well, unless a prohibitively small time step is used. Let us take the example (Dahlquist and Björck, 1974):

$$\frac{dy}{dt}=100(\sin t-y),\quad y(0)=0 \tag{24.46}$$

with exact solution:

$$y(t)=\frac{\sin t-0.01\cos t+0.01e^{-100t}}{1.0001}. \tag{24.47}$$

This is a stiff problem because of the different time scales, as can be seen by the presence of the exponential term (quickly decaying) in the solution. The other terms do not decay as quickly and they represent long-term behaviour.

We carried out an experiment using the explicit Euler method and we had to divide the interval [0, 3] into 1.2 million subintervals in order to achieve accuracy to three decimal places. The implicit Euler and Crank–Nicolson methods are not much better.

We now take the example of the following 2×2 systems (Lambert, 1991):

$$\begin{aligned}
\frac{dy_1}{dt} &= 2y_1+y_2+2\sin x,\\
\frac{dy_2}{dt} &= y_1-2y_1+2(\cos x-\sin x),\\
y_1 &= 2,\ y_2(0)=3.
\end{aligned} \tag{24.48}$$
