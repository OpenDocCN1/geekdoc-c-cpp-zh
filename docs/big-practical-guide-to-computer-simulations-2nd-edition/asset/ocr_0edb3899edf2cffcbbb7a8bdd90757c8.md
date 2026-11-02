More options, like relative coordinates, line styles, etc., can be obtained by typing help set arrow.

So far, all output has appeared on the screen. It is possible to redirect the output, for example, to an encapsulated postscript file (by setting set terminal postscript and redirecting the output set output "test.eps"). When you now enter a plot command, the corresponding postscript file will be generated.

Note that not only several functions but also several data files or a mixture of both can be combined into one figure. To remember what a plot exported to files means, you can set axis labels of the figure by typing set xlabel "L", which becomes active when the next plot command is executed. Also you can use set title or place arbitrary labels via set label. Use the help command to find out more.

Also three-dimensional plotting (in fact a projection into two dimensions) is possible using the splot command (enter help splot to obtain more information). Here, as example, we plot a two-dimensional Gaussian distribution:

```
gnuplot> x0=3.0
 gnuplot> y0=-1.0
 gnuplot> sx=1.0
 gnuplot> sy=5.0
 gnuplot> gauss2d(x,y)=exp(-(x-x0)**2/(2*sx)-(y-y0)**2/(2*sy))\
 > /sqrt(4*pi*2*sx*2*sy**2)
 gnuplot> set xlabel "x"
 gnuplot> set ylabel "y"
 gnuplot> splot [x0-2:x0+2] [y0-4:y0+4] gauss2d(x,y) with points
 gnuplot>
```

Note that the long line containing the definition of the (two-argument) function gauss2d() is split up into two lines using a backslash at the end of the first line. Furthermore, some of the variables are used inside the interval specifications at the beginning of the splot command. Clearly, you also can plot data files with three-dimensional data. The resulting plot appearing in the output window is shown in Fig. 8.26. You can drag the mouse inside the window showing the plot, which will alter the view.

Finally, to stop the interactive execution of gnuplot, enter the command exit. These examples should give you already a good impression of what can be done with gnuplot. More can be found in the documentation or the online help. How to fit functions to data using gnuplot is explained in Sec. 8.6.2. So far, the plots were quickly made to get an impression