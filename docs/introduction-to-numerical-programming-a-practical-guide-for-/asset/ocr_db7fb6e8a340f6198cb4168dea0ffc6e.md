# Listing 3.10 Plotting Two Functions with the Routine MultiPlot (Python Coding)

```
# Plots two functions of one variable on the same graph
from math import *
from graphlib import *

def Func(x):                     # function to be plotted
    return pow(x,3) * exp(-x)

# main

nplot = 2                        # number of plots
n = [0]*(nplot+1)                # ending indexes of plots
col = [""]*(nplot+1)            # plot colors
sty = [0]*(nplot+1)              # plot styles

xmin = -0.82; xmax = 7.8         # limits of plotting interval
n1 = 30                          # number of points for set 1
n2 = 50                          # number of points for set 2

x = [0]*(n1+n2+1)                # coordinates
y = [0]*(n1+n2+1)

h = (xmax-xmin)/(n1-1)           # spacing for set 1
for i in range(1,n1+1):
    x[i] = xmin + (i-1)*h        # arguments
    y[i] = Func(x[i])            # function values

h = (xmax-xmin)/(n2-1)           # spacing for set 2
for i in range(1,n2+1):
    x[n1+i] = xmin + (i-1)*h     # arguments
    y[n1+i] = Func(x[n1+i]) * 0.9  # function values

GraphInit(800,600)               # create canvas

n[1] = n1  ; col[1] = "red"; sty[1] = 0   # scatter plot
n[2] = n1+n2; col[2] = "blue"; sty[2] = 1 # line plot
MultiPlot(x,y,y,n,col,sty,nplot,10,0e0,0e0,0,0e0,0e0,0,
          0.15,0.95,0.15,0.85,"x","y","Multiple plots")  # create plots

MainLoop()                       # enter Tkinter event loop
```

The routine Contour creates the contour plot of a real function of two variables, defined in the domain [xmin,xmax] × [ymin,ymax] and specified by its values z[i][j] at the nx × ny nodes of a regular grid. The representation is confined to z-values between zmin and zmax. The rest of the parameters, fxmin through title, have the same significance as for Plot and MultiPlot.

In broad lines, Contour scans the z-levels in increasing order, between zmin and zmax. For each level, the code runs sequentially through the square cells formed by four neighboring grid nodes. In each cell, the occurrence of the current z-level is looked for along each of the four sides, whereby the coordinates of the occurrence points are determined by inverse linear interpolation. Each pair of such points located on different cell sides is connected by a colored line segment in the color corresponding to the current level. Finally, the overall contour plot results by the concatenation of the level segments from the individual square cells.