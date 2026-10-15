# Listing 9.5 Interpolation Using Neville’s Method (Python Coding)

```
# Interpolation by Neville’s algorithm
from modfunc import *

# main

n = 8                                         # number of data points
ni = 50                                       # number of interpolation points

x = [0]*(n+1)                                 # data points
y = [0]*(n+1)

x[1] = 0.15; x[2] = 0.2; x[3] = 0.3; x[4] = 0.5       # data points:
x[5] = 0.8 ; x[6] = 1.1; x[7] = 1.4; x[8] = 1.7       # f(x) = 1/x
for i in range(1,n+1): y[i] = 1e0/x[i]

out = open("interpol.txt","w")                     # open output file
out.write("      x            y            xi            yi            err\n")
h = (x[n]-x[1])/(ni-1)
for i in range(1,ni+1):
    xi = x[1] + (i-1)*h                             # interpolation argument
    (yi,err) = Neville(x,y,n,xi)                    # interpolant value
    if (i <= n):
        out.write("{0:12.3e}{1:12.3e}{2:12.3e}{3:12.3e}{4:12.3e}\n".format(x[i],y[i],xi,yi,err))
    else:
        out.write("{0:36.3e}{1:12.3e}{2:12.3e}\n".format(xi,yi,err))
out.close()
```

![](bbox=[0.28, 0.56, 0.77, 0.78])

FIGURE 9.3 Plot of the Neville interpolant and the associated error bars for a case of spurious oscillations. The interpolated data sample the function f(x) = 1/x.

# 9.4 Cubic Spline Interpolation

As illustrated by the applications presented in the previous two sections, the major drawback of the Lagrange polynomial, employed as single interpolant over the entire range of tabulated data, is the