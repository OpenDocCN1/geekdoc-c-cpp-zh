# USING PROC UNIVARIATE 229

PROC MEANS is useful for calculating descriptive statistics for many variables at a time, whereas PROC UNIVARIATE is best for the case in which you want to analyze one or a few variables in depth and create detailed histograms. The following Hands-on Example illustrates some of these commonly used options and statements.

# HANDS-ON EXAMPLE

In this example, you will learn how to use PROC UNIVARIATE.

+   1. Open the program file AUNI1.SAS.

```
DATA EXAMPLE;
INPUT AGE @@;
DATALINES;
12 11 12 12 9 11 8 8 7 11 12 14 9 10 7 13
6 11 12 4 11 9 13 6 7 13 93 12 12 10 13
11 8 11 15 12 14 10 10 13 13 8 7 13
11 9 12
;
nPROC UNIVARIATE DATA=EXAMPLE;
VAR AGE;
RUN;
```

+   2. Run this program and observe that this procedure produces several tables of output, and that the output in the Results Viewer is in HTML format. Below is a description of the statistics reported in these tables.

# 9.2.1 Understanding PROC UNIVARIATE Output

The output from the Hands-on Example is given in several tables, and we describe the contents in each table below:

Moments Output: The first table (Moments; Table 9.15) provides a list of descriptive statistics for the variable AGE.

N is the sample size unless the sample size unless a WEIGHT statement is used to identify a variable that counts for each observation.

Mean is the arithmetic mean (also known as the average).

Sum Observations is the total (sum) of all the data values.

Std Deviation is the standard deviation.

Variance is a measure of the spread of the distribution (and is the square of the standard deviation).

Skewness is a measure of the symmetry of the data. For normally distributed data, skewness should be close to 0. A positive value indicates that the skew is to the right (long right tail), and a negative value indicates a skew to the left (long left tail).