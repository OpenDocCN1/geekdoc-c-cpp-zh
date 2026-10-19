cated numerics of NumPy and LAPACK (Anderson et al., 2013), and, believe it or not, is easy to use. Specifically, Matplotlib uses the NumPy array (vector) object to store the data to be plotted. In Chapter 6, we talk at more length about NumPy arrays, so you may want to go there soon to understand arrays better.

Matplotlib commands are by design similar to the plotting commands of MATLAB, a commercial problem-solving environment that is particularly popular in engineering. As is true for MATLAB, Matplotlib assumes that you have placed the x and y values that you wish to plot into 1D arrays (vectors), and then plots these vectors in one fell swoop. This is in contrast to Visual, which first creates a plot object and then adds points to the object one by one. Because Matplotlib is not part of standard Python, you must import the entire Matplotlib package, or the individual methods you use, into your program. For example, on line 2 of EasyMatPlot.py in Listing 1.4 (line numbers are in the dark shading on the right), we import Matplotlib as the pylab library:

```
from pylab import *        # Load Matplotlib
```

Then, on lines 6 and 7 we calculate and input arrays of the x and y values

```
x = arange(Xmin, Xmax, DelX)    # Form x array in range with increment
y = -sin(x)*cos(x)               # Form y array as function of x array
```

As you can see, NumPy's arange method constructs an array covering “a range” between Xmax and Xmin in steps of DelX. Because the limits are floating-point numbers, so also will be the x_i's. And because x is an array, y = -sin(x)*cos(x) is automatically one too! The actual plotting is performed on line 14 with a dash “-” used to indicate a line, and lw = 2 to set its width. The result is shown in Figure 1.5a with the desired labels and title. The show() command produces the graph on your desktop. More commands are given in Table 1.3. We suggest you try out some of the options and types of plots possible.

![](bbox=[0.22, 0.65, 0.87, 0.85])

Figure 1.5 Matplotlib plots. (a) Output of EasyMatPlot.py showing a simple, x–y plot. (b) Output from GradesMatPlot.py that places two sets of data points, two curves, and unequal upper and lower error bars, all on one plot.