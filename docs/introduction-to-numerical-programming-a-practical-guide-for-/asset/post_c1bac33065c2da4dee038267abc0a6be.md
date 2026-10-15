
Euler — Euler propagator for systems of first-order ODEs.
EulerPC — Euler predictor–corrector propagator for systems of first-order ODEs.
RungeKutta — Fourth-order Runge–Kutta solver for Cauchy problems for systems of first-order ODEs.
RKadapt — Adaptive ODE solver using step-halving and the Runge–Kutta method.
RKFehlberg — Adaptive ODE solver based on the Runge–Kutta–Fehlberg method.
Euler1 — Euler propagator for a second-order ODE.
EulerCromer1 — Euler–Cromer propagator for a second-order ODE.
Verlet1 — Verlet propagator for a second-order ODE.
Euler2 — Euler propagator for a system of second-order ODEs.
EulerCromer — Euler–Cromer propagator for a system of second-order ODEs.
Verlet2 — 2D velocity Verlet propagator for a single particle.
Verlet — Velocity Verlet propagator for a system of particles in interaction.
EulerCromerQM — Euler–Cromer integrator for the 1D Schrödinger equation.
Numerov — Numerov integrator for the 1D Schrödinger equation.
Propag — Propagates the solution of a second-order ODE on a regular mesh using the Euler–Cromer method.
Shoot — Solves a two-point boundary-value problem for a second-order ODE using the shooting method.
ShootQM — Solves the 1D Schrödinger equation using the shooting method.
Bilocal — Linear bilocal problem solver based on the finite-difference method.

## pde.py

Contains routines for solving partial differential equations.

Poisson0 — Solver for the 2D Poisson equation in Cartesian coordinates with Dirichlet boundary conditions.
PoissonXY — Solver for the 2D Poisson equation in Cartesian coordinates with arbitrary boundary conditions.
Poisson2D — Solver for the 2D Poisson equation in Cartesian coordinates on an irregular domain.
PropagFTCS — Explicit forward-time central-space propagator for the diffusion equation.
PropagBTCS — Implicit backward-time central-space propagator for the diffusion equation.
PropagCN — Crank–Nicolson propagator for the diffusion equation.
PropagDiff — Crank–Nicolson propagator for the diffusion equation with variable diffusion coefficient.
PropagQTD — Crank–Nicolson propagator for the Schrödinger equation based on tridiagonal solver.
PropagQGS — Crank–Nicolson propagator for the Schrödinger equation using the Gauss–Seidel method.
PropagWave — Explicit forward-time central-space propagator for the classical wave equation.

## utils.py

Contains utility routines.

Nint — Returns the nearest integer to its real-type argument.
Sign — Transfers the sign of its second argument onto the absolute value of the first argument.
Magn — Returns the order of magnitude of its argument as a power of 10.
Index — Indexes a numeric sequence by direct insertion

## Appendix E: The Graphics Library
graphlib.py Based on Tkinter

Listing E.1 shows the Python library `graphlib.py` based on Tkinter, which is used for producing runtime graphics throughout the book. The module contains functions for plotting real functions of one variable (`Plot`, `MultiPlot`, and `HistoBin`), as well as of two variables (`Contour`). Functions are also provided for rendering systems of particles as connected spheres (`PlotParticles`) and 3D structures defined by triangular planes (`PlotStruct`).

The module `graphlib.py` uses a series of auxiliary functions, which are included in the module `utils.py`, shown in Listing E.2.

```
# ------------------------------ graphlib.py ------------------------------
# Graphics library based on Tkinter.
# Author: Titus Beu, 2013
# --------------------------------------------------------------------------
from math import *
from utils import *
from tkinter import *

root = Tk()                                      # create Tk root widget
root.title("graphlib v1.0")

#==========================================================================
def MainLoop():                                  # creates Tk event loop
    root.mainloop()

#==========================================================================
def GraphUpdate():                                # updates Tk root widget
    root.update()

#==========================================================================
def GraphInit(nxwin, nywin):       # creates Canvas widget and returns object
    global w, nxw, nyw                          # make canvas object available

    nxw = nxwin; nyw = nywin                     # canvas size
    w = Canvas(root, width=nxw, height=nyw, bg = "white")  # create canvas
    w.pack()                                     # make canvas visible
    return w

#==========================================================================
def GraphClear():                                # deletes content of Canvas widget
    global w, nxw, nyw                          # canvas object and size
    w.delete(ALL)

#==========================================================================
def Limits(xmin, xmax, maxint):
# --------------------------------------------------------------------------
```

```
# Replaces the limits xmin and xmax of a real interval with the limits of
# the smallest extended inteval which includes a number <= maxint of
# subintervals of length d * 10**p, with d = 1, 2, 5 and p integer.
#
# scale - scale factor (10**p)
# nsigd - relevant number of significant digits
# nintv - number of subintervals
#
# Returns: xmin, xmax, scale, nsigd, nintv
#-------------------------------------------------------------------------------
eps = 1e-5                                            # relative precision criterion
xfact = [0.5e0,0.5e0,0.4e0]                            # 0.5*0.5*0.4 = 0.1

if (abs(xmax - xmin) < 10e0*eps*abs(xmax)):
    corrmin = 1e0 - 10e0 * Sign(eps,xmin)
    corr_max = 1e0 + 10e0 * Sign(eps,xmax)
    xmin *= corrmin
    xmax *= corr_max

factor = 1e0/(eps * min(Magn(xmin),Magn(xmax))) if (xmin * xmax) else \        # initial scale factor
    1e0/(eps * max(Magn(xmin),Magn(xmax)))

corrmin = 1e0 + Sign(eps,xmin)                        # corrections
corr_max = 1e0 - Sign(eps,xmax)
for i in range(1,100):                                # multiply iteratively
    xmins = floor(xmin * factor * corrmin)            # factor with xfact[]
    xmaxs = ceil (xmax * factor * corr_max)           # until the no. of
    xnint = abs(xmaxs - xmins)                        # subintervals becomes
    if (xnint <= maxint): break                       # xnint <= maxint
    modi = i % 3
    factor = factor * xfact[modi]

factor = 1e0 / factor                                 # scale factor
xmin = xmins * factor                                 # xmin and xmax
xmax = xmaxs * factor
scale = max(Magn(xmin),Magn(xmax))                    # scale factor
factor = max(abs(xmins),abs(xmaxs))
for i in range(1,modi+1): factor = factor / xfact[i]
nsigd = int(log10(factor) + 1)                        # no. of significant digits
nintv = Nint(xnint)                                   # no. of subintervals

return (xmin, xmax, scale, nsigd, nintv)

#================================================================================
def FormStr(x, scale, nsigd):
#-------------------------------------------------------------------------------
# Formats the number x (with factor scale) to nsigd significant digits
# returning the mantissa in mant[] and the exponent of 10 in expn[].
#
# Returns: mant, expn
#-------------------------------------------------------------------------------
ndigmax = 5                                           # maximum no. of digits
mant = expn = ""

n = Nint(log10(scale))                                # exponent
if ((n < -1) or (n > 3)):
    expn = repr(n)
    x = x / scale                                     # divide x by scale
    n = 0
```

```
n += 1                                          # no. of digits before decimal point
ndig = min(ndigmax, max(nsigd, n))                # total no. of digits
ndec = ndig - n                                   # no. of decimals
x = round(x, ndec)
mant = "{0:{1}:.{2}f}".format(x, ndig, ndec)

return (mant, expn)

#==============================================================================
def Plot(x, y, n, col, sty, fxmin, fxmax, fymin, fymax, xtext, ytext, title):
#------------------------------------------------------------------------------
# Plots a real function of one variable specified by a set of (x,y) points.
# The x and y-domains are extended to fit at most 10 intervals expressible
# as d * 10^p, with d = 1, 2, 5 and p integer.
#
# x[]  - abscissas of tabulation points (x[1] through x[n])
# y[]  - ordinates of tabulation points (y[1] through y[n])
# n    - number of tabulation points
# col  - plot color ("red", "green", "blue" etc.)
# sty  - plot style: 0 - scatter plot, 1 - line plot, 2 - polar plot,
#                3 - drop lines, 4 - histogram
# fxmin - min fractional x-limit of viewport (0 < fxmin < fxmax < 1)
# fxmax - max fractional x-limit of viewport
# fymin - min fractional y-limit of viewport (0 < fymin < fymax < 1)
# fymax - max fractional y-limit of viewport
# xtext - x-axis title; for "None" - axis is not labeled
# ytext - y-axis title; for "None" - axis is not labeled
# title - plot title
#------------------------------------------------------------------------------
    global w, nxw, nyw                               # canvas object and size
    maxintx = maxinty = 10                           # max. number of labeling subintervals

    xmin = min(x[1:n+1]); xmax = max(x[1:n+1])        # domain limits
    ymin = min(y[1:n+1]); ymax = max(y[1:n+1])

    ixmin = Nint(fxmin*nxw); iymin = Nint((1e0-fymin)*nyw)  # viewport limits
    ixmax = Nint(fxmax*nxw); iymax = Nint((1e0-fymax)*nyw)

    if (sty == 2):                                   # polar plot
        xmin = min(xmin, ymin); xmax = max(xmax, ymax)    # make domain square
        xmax = max(abs(xmin), abs(xmax)); xmin = -xmax
        ymin = xmin; ymax = xmax
        if (ixmax-ixmin > iymin-iymax):              # adjust viewport limits
            c = 0.5*(ixmin+ixmax)
            d = 0.5*(iymin-iymax)
            ixmin = c - d; ixmax = c + d
        if (ixmax-ixmin < iymin-iymax):
            c = 0.5*(iymin+iymax)
            d = 0.5*(ixmax-ixmin)
            iymin = c + d; iymax = c - d

    w.create_rectangle(ixmin, iymax, ixmax, iymin)   # draw plot frame

    nfont = min(int((ixmax-ixmin)/60.) + 3, 12)       # font size
    font1 = ("Helvetica", nfont)                    # axis label font
    font2 = ("Helvetica", Nint(1.2*nfont))          # axis title font
    font3 = ("Helvetica", Nint(1.4*nfont))          # plot title font
    if ((ixmax-ixmin) < 3 * (iymin-iymax)):
```
