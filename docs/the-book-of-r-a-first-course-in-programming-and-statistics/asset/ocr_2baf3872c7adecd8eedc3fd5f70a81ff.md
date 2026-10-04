For example, in many cases it makes sense to show lines connecting each coordinate, such as when plotting time series data. For this, you would specify plot type "1". Using foo and bar from Section 7.1, the following produces the plot in the left panel of Figure 7-2:

```
R> plot(foo,bar,type="1")
```

![](bbox=[0.238, 0.203, 0.849, 0.418])

Figure 7-2: A line plot produced using five adjoining coordinates, setting type="1" [left] or type="b" [right]

The default value for type is "p", which can be interpreted as "points only". Since you didn't specify anything different, this is what is used for the graph in Figure 7-1. In this example, on the other hand, you've set type="1" (meaning lines only). Other options "b" for both points and lines (shown in the right panel of Figure 7-2) and "o" for overlapping the points with lines (this eliminates the gaps between points and lines visible for type="b"). The option type="n" results in no points or lines plotted, creating an empty plot, which can be useful for complicated plots that must be constructed in steps.

# 7.2.2 Title and Axis Labels

By default, a basic plot won't have a title, and axes will be labeled with the names of the vectors being plotted. But a main title and more descriptive axes often make the plot data easier to interpret. You can add these by supplying text as character strings for main title, xlab for the x-axis, and ylab for the y-axis. Note that these strings may include escape sequences (discussed in Section 4.2.3). The following code produces the plot in Figure 7-3:

```
R> plot(foo,bar,type="b",main="My lovely plot",xlab="x axis label",ylab="location y")
```

```
R> plot(foo,bar,type="b",main="My lovely plot\ntitle on two lines",xlab=""")
```