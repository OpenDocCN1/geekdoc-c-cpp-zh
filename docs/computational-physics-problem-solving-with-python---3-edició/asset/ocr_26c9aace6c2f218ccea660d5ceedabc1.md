EasyVisual.py is seen to create two plot objects, Plot1 and Plot2, with the plot method used to plot each object. Plot1 uses the gcurve method with no options specified other than the color of the curve (white). We obtain (Figure 1.2a) a connected curve by default, but no labels. In contrast, Plot2 uses the gdisplay method to set the display characteristics for the plot to follow, and then gdots to draw the data as points (Figure 1.2b). You use a gdisplay plotting object before you create a gcurve graph object, in order to set the size, position, and title for the graph window, to specify titles for the x and y axes, and to specify maximum values for each axis. The gdisplay arguments are self-explanatory, with the width and height given in pixels. Because we set Plot2= gdots(), only points are plotted.

# Listing 1.2 3GraphVisual.py produces a 2D x–y plot with the Matplotlib and NumPy packages.

```
# 3GraphVisual.py: 3 plots in the same figure, with bars, dots and curve
from visual import *
from visual.graph import *
string = "blue: sin^2(x), white: cos^2(x), red: sin(x)*cos(x)"
graph1 = gdisplay(title=string, xtitle='x', ytitle='y')
y1 = gcurve(color=color.yellow, delta=3)      # curve
y2 = gvbars(color=color.white)                # vertical bars
y3 = gdots(color=color.red, delta=3)          # dots
for x in arange(-5, 5, 0.1):                   # arange for floats
    y1.plot( pos=(x, sin(x)*sin(x)) )
    y2.plot( pos=(x, cos(x)*cos(x)/3.) )
    y3.plot( pos=(x, sin(x)*cos(x)) )
```

Note that the Python codes are listed within shaded boxes with some formatting to improve readability. For example, see Listing 1.2. Note that we have structured the codes so that a line is skipped before major elements like functions, and that indentations indicate structures in Python (where Java and C may use braces).

It is often a good idea to place several plots in the same figure. The program 3GraphVisual.py in Listing 1.2 does that and produces the graph in Figure 1.3a. There are white vertical bars created with gvbars, red dots created with gdots, and a yellow curve created with gcurve (colors appear only as shades of gray in the paper text). Also note in 3GraphVisual.py that we avoid having to include the package name as a prefix to the commands by starting the program with import visual.graph as vg. This both imports Visual's graphing package and assigns the symbol vg to visual.graph.

# 1.5.1.1 VPython's 3D Objects

# Listing 1.3 3Dshapes.py produces a sample of VPython's 3D shapes.

```
# 3Dshapes.py: Some 3D Shapes of VPython
from visual import *
graph1 = display(width=500, height=500, title='VPython 3D Shapes',
    range=10)
```