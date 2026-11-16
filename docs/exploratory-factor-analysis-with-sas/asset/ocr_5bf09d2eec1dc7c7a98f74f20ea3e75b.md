```
end;
*Compute mean of the weighted item scores as the factor score;
fs(f)=mean(of wt.); *compute mean of weighted estimates as the factor score;
end;
run;
```

**Methods of factor weighting.** Many different types of weights are used in the estimation of factor scores. As we mentioned above, Table 9.1 on page 163 displays two such types that can be used to estimate factor scores for the engineering data. Let's do a quick comparison of these weights to determine the comparability of their subsequent factor scores. An initial glance will tell you that the coefficients are in a different metric. Regardless of whether you sum or average the different composites taken, the scores will be on completely different scales. Nevertheless, the coefficients do tend to follow a similar rank order. A few of the coefficients deviate from this pattern, but the deviations are minor in size. Furthermore, if we examine the correlation between the two sets of factors scores produced (see Figure 9.2 on page 166), we would conclude that the methods provide the same fundamental results. Thus, at least when it comes to picking between different weighted methods, the specific weights used might not make a large difference in the results.