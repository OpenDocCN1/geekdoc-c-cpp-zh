# Figure 9.2 Comparison of Trends in Protein over Time

![](bbox=[0.18, 0.11, 0.86, 0.48])

measurements and the interaction between diets and weekly measurements are the subplot treatments. A simple univariate analysis of the data could be made using the split-plot model with either proc glm or proc mixed. For example, the commands to make the analysis in proc mixed are shown below.

```
proc mixed data=strung;
   class Diet week ;
   model protein=Diet week Diet*week;
   random Cow(Diet);
   lsmeans Diet week;
   estimate 'Lupins vs Barley' Diet 1 -1 0;
   estimate 'Mixed vs Barley' Diet 1 0 -1;
run;
```

In this analysis the diet factor is compared to the cow-to-cow variation and is found to be non-significant. The difference in protein levels over time is compared to the within cow variation and is found to be significant at the alpha = 0.01 level, indicating that the protein level decreases over the first five weeks for all three diets. The comparison of the trends in protein over time,