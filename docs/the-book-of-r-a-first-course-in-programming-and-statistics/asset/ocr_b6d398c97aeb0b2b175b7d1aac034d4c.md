# 24.3.2 Facets Mapped to a Categorical Variable

If you independently created ggplot2 graphics to appear in the same window, grid.arrange is arguably the best way to deal with them. However, the ggplot2 package offers a flexible alternative to quickly view multiple plots. Often, when exploring a data set, you'll want to create several plots of the same variables based on the levels of one or more categorical variables. This behavior, referred to as faceting, familiar territory for ggplot2 using either the facet_wrap or the facet_grid command.

Let's focus on the simplest case where you have one categorical variable. Remaining with the air data frame object, the following line creates a ggplot2 object of the density plots of the New York temperatures on the right of Figure 24-3:

```
ggp <- ggplot(data=air,aes(x=Temp,fill=Month)) + geom_density(alpha=0.4) + 
  ggtitle("Monthly temperature probability densities") +
  labs(x="Temp (F)",y="Kernel estimate")
```

Rather than view all densities together, you can create a plot of each one separately, displaying them in the same device, with the following three uses of facet_wrap, the results are at the top left, top right, and bottom of Figure 24-5:

```
ggp + facet_wrap("Month")
gp + facet_wrap("Month,scales="free",nscale="free")
gp + facet_wrap("Month,nrow=1)
```

![](bbox=[0.238, 0.558, 0.905, 0.846])

Figure 24-5: Three examples using facet_wrap to display kernel density estimates of the temperature data, split by month