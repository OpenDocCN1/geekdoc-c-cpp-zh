This result matches your manually computed version from earlier. Note also that the corresponding confidence level, $1 - \alpha$, is stored alongside this component (refer to Section 6.2.1).

In examining the result for the snack example, with a $p$-value to be careful when interpreting hypothesis tests. With $\alpha$ at 0.05 for this particular test, $H_0$ is rejected. But what if the test were carried out with $\alpha=0.01$? The p-value is greater than 0.01, so in that case, $H_0$ would be retained, for no reason other than the arbitrary movement of the $\alpha$. In these situations, it's helpful to comment on the perceived strength of the evidence against the null hypothesis.
Reasonably state that there exists some evidence to support $H_A$ but that this evidence is not especially strong.

# Exercise 18.1

+   a. Adult domestic cats of a certain breed are said to have an average weight of 3.5 kilograms. A feline enthusiast disagrees and collects a sample of 73 weights of cats of this breed. From her sample, she calculates a mean of 3.97 kilograms and a standard deviation of 2.21 kilograms. Perform a hypothesis test to test her claim that the true mean $\mu$ is not 3.5 kilograms by setting up the appropriate hypothesis, carrying out the analysis, and interpreting the p-value (assume the significance level is $\alpha = 0.05$).
b. Suppose it was previously believed that the mean magnitude of seismic events off the coast of Fiji is 4.3 on the Richter scale. Use the data in the mag variable of the ready-to-use quite set, providing 1,000 sampled seismic events in that area, to test the claim that the true mean magnitude is in fact greater than 4.3. Set up appropriate hypotheses, use t. test (conduct the test at a significance level of $\alpha = 0.01$), and draw a conclusion.
c. Manually compute a two-sided confidence interval for the true mean of (b).

# 18.2.2 Two Means

Often, testing a single sample mean is not enough to answer the question you're interested in. In many settings, a researcher wants to directly compare the means of two distinct groups of measurements, which boils down to a hypothesis test for the true difference between two means; call them $\mu_1$ and $\mu_2$.

The way in which two groups of data relate to each other affects the specific form of standard error for the difference between two sample means and therefore the test statistic itself. The actual comparison of the two