![](bbox=[0.238, 0.066, 0.608, 0.303])

**Figure 14-8:** A scatterplot of petal measurements split by species using the built-in iris data frame

# Consider the two objects created here:

The first line creates a vector *iris_pch* of each length equal to the number of observations in iris, with every entry being 19. Vector subsetting then overwrites the entries corresponding to *Iris versicolor* and sets the point character to 1. The same steps are followed to create col_; an appropriately sized vector is filled with the character strings "black", and those entries corresponding to *Iris virginica* are overwritten and set to "gray". With that, note that the single line shown next, followed by the same call to legend, will produce an identical plot:

```
```r
plot(iris[,4,3],col=iris_col,pch=iris_pch, xlab="Petal Width (cm)",ylab="Petal length (cm")
```
```

# 14.2 Matrix of Plots

The "single" type of planar scatterplot is really useful only when comparing two numeric-continuous variables. When there are more continuous variables of interest, it isn't possible to display... A simple and common solution is to generate a two-variable scatterplot for each pair of variables and show them together in a structured way; this is referred to as a *scatterplot matrix*. Making use of the iris_pch and iris_col vectors created earlier, you can generate a scatterplot matrix for all