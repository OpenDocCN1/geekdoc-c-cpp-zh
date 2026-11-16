![](bbox=[0.15, 0.08, 0.85, 0.44])

Figure 8.6 The decision tree representing the problem instance in Example 8.4.

The previous discussion implies that we have these conditional probabilities:

$P(Test = positive|Tran = good) = .3$
$P(Test = positive|Tran = bad) = .9$

Furthermore, Sam knows that 20% of the 1996 Spiffycars have bad transmissions. That is,

$P(Tran = good) = .8$.

Sam is going to have his friend run the test for free, and then he will decide whether to buy the car.

This problem instance is represented in the decision tree in Figure 8.6. Notice first that, if he does not buy the vehicle, the outcome is simply $10,000. This is because the point in the future is so near that we can neglect interest as negligible. Note further that the probabilities in that tree are not the ones stated in the example. They must be computed from the stated probabilities. We do that next. The probability on the upper edge emanating from the Test node is the prior probability the test is positive. It is computed as follows (note that we use our abbreviated notation):

$P(positive) = P(positive|good)P(good) + P(positive|bad)P(bad)$
$= (.3)(.8) + (.9)(.2) = .42.$