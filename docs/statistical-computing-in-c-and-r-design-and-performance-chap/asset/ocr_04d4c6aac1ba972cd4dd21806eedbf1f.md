# AN INTRODUCTION TO R

```
> pdf("some.pdf")
> dev.list()
quartz  pdf
  2       3
> plot(x,x^2)
> dev.set(which = 2)
  2
quartz
> plot(x,x^2)
> dev.off(3)
quartz
  2
> system("ls *.pdf")nsome.pdf
```

An initial check of the working directory shows that no pdf files are present. A plot is then created which initializes the X11 terminal. The output from dev.list() indicates that only this device (called quartz) in this instance assigned the number 2 is available for plotting. A new device is created for creating a pdf file at which point there are two devices and the output from plot is sent to the graphics device numbered 3 it writes to the file.pdf. A switch is made back to the X11 device and the graphics output is sent to the X11 terminal where it becomes visible. The pdf device is then closed and we are informed that the X11 device is the only one that remains active. A check reveals that the file.pdf file has been created in the current directory.

# B.3 R for statistical analysis

As the previous two sections have fully demonstrated, R is much more than just a statistics software package. Of course, it does come equipped with a number of functions for carrying out many of the standard statistical calculations that arise in the analysis of data. Many are more available through packages that can be downloaded from the CRAN website.

There is a generic function that produces some of the standard summary statistics when it is applied to an array or data frame. The ensuing output was produced using one of the data sets that comes with R.

```
> data(mtcars)
> A <- as.matrix(mtcars, c(1, 3, 6))
> summary(A)
```

| mpg | disp | wt |
|---|---|---|
| Min. : :10.40 | Min. : :71.1 | Min. : :1.613 |
| 1st : :15.43 | 1st : :120.8 | 1st : :2.581 |
| Median : :19.20 | Median : :196.3 | Median : :3.325 |
| Mean : :20.09 | Mean : :230.7 | Mean : :3.217 |
| 3rd : :22.80 | 3rd : :92.6 | 3rd : :3.610 |
| Max. : :33.90 | Max. : :472.0 | Max. : :5.424 |

```
> apply(A, 2, IQR)
6.0269481 123.9386938 0.9784574
```

| mpg | disp | wt |
|---|---|---|
| 7.37500 20.17500 | 1.02875 |

The data set mtcars in this example contains information on several variables related to 32 cars that was reported in a 1974 issue of Motor Trend magazine. We have elected to work