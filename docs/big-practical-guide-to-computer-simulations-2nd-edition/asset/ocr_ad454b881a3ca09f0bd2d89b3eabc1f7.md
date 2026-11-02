specified like in

```
plot [7:20] [-1.79:-1.77] "sg_e0_L.dat" with yerrorbars
```

If you just want to set the y range, you have to specify [] for the x-range. You can also fix the ranges via the set xrange and the set yrange commands, such that you do not have to give them each time with the plot command, see help set xrange or help unset xrange for unsetting a range.

Gnuplot knows a lot of built-in functions like sin(x), log(x), powers, roots, Bessel functions, error function,11 and many more. For a complete list type help functions. These function can be also plotted. Furthermore, using these functions and standard arithmetic expressions, you can also define your own functions, e.g. you can define a function ft(x) for the Fischer-Tippett pdf (see Eq. (8.43)) for parameter λ (called lambda here) and show the function via

```
gnuplot> ft(x)=lambda*exp(-lambda*x)*exp(-exp(-lambda*x))
gnuplot> lambda=1.0
gnuplot> plot ft(x)
```

You can also include arithmetic expressions in the plot command. To plot a shifted and scaled Fischer-Tippett pdf you can type:

```
gnuplot> plot [0:20] 0.5*ft(0.5*(x-5))
```

The Fischer-Tippett pdf has a tail which drops off exponentially. This can be better seen by a logarithmic scaling of the y axis.

```
gnuplot> set logscale y
gnuplot> plot [0:20] 0.5*ft(0.5*(x-5))
```

will produce the plot shown in Fig. 8.24.

Furthermore, it is also possible to plot several functions in one plot, via separating them via commas, e.g. to compare a Fischer-Tippett pdf to the standard Gaussian pdf, here the predefined constant pi is used:

```
gnuplot> plot ft(x), exp(-x*x/2)/sqrt(2*pi)
```

It is possible to read files with multi columns via the using data modifier, e.g.

```
gnuplot> plot "test.dat" using 1:4:5 w e
```