the probabilities are near 1 or 0. Suppose that in a wealthy suburban high school, the probability of graduation is .99, which corresponds to odds of 99. When financial aid is increased for needy students, the probability of graduation goes up to .995, which implies odds of 199. Apparently, the odds of graduation have more than *doubled* under the new program even though only half a percent more students are graduating. Is this a meaningful increase? That depends on many nonstatistical issues.

For those who insist on interpreting logistic models in terms of probabilities, there are several graphical and tabular methods available (Long 1997). Perhaps the simplest approach is to make use of equation (2.6):

$$\frac{\partial p_i}{\partial x_i}=\beta p_i(1-p_i).$$

This equation says that the change in the probability for a 1-unit increase in $x$ depends on the logistic regression coefficient for $x$, as well as on the value of the probability itself. For this to be practically useful, we need to know what probability we are starting from. If we have to choose one value, the most natural is the overall proportion of cases that have the event. In our example, 50 out of 147 defendants got the death penalty, so the overall proportion is .34. Taking .34 times 1−.34, we get .224. We can multiply each of the coefficients in Output 2.3 by .224, and we get:

| Variable | Value |
|---|---:|
| BLACKD | .133 |
| WHITVIC | .057 |
| SERIOUS | .046 |

We can then say that, on average, the probability of a death sentence is .133 higher if the defendant is black compared with nonblacks, .057 higher if the victim is white compared with non-white, and .046 higher for a 1-unit increase on the SERIOUS scale. These are sometimes called “marginal effects,” and they are of considerable interest in some fields. Of course, these numbers only give a rough indication of what actually happens for a given change in the $x$ variable. Note, however, that they are very similar to the coefficients obtained with the OLS regression in Output 2.1.

Instead of choosing a single value for $p_i$, we can calculate a predicted probability for each individual, using equation (2.5). Then we can use the derivative formula to generate marginal effects for each individual. You can easily get them with PROC QLIM (part of the