Notice that the decision tree in Figure 8.3 is symmetrical, whereas the one in Figure 8.2 is not. The reason is that we encounter the same uncertain event regardless of which decision is made. Only the utilities of the outcomes are different.

Before proceeding, we address a concern you may have. That is, you be wondering how an individual could arrive at the probabilities of .25, .5, and .25 in Example 8.1. These probabilities are often not relative frequencies; rather, they are subjective probabilities that represent an individual's reasonable numeric beliefs. The individual arrives at them by a careful analysis of the situation. Methods for assessing subjective beliefs were discussed briefly in Chapter 2, Section 5.3.2 and are discussed in more detail in [Neapolitan, 1996]. Even so, you may argue that the individual surely must believe there are many more possible future values for a share of NASDIP than three. How can the individual claim the only possible values are $5, $10, and $20? You are correct. However, if further refinement of one's beliefs would not affect the decision, then it is not necessary to do so. So if the decision maker feels that a model containing more values would not result in a different decision, it is sufficient to use the model containing only the values $5, $10, and $20.

# 8.1.2 Solving More Complex Decision Trees

The general algorithm for solving decision trees is quite simple. There is a time ordering from left to right in a decision tree. That is, any node to the right of another node occurs after that node in time. The tree is solved as follows:

+   Starting at the right,
+   proceed to the left
+   passing expected utilities to chance nodes;
+   passing maximums to decision nodes;
+   until the root is reached.

We now present more complex examples of modeling with decision trees.

Example 8.3 Suppose Nancy is a high roller, and she is considering buying 10,000 shares of ICK for $10 a share. This number of shares is so high that if she purchases them, it could affect market activity and bring up the price of ICK. She also believes the overall value of the Dow Jones Industrial Average will affect the price of ICK. She feels that in one month the Dow will be at either 10,000 or 11,000. ICK will be at either $5 or $20 per share. Her other choice is to buy an option on ICK for $100,000. The option will allow her to buy 50,000 shares of ICK for $15 a share in one month. To analyze this problem instance, she constructs the following probabilities:

+   P(ICK = $5|Decision = Buy ICK, Dow = 11,000) = .2
+   P(ICK = $5|Decision = Buy ICK, Dow = 10,000) = .5
+   P(ICK = $5|Decision = Buy option, Dow = 11,000) = .3
+   P(ICK = $5|Decision = Buy option, Dow = 10,000) = .6.