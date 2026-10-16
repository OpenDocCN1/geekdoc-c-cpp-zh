# Bayes Theorem

What we have seen so far are called classic probability theories championed in the 17th century in France.

There is another system of probability, invented and advanced by Bayes in the 18th century in England (see Box 11.4 for a short biography).

In Bernoulli's system, the future is predicted by current probability derived from current data. In the Bayesian system of thinking, the probability of a future event is influenced by history too. Future probability is a product of current and historic probabilities. Extending it further, future probability is a product probability derived from data and theoretical probability derived from knowledge. Bayes boldly combined soft (subjective) and hard (derived from data) probabilities, a notion that remained unacceptable to many statisticians for years but widely adopted now. Bayes used the notion of conditional probability.

We can define conditional probability in terms of absolute probabilities: P(A|B) = P(A and B)/P(B); that is, the probability that A and B are both true divided by the probability that B is true.

Bayes used some special terms. Future probability is known as posterior probability. Historic probability is known as prior probability. Future probability can only be a likelihood, an expression of chance softer than the rigorous term probability. Future probability is a conditional probability.

# A Clinical Lab Example

A simple illustration of the Bayes analysis is provided by Trevor Lohrbeer in Bayesian Maths for Dummies [4]. The gist of this analysis is as follows:

A person tests positive in a lab. The lab has a reputation of 99% correct diagnosis but also has false alarm probability of 5%. There is a background information that the disease occurs in 1 in 1000 people (0.1% probability). Intuitively one would expect the probability that the person has the disease is 99%, based on the lab's reputation. Two other probabilities are working in this problem: a background probability of 0.1% and a false alarm probability of 5%. Bayes theorem allows us to combine all the three probabilities and predict the chance of the person having the disease as 1.94%. This is dramatically less than an intuitive guess.

The Bayesian breakthrough is in that general truth (or disease history) prevails upon fresh laboratory evidence. Data 11.1 presents the following three probabilities that define the situation.

+   P₁: probability of correct diagnosis
+   P₂: probability of false alarm
+   P₃: prevalent disease probability (background history)