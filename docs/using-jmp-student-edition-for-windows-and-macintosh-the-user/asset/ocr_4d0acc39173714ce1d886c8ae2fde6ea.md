# Figure 14.2 Initial Power and Sample Size Dialogs for Single Mean (left) and Two Means (right)

![](bbox=[0.21, 0.1, 0.86, 0.36])

The Two Sample Means choice in the initial Power and Sample Size dialog always requires values for Alpha and the error standard deviation (Error Std Dev), as shown here, and one or two of the other three values: Difference to detect, Sample Size, and Power. The power and sample size platform then calculates the missing item. If there are two unspecified fields, the power and sample size platform constructs a plot that shows the relationship between those two values:

+   - power as a function of sample size, given specific effect size
+   - power as a function of effect size, given a sample size
+   - effect size as a function of sample size, for a given power.

The Power and Sample Size dialog asks for the values depending the first choice of design:

+   - Alpha Alpha is the significance level, usually 0.05. This implies willingness to accept (if the true difference between groups is zero) that 5% (alpha) of the time a significant difference will be incorrectly declared.
+   - Error Std Deviation Error Std (Standard) Deviation is the true residual error. Even though the true error is not known, the power calculations are an exercise in probability that calculates what might happen if the true values were as specified.
+   - Extra Params Extra Params (Parameters) is only for multi-factor designs. Leave this field zero in simple cases. In a multi-factor balanced design, in addition to fitting the means described in the situation, there are other factors with the extra parameters that can be specified here. For example, in a three-factor two-level design with all three two-factor interactions, the number of extra parameters is five—two parameters for the extra main effects, and three parameters for the interactions. In practice, it isn’t very important what values you enter here unless the experiment is in a range where there is very few degrees of freedom for error.
+   - Difference to Detect Difference to detect is the smallest detectable difference (how small a difference you want to be able to declare statistically significant). For single sample problems this is the difference between the hypothesized value and the true value.
+   - Sample Size Sample size is the total number of observations (runs, experimental units, or samples). Sample size is not the number per group, but the total over all groups. Computed sample size numbers can have fractional values, which you need to adjust to real units. This is usually done by