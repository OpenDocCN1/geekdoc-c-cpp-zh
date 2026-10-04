6 93 10 1 1
7 106 12 1 1
8 125 14 1 1
9 149 16 1 1
10 171 18 1 1
11 199 20 1 1
12 205 21 1 1
13 40 0 2 1
14 49 2 2 1
15 58 4 2 1

You can treat this data set like any other data frame you've created in R—note the use of [1:15,] to access the desired rows from such an object, as detailed in Section 5.2.1.

# 8.1.2 Contributed Data Sets

```
R> library("tseries")
```

'tseries' version: 0.10-32

'tseries' is a package for time series analysis and computational finance.

See library(help="tseries") for details.

You can now enter library(help="tseries") to see the list of data sets in this package, and you can enter ice.river to find more details about the data set you want to work with. The help file describes ice.river as a "time series object" composed of river flow, precipitation, and temperature measurements—data initially reported in Tong (1990). To access this object yourself, you must explicitly load it using the data function. Then you can work with ice.river in your workspace as usual. Here are the first five records:

```
R> data(ice.river)
R ice.river[1:5]
flow.wat prec temp
[1,] 16.10 30.2 8.1 0.9
[2,] 19.20 29.0 4.4 1.6
[3,] 14.50 28.4 7.0 0.1
[4,] 11.00 27.8 0.0 0.6
[5,] 13.60 27.8 0.0 2.0
```