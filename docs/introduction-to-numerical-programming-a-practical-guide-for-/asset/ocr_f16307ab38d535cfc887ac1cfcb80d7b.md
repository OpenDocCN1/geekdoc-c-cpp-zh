![](bbox=[0.262, 0.089, 0.741, 0.35])

**FIGURE 3.10** Plots of two functions on the same graph, created with routine `MultiPlot`.

# **Listing 3.11** Contour Plot of the Function $\cos x^2 + \cos y^2$ Using Routine `Contour` (Python Coding)

```
```python
# Contour plot of a function of two variables
from math import *
from graphlib import *


def Func(x, y):                                      # function to be plotted
    return cos(x*x) + cos(y*y)

# main

ymin = -pi; xmax = pi; ymin = -pi; ymax = pi             # domain boundaries
nx = 41; ny = 41                                        # number of mesh points

u = [[0]*(ny+1) for j in range(nx+1)]                   # array of function values

hx = (xmax-xmin)/(nx-1)                                 # x-mesh spacing
hy = (ymax-ymin)/(ny-1)                                 # y-mesh spacing
for i in range(1,nx+1):
    x = xmin + (i-1)*hx                                  # x-mesh point
    for j in range(1,ny+1):
        y = ymin + (j-1)*hy                              # y-mesh point
        u[i][j] = Func(x,y)                              # function value

umin = umax = u[1][1]                                   # minimum and maximum of function
for i in range(1,nx+1):
    for j in range(1,ny+1):
        if (u[i][j] < umin): umin = u[i][j]
        if (u[i][j] > umax): umax = u[i][j]

GraphInit(800,800)                                      # create canvas

Contour(u,nx,ny,xmin,xmax,ymin,ymax,umin,umax,           # create contour plot
        0.15,0.85,0.15,0.85,"x","y","cos(x*x) + cos(y*y)")

MainLoop()                                              # enter Tkinter event loop
```
```