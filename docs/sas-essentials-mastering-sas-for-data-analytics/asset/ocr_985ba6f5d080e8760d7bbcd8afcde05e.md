Creating an SGPLOT HISTOGRAM: One of the main differences in SGPLOT (as opposed to GPLOT) is that you can more easily overlay various components in the same plot. For example, to create a histogram, you could use the code

```
PROC SGPLOT;
HISTOGRAM AGE;
RUN;
```

To add a density plot (default is a normal plot), you simply add another plot statement:

```
PROC SGPLOT;
HISTOGRAM AGE;
DENSITY AGE;
RUN;
```

# HANDS-ON EXAMPLE

+   1. Open the program file SGPLOT1.SAS.

```
PROC SGPLOT DATA=MSASLIB.WOUND;
HISTOGRAM sbp;
TITLE "SGPLOT Histogram";
RUN;
```

Run this code and observe the output shown in Figure 18.14.

![](bbox=[0.246, 0.532, 0.742, 0.783])

Figure 18.14 Histogram created using SGPLOTS

+   2. Add the following code after the HISTOGRAM line:

```
DENSITY SBP/TYPE=KERNEL;
```