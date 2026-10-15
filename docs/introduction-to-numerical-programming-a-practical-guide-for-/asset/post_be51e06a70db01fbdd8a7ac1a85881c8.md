
```
ht*(c1*f1[i] + c3*f3[i] + c4*f4[i] + c5*f5[i] + c6*f6[i])       # error estimate
erri = ht*(e1*f1[i] + e3*f3[i] + e4*f4[i] + e5*f5[i] + e6*f6[i])
erri = fabs(erri/yt[i])
if (err < erri): err = erri

f = 1e0                                      # scaling factor for step size
if (err): f = 0.9e0*pow(eps/err,1e0/p)
if (f > 5e0): f = 5e0                       # prevent increase > 5x
ht1 = f * ht                                 # guess for next step size
if (err <= eps): break                       # precision attained: exit
ht = ht1                                     # reduce step size and repeat

if (it > itmax): print("RKFehlberg: max. no. of iterations exceeded !")
for (i in range(1,n+1)): y[i] = yt[i]       # update y with the best solution
return (ht, ht1)
```

As in the case of the RungeKutta routine, we do not actually evaluate the coefficients \(k_i\) themselves, but rather the involved values of the right-hand-side function \(f\), and these are stored in the local arrays f1, f2, f3, f4, f5, and f6. For the rest, the control mechanism of the integration step size is identical with the one implemented in RKadapt.

The exit from the scaling loop of the step size is initiated once the maximum relative error of the solution components, err, drops under the desired relative tolerance eps. Anyway, increases of more than 5 times of the step size are prevented. The particular Runge–Kutta–Fehlberg coefficients coded in RKFehlberg can be readily replaced with the coefficients specific to other embedded adaptive ODE solvers.

As an illustration for the operation of the RKFehlberg solver, let us consider a Cauchy problem for a second-order ODE with a strongly discontinuous coefficient:

$$y'' = f(t)y,\quad y(0)=0,\quad y'(0)=1,$$  (12.53)

$$f(t)=\begin{cases}1, & 0\le t\le 5,\\-100, & t>5.\end{cases}$$

The exact analytic solution can be easily shown to consist of two functionally different restrictions—a rapidly growing hyperbolic sine and a combination of wildly oscillating harmonic functions:

$$y(t)=\begin{cases}\sinh t, & 0\le t\le 5,\\\sinh 5\cos 10(t-5)+\frac{1}{10}\cosh 5\sin 10(t-5), & t>5.\end{cases}$$

It is obvious that a constant integration step size cannot ensure a uniform precision throughout the definition domain. A step size, small enough to cope with the functional discontinuity and reproduce the oscillatory behavior, results in a waste of effort in the hyperbolic part. In such cases, adaptive solvers are definitely the methods of choice. Program 12.7 implements in Func the right-hand sides of the equivalent system of first-order ODEs and repeatedly calls the routine RKFehlberg to advance the solution up to tmax. The propagation loop is supposed to update the trial step size ht with the guess ht1 returned by the preceding call to RKFehlberg. The solution \(y(t)\) is shown in the left panel of Figure 12.4, while the pronounced time dependence of the employed step size is depicted in the right panel. For the same relative tolerance \(\varepsilon=10^{-8}\), the two forms of the solution can be seen to require step sizes differing by more than one order of magnitude.

## Listing 12.7 Application of Adaptive Step Size Control (Python Coding)

```
# Solves a Cauchy problem with adaptive step size control
from math import *
from ode import *

def Func(t, y, f):                     # RHSs of ODEs
    f[1] = y[2]
    f[2] = (1e0 if t < 5e0 else -100e0) * y[1]

# main

y0 = 0e0; dy0 = 1e0                     # initial values
tmax = 10e0                             # time span
ht = 0.01e0                             # step size
eps = 1e-8                              # relative solution precision

n = 2                                   # number of 1st order ODEs
y = [0]*(n+1)                           # solution components

out = open("ode.txt","w")             # open output file
out.write("      t           y           h\n")

t = 0e0
y[1] = y0; y[2] = dy0                    # initial values
out.write("{0:10.5f}{1:10.5f}{2:10.5f}\n".format(t,y[1],ht))

ht1 = ht                               # initial step size guess
while (t+ht <= tmax):                   # propagation loop
    ht = ht1                            # update initial step size with guess
    (ht, ht1) = RKFehlberg(t,ht,eps,y,n,Func)
    t += ht

    out.write("{0:10.5f}{1:10.5f}{2:10.5f}\n".format(t,y[1],ht))

out.close()
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_466_0.png)

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_466_1.png)

FIGURE 12.4 Solution of the Cauchy problem 12.53 using adaptive step size control based on the Runge–Kutta–Fehlberg method (left panel). Time evolution of the employed integration step size (right panel).

## 12.6 Methods for Second-Order ODEs

Cauchy problems for second-order ODEs arise in many areas of applied sciences and engineering, most frequently describing time or space dependences of the continuous quantities of interest. However different may seem two of the prototypical second-order ODEs, namely, Newton’s second law and the 1D time-independent Schrödinger equation, the numerical methods applicable for their solution share many common features.

Let us thus consider the generic Cauchy problem:

d²y/dt² = f(t, y, y')  (12.54)
y(t₀) = y₀,    y'(t₀) = y'₀.  (12.55)

The algorithms developed for solving it typically derive from the Taylor series method (see Section 12.2), with the first derivative y' (often having a well-defined significance within the underlying formalism) being propagated explicitly along with the solution.

Considering two consecutive values of the independent variable, tₘ and tₘ₊₁, separated by h = tₘ₊₁ − tₘ, and starting from the known initial values yₘ ≡ y(tₘ) and y'ₘ ≡ y'(tₘ), the propagation of the solution to tₘ₊₁ can be performed based on the Taylor expansions of y and y', with the second derivative y'' determined directly from the ODE. The relevant equations arranged in algorithmic order read:

y''ₘ = f(tₘ, yₘ, y'ₘ),
yₘ₊₁ = yₘ + h y'ₘ + ½ h² y''ₘ + O(h³),  (12.56)
y'ₘ₊₁ = y'ₘ + h y''ₘ + O(h²).

One defining characteristic of all algorithms built on these equations is that each propagation step requires just a single evaluation of the second derivative from the right-hand side of the ODE. Practical implementations actually use variants of these equations, tuned alternatively for simplicity, precision, or storage efficiency.

The simplest variant is the Euler method, which is the equivalent for second-order ODEs of the approach described in Section 12.3. Euler’s method essentially implies retaining the linear approximations in the propagators of both the position and the velocity:

y''ₘ = f(tₘ, yₘ, y'ₘ),
yₘ₊₁ = yₘ + h y'ₘ + O(h²),  (12.57)
y'ₘ₊₁ = y'ₘ + h y''ₘ + O(h²).

Since it uses only information from tₘ (not also from tₘ₊₁), this scheme is also known as first-point approximation and its obvious advantage is the ease of implementation.

In spite of its appealing simplicity, Euler’s method is hardly recommendable due to its nonnegligible downsides. First, with its O(h) global truncation error, it is the lowest-order solver for second-order ODEs. Second, due to the rapid propagation of the truncation errors, it often yields unstable solutions, especially for oscillatory systems. Third, since it only uses information from tₘ, the propagation from tₘ to tₘ₊₁ is not time reversible (the propagator is not symmetric in t).

The so-called Euler–Cromer method (Cromer 1981) uses the same O(h) approximations of the Taylor series, but, very importantly, it cures the instability of the Euler method. The basic relations are formally obtained by the simple inversion of the equations for y'ₘ₊₁ and yₘ₊₁, and by using in the latter one,

instead of the initial derivative y′_m, the updated value y′_{m+1}: y''_m = f(t_m, y_m, y'_m), y'_{m+1} = y'_m + h y''_m + O(h^2), y_{m+1} = y_m + h y'_{m+1} + O(h^2). (12.58)

In implementations, the preceding evaluation of y'_{m+1} and its subsequent use in y_{m+1} allows for a single program variable to be allocated both for y'_m and y'_{m+1}. Moreover, the use of the updated derivative, thus of information from both t_m and t_{m+1}, proves to bring about a radical improvement in the solution’s stability (Cromer 1981). In terms of the solution’s precision, though, the Euler–Cromer method maintains the same low O(h) order as the original Euler method.

The velocity Verlet method (Swope et al. 1982), considered in the following, belongs to a family of algebraically equivalent O(h^2) algorithms, which includes the original Verlet method (Verlet 1967) and the Leapfrog method (Hockney and Eastwood 1988). In general, these are employed for solving Newton’s equations of motion in molecular dynamics simulations (Rapaport 2004), but may as well be used for solving initial-value problems for other second-order ODEs. The main difference between the Euler/Euler–Cromer and the velocity Verlet algorithms regards the additional retention within the latter of the parabolic terms in the Taylor expansion of the solution. Concretely, the propagated solution may be expressed successively as y_{m+1} = y_m + h y'_m + 1/2 h^2 y''_m + O(h^3) = y_m + h (y'_m + 1/2 h y''_m) + O(h^3) = y_m + h y'_{m+1/2} + O(h^3).

The solution y_{m+1} appears to be propagated linearly from t_m to t_{m+1} based on the derivative y'_{m+1/2} at mid-interval, that is, at t_{m+1/2} = t_m + h/2. From a different perspective, y'_{m+1/2} can be regarded as the average first derivative over the interval [t_m t_{m+1}]. The propagated solution y_{m+1} substituted in the ODE determines the second derivative y''_{m+1} at the interval end, which, in turn, also enables the propagation of the first derivative y'_{m+1/2} up to t_{m+1}.

The algorithmic sequence of propagation formulas of the velocity Verlet method finally takes the form: y'_{m+1/2} = y'_m + 1/2 h y''_m + O(h^2), y_{m+1} = y_m + h y'_{m+1/2} + O(h^3), y''_{m+1} = f(t_{m+1}, y_{m+1}, y'_{m+1/2}), y'_{m+1} = y'_{m+1/2} + 1/2 h y''_{m+1} + O(h^2). (12.59)

Besides ensuring O(h^2) precision (superior by one order over the Euler and Euler–Cromer methods), the velocity Verlet method also stands out by stability and the small storage requirements facilitated by the algorithmic possibility of all quantities to overwrite themselves along the propagation. Nevertheless, an aspect requiring special attention needs to be emphasized. The second derivative y''_{m+1} determined at one step is necessary not only to propagate the first derivative y'_{m+1/2} over the second interval half, from t_{m+1/2} to t_m, but also to advance y'_{m+1} over the first half of the next step, from t_{m+1} to t_{m+3/2}. For this reason, along with y_{m+1} and y'_{m+1}, also, the second derivative y''_{m+1} needs to be saved for being used at the next step.

The implementations of the Euler, Euler–Cromer, and velocity Verlet methods for the solution of initial-value problems for single second-order ODE are presented in Listing 12.8.
