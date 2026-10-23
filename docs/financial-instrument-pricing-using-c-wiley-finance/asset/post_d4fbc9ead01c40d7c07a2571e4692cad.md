
In this case the time variable is still continuous. We can discretise it in time using the BTCS (implicit Euler) scheme:

```
\frac{U(t + k) - U(t)}{k} = A U(t + k)
```

or

```
(I - kA)U(t + k) = U(t)
```

or

```
U(t + k) = (I - kA)^{-1} U(t).
```

This is now a first-order approximation to the exact solution. As with the previous examples we can define two approximate solutions on meshes of size k and 2k to get a second-order accurate solution extrapolation algorithm:

```
U^{(1)}(t + 2k) = (I - 2kA)^{-1} U(t)
U^{(2)}(t + 2k) = (I - kA)^{-1} (I - kA)^{-1} U(t)
U(t + 2k) = 2 * U^{(2)} - U^{(1)}.
```

Richardson extrapolation of the BTCS has a number of advantages:

- It is second-order accurate in time.
- It is an L-stable method (Lawson and Morris, 1978) which makes it suitable for stiff equations and equations with discontinuous initial conditions. The Crank–Nicolson method is only A-stable and it can produce oscillations. A workaround is to apply the method described in Rannacher (1984) in which the BTCS scheme is employed for the first few time steps and then Crank–Nicolson is used when initial oscillations have subsided.
- It can be parallelised; the schemes on mesh size k and k/2 can run in parallel.

We shall discuss the implementation of this method in Chapter 21.

## 20.10 SUMMARY AND CONCLUSIONS

In this chapter we have introduced one-factor PDEs and we defined how they are incorporated into an IBVP that we then approximate using the finite difference method. We have attempted to give an overview of major mathematical and numerical topics that need to be understood before designing the related algorithms and their subsequent implementation in C++. In particular, in Section 20.6 we proposed 18 attention points that you should be acquainted with when working with FDM. For a more detailed account of the finite difference method, see Duffy (2006).

## 20.11 EXERCISES AND PROJECTS

1. (Kinds of PDEs in Computational Finance, Initial Investigations and Small Project)
One-factor PDEs are common in computational finance, for example:

- CIR (see Cox, Ingersoll and Ross, 1985).
- CEV (see Beckers, 1980).
- Hull–White and extended Vasicek models (see Hull and White, 1996).

Answer the following questions:

- a) Determine the coefficients of the PDEs in these cases (see equation (20.13)).
- b) Can you change the independent variable to simplify the PDE in some way (see Section 20.3)? What is the range of values that the underlying variable takes before and after a change of variable?
- c) PDEs are usually defined on infinite or semi-infinite intervals. Discuss the use of domain truncation and domain transformation to reduce these PDEs to a bounded domain. Which transformations in Section 20.3.4 would be good candidates?
- d) Based on part c), determine which boundary conditions to apply based on heuristic reasoning, Fichera theory or Feller theory. In particular, which boundaries need boundary conditions and which boundaries do not?

2. (Quiz: Crank Nicolson Method)
Which of the following statements is true regarding the Crank–Nicolson method?

- a) It is second-order accurate in time.
- b) It uses second-order divided differences in space.
- c) It is a monotone scheme.
- d) It leads to a tridiagonal matrix system when applied to equation (20.13).

3. (Choice of Domain Transformer)
In this exercise we discuss the applicability of domain transformations similar to that in equation (20.24), namely:

y = tanh αx (Case 1) and y = 1 / (1 + αx) (Case 2).

a) Verify the following:

x = (1 / 2α) log((1 + y)/(1 - y)) = log((1 + y)/(1 - y))^{1/2α}
 dy/dx = α(1 - y²)
 ∂u/∂x = α(1 - y²) ∂u/∂y
 ∂²u/∂x² = α²(1 - y²) ∂/∂y ((1 - y²) ∂u/∂y)
for Case 1 and
x = (1 - y)/(αy), dy/dx = -αy²
∂u/∂x = -αy² ∂u/∂y
∂²u/∂x² = α²y² ∂/∂y (y² ∂u/∂y)

for Case 2. In the latter case we note that the mapping of the semi-interval is to the interval (1, 0), that is the end points are crossed! Case 2 is popular in interest-rate applications.

b) Determine the coefficients of the transformed PDE (as in equation (20.13)) when applying both of these transformations to the one-factor Black–Scholes PDE. Which transformed PDE is more amenable to the finite difference method?

# 4. (Domain Transformation for Infinite Intervals)

Consider the following partial differential equations for the one-dimensional wave and heat equations on an infinite interval:

∂u/∂t + a ∂u/∂x = 0,    −∞ < x < ∞,    t > 0,
∂u/∂t = a² ∂²u/∂x²,    −∞ < x < ∞,    t > 0.

Answer the following questions:

a) Transform these PDEs to PDEs on the interval [−1, 1] by using the transformations:

y = tanh αx
y = coth αx.

Compare the forms of the PDEs resulting from these transformations.

b) Compute the Fichera function for each PDE in part a) of this exercise. What are the resulting boundary conditions?

c) Apply ADE to each of the transformed PDEs. Compare the approach with the Crank–Nicolson method.

# 5. (Solving Two-Point Boundary Value Problems, Non-trivial Project)

We examine the example in Section 20.7.1 as preparation for later chapters. We focus attention on the TPBVP defined by system (20.50) and we analyse it from various perspectives. Answer the following questions:

a) Approximate system (20.50) using a centred difference scheme on a constant mesh. The scheme’s code should be flexible enough so as to accommodate the exponential fitting method in scheme (20.51) and the classical finite difference scheme with a fitting factor equal to 1 (you may need to use a mixin method or a function object to achieve this level of flexibility).

b) Set up the tridiagonal system of equations from part a) and solve it using the Thomas and Double Sweep algorithms. Do you get the same answers in each case?

c) Prove that the matrix corresponding to the fitting scheme is monotone for all values of the diffusion and convection terms. In the case of the classical finite difference schemes with centred differencing in space, what are the constraints on the constant mesh size in order for the matrix to be monotone?

d) Consider the case of small diffusion and/or large convection for both schemes. Do you get correct answers?

e) We employ Richardson extrapolation on the classical finite difference scheme to improve accuracy from second order to fourth order (Keller, 1968). To this end, let

$u_{2j}(h/2)$ and $u_j(h)$, $j=0,\ldots,J$ be the finite difference solutions on the meshes $h/2$ and $h$, respectively. Now construct the array:

$$\bar{u}_j=\frac{4}{3}u_{2j}(h/2)-\frac{1}{3}u_j(h)\qquad 0\leq j\leq J.$$

Verify by numerical experiment that it is a fourth-order approximation to the exact solution.

- **f)** Use first-order upwinding as in equation (20.47). Is the resulting matrix monotone? Can you reproduce the numerical results for this scheme as reported in Section 20.7.1?
- **g)** Convert system (20.50) to conservative form and approximate it using the finite difference method.
- **h)** We now return to Chapter 13 by solving the heat equation using Rothe’s method. The *semi-discrete system* of ODEs will be a special case of the following equation that uses implicit Euler in time:

$$-\frac{u^{n+1}-u^n}{\Delta t}+\sigma(x,t_{n+1})\frac{d^2u^{n+1}}{dx^2}+\mu(x,t_{n+1})\frac{du^{n+1}}{dx}+b(x,t_{n+1})u^{n+1}=f(x,t_{n+1}),$$

$$0\leq n\leq N-1.$$

Implement the scheme in C++ using explicit Euler (for convenience) as the approximation to the time derivative. The focus is on creating an algorithm that can easily be mapped to C++. The algorithm will need to implement the time-marching aspect of the problem.

## CHAPTER 21

## Software Framework for One-Factor Option Models

### 21.1 INTRODUCTION AND OBJECTIVES

In this chapter we concentrate on implementing the algorithms that describe the finite difference schemes from Chapter 20. We use a combination of styles that C++ has to offer to show what is possible. Chapter 20 deals with the mathematics of the problem and associated numerical methods, whereas this chapter focuses on how to map the algorithms to C++. There is thus a clear separation of concerns. More precisely, the goals in this chapter are:

- To create a seamless mapping from FD algorithms to C++, thus helping us to create code that is built to be maintained and extended. We achieve this end by using system decomposition methods and design patterns.
- To experiment with a range of FD schemes (some of which are new in finance) and determine how stable and accurate they are.
- Having determined that a scheme is to our liking, to optimise the code by modifying the design or the code in some way in order to improve the performance.

We discuss a number of design and coding styles to satisfy the first two goals. We then measure the run-time performance of the code to determine whether it satisfies the third goal.

The skills developed in this chapter can be applied to a range of applications. We make this claim based on how we designed problems in Chapter 9. The key issues are to decide what the initial high-level architecture is going to be and how we design classes, class hierarchies and polymorphic functions.

In Chapters 22 and 23 we discuss how to price other kinds of one-factor and two-factor options problems as well as extending the software to suit new requirements.

### 21.2 A SOFTWARE FRAMEWORK: ARCHITECTURE AND CONTEXT

We examine linear convection–diffusion–reaction PDEs of non-conservative type and their approximation by finite difference schemes. The initial system layout is shown in Figure 21.1
