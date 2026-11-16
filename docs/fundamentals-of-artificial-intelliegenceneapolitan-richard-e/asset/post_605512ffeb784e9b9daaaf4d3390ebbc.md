
Furthermore, she assigns

P(Dow = 11,000) = .6.

This problem instance is represented by the decision tree in Figure 8.4. Next we solve the tree:

EU(ICK₁) = (.2)($50,000) + (.8)($200,000) = $170,000

EU(ICK₂) = (.5)($50,000) + (.5)($200,000) = $125,000

EU(Buy ICK) = EU(DOW₁) = (.6)($170,000) + (.4)($125,000) = $152,000

EU(ICK₃) = (.3)($0) + (.7)($250,000) = $175,000

EU(ICK₄) = (.6)($0) + (.4)($250,000) = $100,000

EU(Buy option) = EU(DOW₂) = (.6)($175,000) + (.4)($100,000) = $145,000

EU(D) = max($152,000, $145,000) = $152,000.

The solved decision tree is shown in Figure 8.5. The decision is to buy ICK. ■

The previous example illustrates a problem with decision trees. That is, the representation of a problem instance by a decision tree grows exponentially with the size of the instance. Notice that the instance in Example 8.3 only has one more element in it than the instance in Example 8.2; that is, it includes that uncertainty about the Dow. Yet its representation is twice as large. So it is quite difficult to represent a large instance with a decision tree. We will see in the next section that influence diagrams do not have this problem. Before that, we show more examples.

### Example 8.4

Sam has the opportunity to buy a 1996 Spiffycar automobile for $10,000, and he has a prospect who would be willing to pay $11,000 for the auto if it is in excellent mechanical shape. Sam determines that all mechanical parts except for the transmission are in excellent shape. If the transmission is bad, it will cost Sam $3000 to repair it, and he would have to repair it before the prospect would buy it. So he would only end up with $8000 if he bought the vehicle and its transmission was bad. He cannot determine the state of the transmission himself. However, he has a friend who can run a test on the transmission. The test is not absolutely accurate. Rather, 30% of the time it judges a good transmission to be bad and 10% of the time it judges a bad transmission to be good. To represent this relationship between the transmission and the test, we define the following random variables:

| Variable | Value | When the Variable Takes This Value |
| :--- | :--- | :--- |
| Test | positive | Test judges the transmission to be bad. |
| | negative | Test judges the transmission to be good. |
| Tran | good | Transmission is good. |
| | bad | Transmission is bad. |

![](img/67fa924962ee21b3590be9f3b10d9fe7_221_0.png)

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

![](img/67fa924962ee21b3590be9f3b10d9fe7_222_0.png)

Figure 8.7 The solved decision tree given the decision tree in Figure 8.6.

The probability on the upper edge emanating from the $Tran_1$ node is the probability the transmission is good given the test is positive. We compute it using Bayes' theorem as follows:

```
P(good|positive) = \frac{P(positive|good)P(good)}{P(positive)}
= \frac{(.3)(.8)}{.42} = .571429.
```

It is left as an exercise to determine the remaining probabilities in the tree. Next, we solve the tree:

```
EU(Tran_1) = (.571429)($11,000) + (.428571)($8000) = $9714
EU(D_1) = max($9714, $10,000) = $10,000
EU(Tran_2) = (.965517)($11,000) + (.034483)($8000) = $10,897
EU(D_2) = max($10,897, $10,000) = $10,897.
```

We need not compute the expected value of the $Test$ node because there are no decisions to the left of it. The solved decision tree is shown in Figure 8.7. The decision is to not buy the vehicle if the test is positive and to buy it if the test is negative.

![](img/67fa924962ee21b3590be9f3b10d9fe7_223_0.png)

Figure 8.8 The decision tree representing the problem instance in Example 8.5.

The previous example illustrates another problem with decision trees. That is, the probabilities needed in a decision tree are not always the ones that are readily available to us. So we must compute them using the Law of Total Probability and Bayes’ theorem. We will see that influence diagrams do not have this problem either. More examples follow.

### Example 8.5

Suppose Sam is in the same situation as in Example 8.4, except that the test is not free. Rather, it costs $200. So Sam must decide whether to run the test, buy the car without running the test, or keep his $10,000. The decision tree representing this problem instance is shown in Figure 8.8. Notice that the outcomes when the test is run are all $200 less than their respective outcomes in Example 8.4. This is because it costs $200 to run the test. Note further that, if the vehicle is purchased without running the test, the probability of the transmission being good is simply its prior probability of .8. This is because no test was run. So our only information about the transmission is our prior information. Next, we solve the decision tree. It is left as an exercise to show that

$EU(D_1) = \$9800$
$EU(D_2) = \$10,697.$

Therefore,

$EU(Test) = (.42)(\$9800) + (.58)(\$10,697) = \$10,320.$

Furthermore,

$EU(Tran_3) = (.8)(\$11,000) + (.2)(\$8000) = \$10,400.$

Finally,

$EU(D_3) = \max(\$10,320, \$10,400, \$10,000) = \$10,400.$

So Sam's decision is to buy the vehicle without running the test. It is left as an exercise to show the solved decision tree.

The next two examples illustrate cases in which the outcomes are not numeric.

### Example 8.6

Suppose Leonardo has just bought a new suit, he is about to leave for work, and it looks like it might rain. Leonardo has a long walk from the train to his office. So he knows if it rains and he does not have his umbrella, his suit will be ruined. His umbrella will definitely protect his suit from the rain. However, he hates the inconvenience of lugging the umbrella around all day. Given that he feels there is a .4 probability it will rain, should he bring his umbrella? A decision tree representing this problem instance is shown in Figure 8.9.

Notice that the outcomes have numeric values, which are needed to solve the problem. We assigned those values as follows. Clearly, the ordering of the outcomes from worst to best is as follows:

- 1. suit ruined
- 2. suit not ruined, inconvenience
- 3. suit not ruined.

We assign a utility of 0 to the worst outcome and a utility of 1 to the best outcome. So

$U(\text{suit ruined}) = 0$
$U(\text{suit not ruined}) = 1.$

Then we consider lotteries (chance nodes) \( L_p \) in which Leonardo gets the outcome “suit not ruined” with probability \( p \) and outcome “suit ruined” with

![](img/67fa924962ee21b3590be9f3b10d9fe7_225_0.png)

Figure 8.9 The decision tree representing the problem instance in Example 8.6.

probability $1 - p$. The utility of “suit not ruined, inconvenience” is defined to be the expected utility of the lottery $L_p$ for which Leonardo would be indifferent between lottery $L_p$ and being assured of “suit not ruined, inconvenience.” We then have

```
U(suit not ruined, inconvenience)
\equiv EU(L_p)
= pU(suit not ruined) + (1 - p)U(suit ruined)
= p(1) + (1 - p)0 = p.
```

Let’s say Leonardo decides $p = .8$. Then

```
U(suit not ruined, inconvenience) = .8.
```

We now solve the decision in Figure 8.9.

```
EU(R) = (.4)(0) + (.6)(1) = .6
EU(D) = max(.6, .8) = .8.
```

So the decision is to take the umbrella.

The method used to obtain numeric values in the previous example easily extends to the case where there are more than three outcomes. For example, suppose there was a fourth outcome “suit goes to cleaners” in between “suit not ruined, inconvenience” and “suit not ruined” in the preference ordering. We consider lotteries $L_q$ in which Leonardo gets outcome “suit not ruined” with probability $q$ and outcome “suit not ruined, inconvenience” with probability $1 - q$. The utility of “suit goes to cleaners” is defined to be the expected utility of the lottery $L_q$ for which Leonardo would be indifferent between lottery $L_q$ and being assured of “suit goes to cleaners.” We then have
