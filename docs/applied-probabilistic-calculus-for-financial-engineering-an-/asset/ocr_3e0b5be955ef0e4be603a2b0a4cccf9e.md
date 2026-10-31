![](bbox=[0.18, 0.12, 0.5, 0.38])

Figure 4.14 An x-y plot for > plot (weight, height, pch=8).

For example, to change the plotting symbol, one may use the keyword pch (for "plotting character") in the following R command:

```
> plot (weight, height, pch=8)
> # Outputting: Figure 4.14.
```

Note that the output is the same as that shown in Figure 4.13, except that the points are marked with little "8-point stars", corresponding to plotting character pch = 8.

In the documentation for pch, a total of 26 options are available, providing different plotting characteristics for points in R graphics. They are shown in Figure 4.15.

The parameter BMI was chosen in order that this value should be independent of a person's height, thus expressing as a single number or index indicative of whether a case subject is overweight, and by what relative amount. Of course, one may plot "height" as the abscissa (namely, the horizontal "x-axis") and "weight" as the ordinate (namely, the vertical "y-axis"), as follows:

```
> plot (height, weight, pch=8) # Outputting: Figure 4.16.
```

Since a normal BMI is between 18.5 and 25, averaging (18.5 + 25)/2 = 21.75. For this BMI value, the weight of a typical "normal" person would be (21.75 × height²). Thus, one can superimpose a line of "expected" weights at BMI = 21.75 on Figure 4.16. This line may be accomplished in the R environment by the following code segments:

```
> ht <- c(1.79, 1.64, 1.73)
> lines (ht, 21.75*ht^2) # Outputting: Figure 4.17.
```

![](bbox=[0.05, 0.9, 0.95, 0.98])

Figure 4.15 Plotting symbols in R: pch = n, n = 0, 1, 2, . . . , 25.