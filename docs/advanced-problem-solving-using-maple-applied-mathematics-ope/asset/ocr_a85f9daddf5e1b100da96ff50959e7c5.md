```
> Foxes := [seq(i, [RF[i,2]], i = 1..201)]:
> pointplot(Foxes, title = "Foxes");
```

![](bbox=[0.277, 0.141, 0.717, 0.419])

```
> pointplot(RF, labels = ["Rabbits", "Foxes"], title = "Predator-Prey");
```

![](bbox=[0.281, 0.483, 0.728, 0.769])

Running this model for even more iterations would show the plot of foxes versus rabbits continuing to spiral. We conclude that the model appears reasonable. We could find the equilibrium values for the system. There are two sets of equilibrium points for rabbits and foxes at (0, 0) and (1200, 130). The orbits of the spiral indicate that the system is moving away from (1200, 130).