
To be more specific: we write a try-catch-block that starts with a statement which we expect to throw a certain exception. After that statement we throw an exception of type missing_exception. At the end of the block we only catch the expected exception type and as recovery action we just celebrate our success by printing a sufficiently glorious message. Any other exception—in particular missing_exception—will not be caught and terminates the program. Our test program is thus only successful when the statement in question throws the expected exception.

Motivated readers can go a little step further and implement a generic exception test that takes the expected exception type as template argument (not deduced but explicitly declared in the call) and a nullary function object that is just called in the try-catch-block. Obviously we will often create this nullary function object with a lambda. This is a very useful testing tool that the author uses frequently in his own software.

### 6.7.5 Clone Function

Write a CRTP class for a member function named clone() that copies the current object—like the Java function clone. Consider that the return type of the function must be the one of the cloned object.

## Chapter 7
Scientific Projects

> "The difference between theory and practice is larger in practice than in theory."
> —Tilmar König

In the preceding chapters, we focused primarily on language features of C++ and how we can best apply them to relatively small study examples. This last chapter should give you some ideas for how to build up larger projects. The first section (§7.1) from the author’s friend Mario Mulansky deals with the topic of interoperability between libraries. It will give you a look behind the curtain at odeint: a generic library that seamlessly inter-operates with several other libraries in a very tight fashion. Then we will provide some background on how executables are built from many program sources and library archives (§7.2.1), how tools can support this process (§7.2.2), and how program sources are appropriately distributed over multiple files (§7.2.3). Finally, we’ll give you a brief introduction into modules.

### 7.1 Implementation of ODE Solvers

*Written by Mario Mulansky*

In this section we will go through the major steps for designing a numerical library. The focus here is not to provide the most complete numerical functionality, but rather to arrive at a robust design that ensures maximal generality. As an example, we will consider the numerical algorithms for finding the solution of *Ordinary Differential Equations* (ODEs). In the spirit of Chapter 3, our aim is to make the implementation as versatile as possible by using generic programming. We start by briefly introducing the mathematical background of the algorithms followed by a simple, straightforward implementation. From this, we will be able to identify individual parts of the implementation and one by one make them exchangeable to arrive at a fully generic library. We are convinced that after studying this detailed example of a generic library design, the reader will be able to apply this technique to other numerical algorithms as well.

### 7.1.1 Ordinary Differential Equations

Ordinary differential equations are a fundamental mathematical tool to model physical, biological, chemical, or social processes and are one of the most important concepts in science or engineering. Except for a few simple cases, the solution of an ODE cannot be found with analytical methods, and we have to rely on numerical algorithms to obtain at least an approximate solution. In this chapter, we will develop a generic implementation of the Runge-Kutta-4 algorithm, a general-purpose ODE solver widely used due to its simplicity and robustness.

Generally, an ordinary differential equation is an equation containing a function x(t) of an independent variable t and its derivatives x', x'', ...:

```
F(x, x_t, x', ..., x^{(n)}) = 0. (7.1)
```

This is the most general form, including implicit ODEs. However, here we will only consider explicit ODEs, which are of the form x^{(n)} = f(x, x', x'', ..., x^{(n-1)}) and are much simpler to address numerically. The highest derivative n that appears in the ODE is called the order of the ODE. But any ODE of order n can be easily transformed into an n-dimensional ODE of the first order [28]. Therefore, it is sufficient to consider only first-order differential equations where n = 1. The numerical routines presented later will all deal with initial value problems (IVPs): ODEs with a value for x at a starting point x(t = t_0) = x_0.

Thus, the mathematical formulation of the problem that will be numerically addressed throughout the following pages is:

```
\frac{d}{dt}\vec{x}(t) = \vec{f}(\vec{x}(t), t), \vec{x}(t = t_0) = \vec{x}_0. (7.2)
```

Here, we use the vector notation \(\vec{x}\) to indicate that the variable \(\vec{x}\) might be a more-dimensional variable. Typically, the ODE is defined for real-valued variables, i.e., \(\vec{x} \in \mathbb{R}^N\), but it is also possible to consider complex-valued ODEs where \(\vec{x} \in \mathbb{C}^N\). The function \(\vec{f}(\vec{x}, t)\) is called the right-hand side (RHS) of the ODE. The most simple physical example for an ODE is probably the *Harmonic Oscillator*, i.e., a point mass connected to a spring. Newton's equation of motion for such a system is:

```
\frac{d^2}{dt^2}q(t) = \omega_0^2 q(t), \quad (7.3)
```

where \(q(t)\) denotes the position of the mass and \(\omega_0\) is the oscillation frequency. The latter is a function of the mass \(m\) and the stiffness of the spring \(\omega_0 = \sqrt{k/m}\). This can be brought into form (7.2) by introducing \(p = dq/dt\), using \(\vec{x} = (q, p)^T\) and defining some initial conditions, e.g., \(q(0) = q_0, p(0) = 0\). Using the shorthand notation \(\dot{\vec{x}} := d\vec{x}/dt\) and omitting explicit time dependencies, we get:

```
\dot{\vec{x}} = \vec{f}(\vec{x}) = \begin{pmatrix} p \\ -\omega_0^2 q \end{pmatrix}, \quad \vec{x}(0) = \begin{pmatrix} q_0 \\ 0 \end{pmatrix}. \quad (7.4)
```

Note that \(\vec{f}\) in Eq. (7.4) does not depend on the variable \(t\), which makes Eq. (7.4) an *Autonomous* ODE. Also note that in this example the independent variable \(t\) denotes the time and \(\vec{x}\) a point in phase spaces, hence the solution \(\vec{x}(t)\) is the *Trajectory* of the harmonic oscillator. This is a typical situation in physical ODEs and the reason for our choice of variables \(t\) and \(\vec{x}\).^1

1. In mathematics, the independent variable is often called x and the solution is y(x).

For the harmonic oscillator in Eq. (7.4), we can find an analytic solution of the IVP: \(q(t) = q_0 \cos \omega_0 t\) and \(p(t) = -q_0 \omega_0 \sin(\omega_0 t)\). More complicated, non-linear ODEs are often impossible to solve analytically, and we have to employ numerical methods to find an approximate solution. One specific family of examples is systems exhibiting *Chaotic Dynamics* [52], where the trajectories cannot be described in terms of analytical functions. One of the first models where this has been explored is the so-called Lorenz system, a three-dimensional ODE given by the following equations for \(\vec{x} = (x_1, x_2, x_3)^T \in \mathbb{R}^3\) :

```
\dot{x}_1 = \sigma(x_2 - x_1)
\dot{x}_2 = Rx_1 - x_2 - x_1x_3 \quad (7.5)
\dot{x}_3 = x_1x_2 - bx_3,
```

where \(\sigma, R, b \in \mathbb{R}\) are parameters of the system. Figure 7-1 depicts a trajectory of this system for the typical choice of parameters \(\sigma = 10, R = 28\), and \(b = 10/3\). For these parameter values the Lorenz system exhibits a so-called _Chaotic Attractor_, which can be recognized in Figure 7-1.

Although such a solution is impossible to find analytically, there are mathematical proofs regarding its _existence_ and _uniqueness_ under some conditions on the RHS \(\vec{f}\), e.g., the Picard-Lindelöf theorem, which requires \(\vec{f}\) to be Lipschitz-continuous [68]. Provided that this condition is fulfilled and a unique solution exists—as is the case for almost all practical problems—we can apply an algorithmic routine to find a numerical approximation of this solution.

### 7.1.2 Runge-Kutta Algorithms

The most common general-purpose schemes for solving initial value problems of ordinary differential equations are the so-called _Runge-Kutta_ (RK) methods [28]. We will focus on the _explicit_ RK schemes as those are easier to implement and well suited for GPUs. They are a family of iterative one-step methods that rely on a temporal discretization to compute an approximate solution of the IVP. Temporal discretization means that the approximate solution is evaluated at time points \(t_n\). So we use \(\vec{x}_n\) for the numerical approximation of the solution \(x(t_n)\) at time \(t_n\). In the simplest but most frequently used case of an equidistant discretization with a constant step size \(\Delta t\), one writes for the numerical solution:
