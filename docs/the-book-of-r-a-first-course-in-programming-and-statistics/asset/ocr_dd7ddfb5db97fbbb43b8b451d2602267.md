+   c. Perform your choice of test in (b) (assume a $\alpha=0.01$ level of significance) and conclude.

Load the MASS package with a call to library("MASS") if you haven't already done so in the current R session. This package includes the ready-to-use Cars93 data frame, which contains detailed data on 93 cars for sale in the United States 1993 (Lock, 1993; Venables and Ripley, 2002).

+   d. Use aggregate to compute the mean length of 93 cars, by two categorical variables: AirBags (type of airbags available—levels are Driver & Passenger, Driver only, and None), and Man.trans.avail (whether the car comes in a manual transmission—levels are Yes and No).

+   e. Produce an interaction plot using the results in (d). Does appear to be an interactive effect of AirBags with Man.trans.avail on the mean length of these cars (if you consider only these variables)?

+   f. Fit a full two-way ANOVA model for the mean lengths according to the two grouping variables (assume satisfaction of all relevant assumptions). Is the interactive effect statistically significant? Is there evidence of any main effects?

# Important Code in this Chapter

| Function/operator | Brief description | First occurrence |
|---|---|--|
| aov | Produce ANOVA table | Section 19.1.3, p. 440 |
| aggregate | Stacked statistics by factor | Section 19.2.1, p. 444 |
| interaction.plot | Two-factor interaction plot | Section 19.2.2, p. 446 |
| kruskal.test | Kruskal-Wallis test | Section 19.3, p. 449 |