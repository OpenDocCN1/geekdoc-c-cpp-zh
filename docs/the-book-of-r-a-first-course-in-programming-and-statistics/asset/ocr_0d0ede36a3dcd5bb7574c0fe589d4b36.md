You can supply more than one variable to the INDEX argument as separate members of a list (any factor vectors given to this argument should be the same length as the first argument that specifies the data of interest). The results are returned as a matrix for two grouping variables, a 3D array for three grouping variables, and so on.

For some analyses, however, you might need the same information in a different format. The aggregate function is similar to tapply, but it returns a data frame, the results in stacked format according to the specified grouping variables (as opposed to an array returned by tapply). It's called in the same way. The first argument takes the data vector of interest. The second argument, should be a list of the desired grouping variables, and in FUN, specify the function to operate on each subset.

```
R> wb.means <- aggregate(warpsbreaks,
  by=list(warpsbreaks$wool,warpsbreaks$tension),FUN=mean)
R> wb.means
Group.1 X
1 A 44.55556
2 B 28.22222
3 A 24.00000
4 B 28.77778
5 A 24.55556
6 B 18.77778
```

Here I stored the result of the call to aggregate as the object wb for later use.

# 19.2.2 Main Effects and Interactions

I mentioned earlier that you could perform just a one-way ANOVA on each grouping variable separately, but this, in general, isn't a good idea. I'll demonstrate this now with the warbreaks data (a quick inspection of the relevant diagnostics shows no obvious cause for concern):

```
R> summary(aov(breaks$wool,data=warpsbreaks))
Df Sum Sq Mean F value Pr(F)
wool 1 451 450.7 2.668 0.108
Residuals 52 8782 168.9
R> summary(aov(breaks$tension,data=warpsbreaks))
Df Sum Sq Mean F value Pr(F)
tension 2 2034 1017.1 7.206 0.00175 **
Residuals 51 7199 141.1 ---

Signif. codes: 0 *** 0.001 ** 0.01 * 0.05 . ' 1
```

This output tells you that if you ignore tension, there is no evidence to suggest that there is any difference in the mean number of imperfections