
If any of the following equations are true, then events A and B are independent:

```
P(A | B) = P(A) or
P(B | A) = P(B) or
P(A ∩ B) = P(A) P(B)
```

If any one of these equations are true, then so are the others.

## Bayes' Theorem

The conditional probability, P(A | B), states the probability of event A given that event B occurred. The inverse problem is to find the inverse probability, which states the probability of an earlier event given that a later one occurred. This type of probability occurs often, as in the case of medical or equipment diagnosis where symptoms appear and the problem is to find the most likely cause. The solution to this problem is Bayes' Theorem, also sometimes called Bayes' Formula, Bayes' Rule, or Bayes' Law, named after the 18th Century British clergyman and mathematician, Thomas Bayes. Bayesian theory is extensively used today in many applications. In the familiar Office Assistant, and Technical Troubleshooter Help that is provided automatically in Microsoft Office and Windows use Bayesian logic to better try and help you rather than relying on simple decision trees (Gates 00).

As an example of Bayes' Theorem, let's see how it applies to the disk drive crashes. From the conditional probability (6), there is a 75% probability a Brand X drive will crash within one year, while based on (7), the probability of a non-Brand X drive crash within one year is 50%. The inverse question is, suppose you have a drive and don't know its brand, what is the probability that if it crashes, it is Brand X? Non-Brand X?

A situation like this, in which you don't really know the drive, occurs all the time since computer manufacturers seldom make their own drives. Instead many buy drives from an original equipment manufacturer (OEM) and repackage the drives to sell under their own label. Depending on what OEM offers the lowest cost, the drive may vary from year to year with only the computer manufacturer's label remaining the same.

Given that a drive crashed, the probability of it being Brand X can be stated using conditional probability and the results (1), (5):

```
P(X | C) = P(C ∩ X) / P(C) = 0.6 / 0.7 = 6/7
```

Alternatively, using the Multiplicative Law on the numerator, and (1), (3), (6):

```
P(X | C) = P(C|X)P(X) / P(C) = (0.75)(0.8) / 0.7 = 0.6 / 0.7 = 6/7
```

The probability P(X | C) is the inverse or a posteriori probability, which states that if the drive crashed, it was Brand X. Figure 4.8 shows a decision tree

### Figure 4.8 Decision Tree for the Disk Crashes

![](img/2c460d4de56b7ffaad3834eee20beaa0_229_0.png)

for the disk crashes. The square symbol indicates an **act** or decision, and the circle indicates an **event** or occurrence. The prior probabilities are those before the experiments of measuring crashes. The posterior or inverse probabilities are those determined after the completion of the experiments. The posterior probabilities allow us to revise the prior probabilities to obtain more accurate results.

The general form of Bayes' Theorem can be written in terms of events, E, and hypotheses (assumptions), H, in the following alternative forms:

```
P(H_1 | E) = \frac{P(E \cap H_1)}{\sum_j P(E \cap H_j)}

= \frac{P(E | H_1) P(H_1)}{\sum_j P(E | H_j) P(H_j)}

= \frac{P(E | H_1) P(H_1)}{P(E)}
```

## 4.9 HYPOTHETICAL REASONING AND BACKWARD INDUCTION

Bayes' Theorem is commonly used for decision tree analysis of business and the social sciences. The method of **Bayesian decision making** is also used in the PROSPECTOR expert system to decide favorable sites for mineral exploration. PROSPECTOR achieved a great deal of fame as the first expert system to discover a valuable molybdenum deposit worth $100,000,000.

As an example of Bayesian decision making under uncertainty, let's look at the problem of oil exploration. Initially, the prospector must decide what the chances are of finding oil. If there is no evidence either for or against oil, the prospector may assign the subjective prior probabilities for oil, O, of:

P(O) = P(O') = 0.5

With no evidence, an assignment of probabilities that are equally weighted between possible outcomes is said to be made in desperation. The term in desperation does not mean that the prospector is (necessarily) in desperate need. It is a technical term for the unbiased prior assignment of probabilities. Naturally, the prospector believes that there is better than a 50-50 chance of finding oil, and so may assume the following:

P(O) = 0.6 P(O') = 0.4

A very important tool in oil and mineral exploration is the seismic survey. In this technique, dynamite or machinery creates sound pulses that travel through the earth. The sound waves are detected by microphones at various locations. By observing the arrival time of pulses and distortion of the sound waveform, it is possible to determine geologic structures and the possibility of oil and minerals. Unfortunately seismic tests are not 100 percent accurate. The sound waves may be affected by some types of geologic structures so the test reports the presence of oil when there really is none (false positive). Likewise, the test may report the absence of oil when there really is oil (false negative). Assume that the past history of the seismic test has given the following conditional probabilities, where + means a positive outcome and – is a negative outcome. Note that these conditional probabilities because the cause (oil or no oil) must have occurred before the effect (test result). A posterior probability would be from an effect (test result) back to the cause (oil or no oil). Generally, a conditional probability is forward in time while a posterior probability is backward in time.

P(+ | O) = 0.8       P(- | O) = 0.2 (false -)
P(+ | O') = 0.1 (false +)   P(- | O') = 0.9

Using the prior and conditional probabilities, we can construct the initial probability tree as shown in Figure 4.9. Also shown are the joint probabilities, which are calculated from the prior and conditional probabilities.

The Addition Law is then used to calculate the total probability of a + and a – test.

P(+) = P(+ ∩ O) + P(+ ∩ O') = 0.48 + 0.04 = 0.52
P(-) = P(- ∩ O) + P(- ∩ O') = 0.12 + 0.36 = 0.48

The P(+) and P(-) are unconditional probabilities that can now be used to calculate the posterior probabilities at the site, as shown in Figure 4.10. For example, the P(O' | -) is the posterior probability for no oil at the site based on a negative test. The joint probabilities are then computed. Notice that the joint probabilities of Figure 4.10 are the same as in Figure 4.9. The revision of probabilities

### Figure 4.9 Initial Probability Tree for Oil Exploration

![](img/2c460d4de56b7ffaad3834eee20beaa0_231_0.png)

### Figure 4.10 Revised Probability Tree for Oil Exploration

![](img/2c460d4de56b7ffaad3834eee20beaa0_231_1.png)

is necessary to give good results when experimental information, such as the seismic test results, occurs after the initial probability estimates (or guess). Figure 4.11 shows the initial Bayesian decision tree using the data from Figure 4.10. The payoffs at the bottom of the tree are positive if money is made and negative if money is lost. The assumed amounts are shown in Table 4-9. Thus, if oil is found, the payoff is $1,000,000 - $200,000 - $50,000 = $750,000 while the decision to quit after the seismic test result gives a payoff of -$50,000, and the payoff for seismic testing and drilling but no oil is of -$200,000 - $50,000 = -$250,000. Note that this payoff is not -$1,000,000 - $200,000 - $50,000 = -$1,250,000 unless you can take advantage of a tax loophole (which is not impossible since many special tax riders are attached to bills in Congress if you have a good lobbyist).

### Figure 4.11 Initial Bayesian Decision Tree for Oil Exploration

![](img/2c460d4de56b7ffaad3834eee20beaa0_232_0.png)

### Table 4.9 Payoff Table for the Oil Exploration Problem

| Item | Value |
|---|---|
| Oil lease, if successful | $1,000,000 |
| Drilling expense | –$200,000 |
| Seismic survey | –$50,000 |

In order for the prospector to make the best decision, the **expected payoff** must be calculated at event node A. The expected payoff is the amount the prospector can make by following the best course of action. To compute the expected payoff at the start, A, we must work backwards from the leaves. In probability theory, this process is called **backward induction**. That is, in order to achieve the expected payoff or goal that we want, we must reason backwards to find the causes that will lead us to the goal.

The expected payoff from an event node is the sum of the payoffs times the probabilities leading to the payoffs:

```
Expected payoff at node C
$673,077 = ($750,000) (12/13) – ($250,000) (1/13)
```

```
Expected payoff at node B
$0 = ($750,000) (1/4) – ($250,000) (3/4)
```

At the action node E, we must decide between an expected payoff of –$50,000 by quitting or $846,153 by drilling. Since $846,153 is greater than –$50,000, we will induce that this is the better action and write it over node E. The path to quitting will be **pruned** or **poisoned** by breaking it with a "=" symbol to indicate this path will not be followed, as in Figure 4.12. Likewise at action node D, the best choice between a payoff of –$50,000 and a payoff of –$500,000 is –$50,000 and so this is written at D.
