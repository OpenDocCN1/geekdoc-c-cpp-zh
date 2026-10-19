in (8.13) is

y(t) = \frac{a}{1 + b e^{-\lambda t}} \quad (8.15)

(which you can verify by substitution), things would be amiss if we tried to obtain a more general solution by adding together two such solutions:

y_1(t) = \frac{a}{1 + b e^{-\lambda t}} + \frac{a'}{1 + b' e^{-\lambda t}} \quad (8.16)

(which you can verify by substitution).

# Initial and boundary conditions

The general solution of a first-order differential equation always contains one arbitrary constant. The general solution of a second-order differential equation contains two such constants, and so forth. For any specific problem, these constants are fixed by the initial conditions. For a first-order equation, the sole initial condition may be the position y(t) at some time. For a second-order equation, the two initial conditions may be the position and velocity at some time. Regardless of how powerful the hardware and software that you utilize, mathematics remains valid, and so you must know the initial conditions in order to solve the problem uniquely.

In addition to the initial conditions, it is possible to further restrict the solutions of differential equations. One such way is by boundary conditions that constrain the solution to have fixed values at the boundaries of the solution space. Problems of this sort are called eigenvalue problems, and they are so demanding that solutions do not always exist, and even when they do exist, a trial-and-error search may be required to find them. In Chapter 9, we discuss how to extend the techniques of the present unit to boundary-value problems.

# 8.4

# Dynamic Form for ODEs (Theory)

A standard form for ODEs, which has found proven to be useful in both numerical analysis (Press et al., 1994) and classical dynamics (Scheck, 1994; Tabor, 1989; José and Salatan, 1998), is to express ODEs of any order as N simultaneous first-order ODEs in the N unknowns y^{(0)}–y^{(N-1)}:

\frac{dy^{(0)}}{dt} = f^{(0)}(t, y^{(i)}) , \quad (8.17)

\frac{dy^{(1)}}{dt} = f^{(1)}(t, y^{(i)}) ,

\ddots \quad (8.18)

\frac{dy^{(N-1)}}{dt} = f^{(N-1)}(t, y^{(i)}) , \quad (8.19)