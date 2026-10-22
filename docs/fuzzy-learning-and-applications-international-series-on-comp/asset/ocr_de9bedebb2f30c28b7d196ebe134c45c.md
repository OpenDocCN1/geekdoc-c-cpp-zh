# 8.8.2 TSP by Szu’s Energy Function

The fuzzy logic-based algorithm was applied to a TSP featuring 15 cities with random distances between them.

The minimum distance in the scenario was 0.05, so the LowerBound was set to 0.75. The Tolerance was set to 10, δ to 5 and ε to 0.01.

The sets of IterDelta, IterMaxGood and PercIterMaxGood values are the same shown in (8.26). This choice was made to assess the influence of IterDelta on the quality of the solution, as done in the previous section.

On the basis of this set of parameters, the fuzzy-logic algorithm gave the HCs:

```
HCs = { A = B = 317
        C = 888
        D = 766 } (8.31)
```

Unfortunately in [5] Szu did not specify the set of HCs that he used in his energy function. For this reason we can not compare the solutions obtained using (8.31) with those featured by the original Szu’s work for the same scenarios, as done in the previous section with the Hopfield and Tank’s solution. The comparison between the two approaches may be done only on the basis of the percentage of optimal solutions obtained in TSPs featuring certain number of cities, as only this information is available in the Szu’s work [5] and in [35].

![](bbox=[0.2, 0.74, 0.8, 0.92])

# Figure 8.12 Quality of solution

In Fig. 8.12 the percentage of optimal solutions obtained with the set of coefficients (8.31) is shown, considering TSPs featuring 5, 10, 15, 20, 25, 30 and 40 cities.

As said in the previous section, 10 different random distance scenarios were