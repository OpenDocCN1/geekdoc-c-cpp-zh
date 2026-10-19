there may not be a single best way to visualize a particular data set, and so some trial and error may be necessary to “see” what works best.

# Listing 1.1 EasyVisual.py produces two different 2D plot using the Visual package.

```
# EasyVisual.py:      Simple graph object using Visual
from visual.graph import *                # Import Visual
Plot1 = gcurve(color = color.white)       # gcurve method
for x in arange(0., 8.1, 0.1):            # x range
    Plot1.plot( pos = (x, 5.*cos(2.*x)*exp(-0.4*x)) ) # Plot pts
graph1 = gdisplay(width=600, height=450,\
    title='Visual 2D Plot', xtitle='x', ytitle='f(x)',\
    foreground = color.black, background = color.white)
Plot2 = gdots(color = color.black)       # Dots
for x in arange(-5., +5, 0.1):
    Plot2.plot(pos = (x, cos(x)))
```

# 1.5.1

# Visual (VPython)’s 2D Plots

As indicated in the description of packets, VPython (Python plus the Visual package) is a simple way to get started with Python and visualizations.³ The Visual package is useful for creating 3D solids, 2D plots, and animations. For example, in Figure 1.2, we present two plots produced by the program EasyVisual.py in Listing 1.1. Notice that the plotting technique is to create first a plot object, and then to add the points to the object, one by one. (In contrast, Matplotlib creates a vector of points and then plots the entire vector.)

![](bbox=[0.185, 0.595, 0.52, 0.725])

![](bbox=[0.5, 0.56, 0.825, 0.72])

(a)

(b)

Figure 1.2 Screen dumps of two x–y plots produced by EasyVisual.py using the Visual package. Plot (a) uses default parameters, while plot (b) uses user-supplied options.

3) Because Visual is not one of the Canopy packages, to run our Visual programs you would need to install the Visual package and the version of Python that runs with it, even if you have Canopy installed. There is no problem doing this because VPython and Canopy go into different folders/directories.