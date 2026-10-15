
```
0.57,0.97,0.15,0.85,"x","P(x)","Neville interpolation");

w.MainLoop();
}
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_332_0.png)

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_332_1.png)

FIGURE 9.10 Lagrange and Neville interpolants (with continuous line) calculated by Programs 9.18 and 9.19. The data points (with squares) sample the function f(x) = 1/x (with dashed line). The error bars represent the estimates provided by Neville’s method. Upper panel uniformly distributed data points along the modeled function; lower panel: equally spaced abscissas of the data points.

## PROBLEM 9.2

Write Python and C/C++ programs using the routine Spline to interpolate a set of n = 6 equally spaced data points sampling the function f(x) = sin x / x in the interval [0, 5π/2].

Evaluate the splines and their first and second derivatives in each of the tabulation subintervals [x_i, x_{i+1}], i = 1, 2, …, n − 1, using their analytical expressions:

S_i(x) = ((A_i x + B_i) x + C_i) x + D_i,
S'_i(x) = (3A_i x + 2B_i) x + C_i,
S''_i(x) = 6A_i x + 2B_i,

and the coefficients A_i, B_i, C_i, and D_i returned by Spline.

Use comparatively *natural* and *clamped* boundaries (which make use of the provided boundary derivatives), by setting `iopt=0` and, respectively, nonzero in the call to Spline. In each case, plot the interpolant along with its first and second derivatives.

For clamped splines, use the exact first derivatives at the tabulation end points ($S'_1(0)=0$, $S'_5(\pi/2)=0$) and notice the sensible improvement of the interpolant in the boundary intervals. Verify that, for the natural splines, the second derivative vanishes at the tabulation end points, whereas for the clamped splines, it is the first derivative that vanishes.

## Solution

The Python implementation is given in Listing 9.20, the equivalent C/C++ version is available as supplementary material (`P09-Spline.cpp`), and the resulting plots are shown in Figure 9.11.

### Listing 9.20  Interpolation Using Cubic Splines (Python Coding)

```
```python
# Interpolation with cubic splines
from modfunc import *
from graphlib import *

def sinc(x): return (sin(x)/x if x else 1e0)

# main

xmin = 0e0; xmax = 5*asin(1e0)                 # tabulation interval: [0,5*pi/2]
n  = 6                                         # number of data points
ni = 100                                       # number of interpolation points
n1 = n + ni; n2 = n + 2*ni; n3 = n + 3*ni; n4 = n + 4*ni       # end indexes
nn = [0]*6                                     # end indexes of plots
col = [""]*6                                   # colors of plots
sty = [0]*6                                    # styles of plots

a = [0]*(n+1); b = [0]*(n+1)                  # spline coefficients
c = [0]*(n+1); d = [0]*(n+1)
x  = [0]*(n+1); y  = [0]*(n+1)                # coordinates of data points
xp = [0]*(n4+1); yp = [0]*(n4+1)              # plotting arrays

nn[1] = n ; col[1] = "black"; sty[1] = 0                    # data points
nn[2] = n1; col[2] = "black"; sty[2] = -1                   # original function
nn[3] = n2; col[3] = "blue" ; sty[3] = 1                    # interpolant
nn[4] = n3; col[4] = "red"  ; sty[4] = -1                   # 1st derivative
nn[5] = n4; col[5] = "green"; sty[5] = -1                   # 1st derivative

h = (xmax-xmin)/(n-1)                                      # generate data points
for i in range(1,n+1):
    xi = xmin + (i-1)*h
    xp[i] = x[i] = xi
    yp[i] = y[i] = sinc(xi)

h = (xmax-xmin)/(ni-1)
for i in range(1,ni+1):
    xi = xmin + (i-1)*h                                      # interpolation arguments
    xp[n3+i] = xp[n2+i] = xp[n1+i] = xp[n+i] = xi             # plotting arguments

GraphInit(1200,600)

#---------------------------------------------------------------- natural splines
Spline(x,y,n,0e0,0e0,0,a,b,c,d,x,y,0)

for i in range(1,ni+1):
```
```
xi = xp[n+i]                                 # interpolation argument
ip = 1
while (ip < n-1 and xi > x[ip+1]): ip += 1      # index of spline

yp[n +i] = sinc(xi)                              # original function
yp[n1+i] = ((a[ip]*xi + b[ip])*xi + c[ip])*xi + d[ip]      # spline
yp[n2+i] = (3*a[ip]*xi + 2*b[ip])*xi + c[ip]      # 1st derivative
yp[n3+i] = 6*a[ip]*xi + 2*b[ip]                   # 2nd derivative

MultiPlot (xp,yp,yp,nn,col,sty,5,10,0e0,0e0,0,0e0,0e0,0,0.07,0.47,0.15,0.85,
"x","S","Spline interpolation - natural splines")
```

```
#------------------------------------------------------------- clamped splines
Spline(x,y,n,0e0,0e0,1,a,b,c,d,x,y,0)
```

```
for i in range(1,n+1):
    xi = xp[n+i]                                 # interpolation argument
    ip = 1
    while (ip < n-1 and xi > x[ip+1]): ip += 1      # index of spline

    yp[n +i] = sinc(xi)                              # original function
    yp[n1+i] = ((a[ip]*xi + b[ip])*xi + c[ip])*xi + d[ip]      # spline
    yp[n2+i] = (3*a[ip]*xi + 2*b[ip])*xi + c[ip]      # 1st derivative
    yp[n3+i] = 6*a[ip]*xi + 2*b[ip]                   # 2nd derivative

MultiPlot (xp,yp,yp,nn,col,sty,5,10,0e0,0e0,0,0e0,0e0,0,0.57,0.97,0.15,0.85,
"x","S","Spline interpolation - clamped splines")

MainLoop()
```

![](img/5c6c126e3d8cf2b3029f4242e9ad2887_334_0.png)

FIGURE 9.11 Interpolation with natural cubic splines (left) and clamped cubic splines (right). The modeled function, f(x) = sin x/x, is sampled in the interval [0, 5π/2] at six equally spaced points. The interpolant is plotted with continuous line, while its derivatives and the original function with dashed lines.

## PROBLEM 9.3

Perform linear regression on the data set (1,0.8), (2,2.1), (3,2.8), (4,4.0) and (5,4.4), and associate with each observation y_i a proportional standard deviation σ_i = 0.15 y_i. Write Python and C/C++ programs

to analyze the data set by calling the function LinFit and apply comparatively the merit functions χ² (Equation 9.41) and S (Equation 9.48).

Plot the data set along with the two regression lines and judge the quality of the fitting procedure based on the uncertainties of the adjusted model parameters a and b.

## Solution

The Python implementation is given in Listing 9.21 and the equivalent C/C++ version is available as supplementary material (P09-LinFit.cpp). The graphical output produced by the program is shown in Figure 9.12.

### Listing 9.21 Linear Fit by the Least-Squares Method (Python Coding)

```
# Linear fit of a model to observed data points
from modfunc import *
from graphlib import *

# main

nn = [0]*4                                 # end-indexes of the 3 plots
col = ['']*4                               # colors of plots
sty = [0]*4                                # styles of plots

n = 5                                      # number of observed data
nfit = 2                                   # number of points plotted from model
n1 = n + nfit; n2 = n + 2*nfit              # end indexes

x = [0]*(n2+1); y = [0]*(n2+1)              # observed data
sigmy = [0]*(n+1)                          # standard deviations of observed data

x[1] = 1e0; y[1] = 0.8e0                    # data points
x[2] = 2e0; y[2] = 2.1e0
x[3] = 3e0; y[3] = 2.8e0
x[4] = 4e0; y[4] = 4.0e0
x[5] = 5e0; y[5] = 4.4e0

iopt = 0                                  # least squares fit: equal errors sigmy
(a, b, sigma, sigmb, chi2) = LinFit(x,y,sigmy,n,iopt)

print("Least squares fit:")
print("a = {0:8.4f} +/- {1:8.4f}".format(a,sigma))
print("b = {0:8.4f} +/- {1:8.4f}".format(b,sigmb))
print("Chi^2 = {0:8.4f}".format(chi2))

h = (x[n]-x[1])/(nfit-1)
for i in range(1,nfit+1):                  # append model points
    x[n+i] = x[1] + (i-1)*h
    y[n+i] = a*x[n+i] + b                  # regression line

for i in range(1,n+1): sigmy[i] = 0.15*y[i]  # generate standard deviations

iopt = 1                                  # Chi-square fit: different errors sigmy
(a, b, sigma, sigmb, chi2) = LinFit(x,y,sigmy,n,iopt)

print("\nChi-square fit:")
print("a = {0:8.4f} +/- {1:8.4f}".format(a,sigma))
print("b = {0:8.4f} +/- {1:8.4f}".format(b,sigmb))
print("Chi^2 = {0:8.4f}".format(chi2))
```
