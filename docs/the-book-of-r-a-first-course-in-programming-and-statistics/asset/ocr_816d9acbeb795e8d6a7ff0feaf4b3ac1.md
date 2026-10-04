for the categorized NW.cols, you have only one hex code for each bin (so just k = 5 colors).

This line produces the image on the right of Figure 25-4.

```
R> plot(surv$Wr.Hnd, surv$Height, col=NW.cols2, pch=19)
```

In terms of this relatively simple example, the visual difference between the two approaches is minimal, though looking closely you can indeed pick out the smoother color transition in the normalized version. As you increase k when using the categorization technique, the visual result will become closer to that of the normalization approach. That said, the normalization approach should generally be preferred, since it more closely fits the continuous nature of the values you’re trying to visualize, and it works more effectively for values with a skewed distribution or when you’re working with a complex color palette.

# 25.1.5 Including a Color Legend

Now that you can use color to significant effect in your plots, you need a legend to reference the color scale. It’s possible to create a legend using base R tools alone, but it can be simpler to use contributed functionality in R instead.

One useful function for this is the colorlegend command. This is found in the shape package (Soetaert, 2014), so first download and install shape from CRAN. The following code then loads the package, reproduces the most recent plot (based on the surv object created earlier and shown on the right of Figure 25-4) with some tidier axis titles, and draws the color strip legend:

```
R> library("shape")
R> plot(surv$Wr.Hnd, surv$Height, col=NW.cols2, pch=19,
    xlab="Writing handspan (cm)", ylab="Height (cm)")
R> colorlegend(NW.pal(200), zlim=range(surv$NW.Hnd), zval=seq(13,23,by=2),
    posx=c(0.3,0.33), posy=c(0.5,0.9), main="Nonwriting handspan")
```

This result is given on the left of Figure 25-5.

The colorlegend functions assumes that you already have a plot present in an active graphics device, so you need to have one created first. The first thing you supply to colorlegend is the color span of the values you want to reference. This is easiest with a color palette function like those listed in the help file ?rainbow or created using colorRampPalette—in other words, a function that takes an integer value telling it how many colors to generate. Doing so with a large number of colors gives you a smooth color strip, so I use NW.pal(200). Next, you provide colorlegend with the range of the values that will be referenced by the legend using zlim, in this case, the range of the nonwriting handspans range(surv$NW.Hnd). The zval argument takes in the values that you want to mark off on the legend. The values of a sequence between 13 and 23, in steps of 2, are marked off.