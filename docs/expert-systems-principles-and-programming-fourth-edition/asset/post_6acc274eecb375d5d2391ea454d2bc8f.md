
### Figure 4.5 Compound Probability of Rolling a Single Die to Give an Even Number and a Number Divisible by Three

![](img/2c460d4de56b7ffaad3834eee20beaa0_222_0.png)

Events that do not affect each other in any way are called independent events. For two independent events A and B, the probability is simply the product of the individual probabilities. Events A and B are said to be pairwise independent:

P(A ∩ B) = P(A) P(B)

Two events are called stochastically independent events if and only if the above formula is true. The term stochastic comes from the Greek and means “guess.” It is commonly used as a synonym for probability. Thus a stochastic experiment has a probabilistic outcome, in contrast to the nonrandom outcome of a deterministic experiment. As a stochastic experiment, try marrying and divorcing 10 people one after another and you might wind up in a happy or unhappy state. On the one hand, if you marry all ten at once you will wind up in the deterministic state of prison.

For three events you might assume that independence is:

P(A ∩ B ∩ C) = P(A) P(B) P(C)

Unfortunately, life and probability are not that simple. The formula for the mutual independence of N events requires that 2^N equations be satisfied. This requirement is summarized by the following equation, where the asterisks mean that every combination of an event and its complement must be satisfied:

P(A*_1 ∩ A*_2 ∩ ... ∩ A*_n) = P(A*_1) P(A*_2) ... P(A*_n)

For three events, the above equation for mutual independence requires that all the following equations be satisfied:

- P(A ∩ B ∩ C) = P(A) P(B) P(C)
- P(A ∩ B ∩ C') = P(A) P(B) P(C')
- P(A ∩ B' ∩ C) = P(A) P(B') P(C)
- P(A ∩ B' ∩ C') = P(A) P(B') P(C')
- P(A' ∩ B ∩ C) = P(A') P(B) P(C)
- P(A' ∩ B ∩ C') = P(A') P(B) P(C')
- P(A' ∩ B' ∩ C) = P(A') P(B') P(C)
- P(A' ∩ B' ∩ C') = P(A') P(B') P(C')

The pairwise independence of every two events is not enough to guarantee mutual independence as shown in Problem 4.6.

For our die, the events of an even number and a number divisible by three definitely affect each other and so is not a stochastic experiment. The probability of an even number on one die and a number divisible by three on another is stochastic.

P(A ∩ B) = P(A) P(B) = 3/6 · 2/6 = 1/6

Now let's consider the case of the union of events, P(A ∪ B). Define n as a function that returns the number of elements of a set. If we add the number of elements in A to those in B and divide by the total elements in the sample space n(S),

P(A ∪ B) = (n(A) + n(B)) / n(S) = P(A) + P(B)

then the result will be too big if the sets overlap. If you look at Figure 4.5, applying this formula gives:

P(A ∪ B) = (3 + 2) / 6 = 5 / 6

but you can easily see that there are only four elements in the union since:

A ∪ B = { 2, 3, 4, 6 }

The problem is that just adding n(A) to n(B) is counting the set intersection {6} twice since it belongs to both A and B.

The correct formula simply requires subtracting the extra probability of set intersection:

P(A ∪ B) = P(A) + P(B) - P(A ∩ B)

which for our die reduces to:

P(A ∪ B) = 3/6 + 2/6 - 1/6 = 4/6 = 2/3

Formula (1) holds when the sets are disjoint and so have no elements in common. It is a special case of formula (2), which is called the Additive Law. The Additive Law can also be derived as a theorem using the three axioms of probability discussed earlier. The Additive Law for three events is:

P(A ∪ B ∪ C) = P(A) + P(B) + P(C)
- P(A ∩ B) - P(A ∩ C) - P(B ∩ C)
+ P(A ∩ B ∩ C)

Other laws for neither A nor B and the exclusive-OR of A and B can also be derived from the axioms. The value of these laws for compound probabilities is that (1) experiments do not have to be made for each possible combination of probabilities and (2) the individual elements of large sample spaces do not have to be counted.

## 4.8 CONDITIONAL PROBABILITIES

Events that are not mutually exclusive influence one another. Knowing that one event has occurred may cause us to revise the probability that another event will occur.

### Multiplicative Law

The probability of an event A, given that event B occurred, is called a conditional probability and is indicated by P(A | B). The conditional probability is defined as:

P(A | B) = P(A ∩ B) / P(B) for P(B) ≠ 0

The probability P(B) is the a priori or prior probability before any information is known. When used in association with a conditional probability, the prior probability is sometimes called the unconditional probability or an absolute probability.

This definition of conditional probability can be intuitively explained if you look at the example of Figure 4.6, which is a sample space of eight events. From Figure 4.6 the probabilities can be calculated as the ratios of the number of events, n(A) or n(B), to the total number in the sample space n(S). That is,

P(A) = n(A) / n(S) = 4 / 8

P(B) = n(B) / n(S) = 6 / 8

### Figure 4.6 Sample Space of Two Intersecting Events

![](img/2c460d4de56b7ffaad3834eee20beaa0_224_0.png)

If we know that event B has occurred, the reduced sample space is just that of B:

n(S) = 6

Since B occurred, only the events in A that are associated with B are considered:

P(A | B) = n(A ∩ B) / n(B) = 2 / 6

To express the result in terms of probabilities, just divide the numerator and denominator of the above by n(S):

P(A | B) = (n(A ∩ B) / n(S)) / (n(B) / n(S))
= P(A ∩ B) / P(B) for P(B) ≠ 0

The Multiplicative Law of probability for two events is then defined as:

P(A ∩ B) = P(A | B) P(B)

which is equivalent to the following:

P(A ∩ B) = P(B | A) P(A)

The Multiplicative Law for three events is the following:

P(A ∩ B ∩ C) = P(A | B ∩ C) P(B | C) P(C)

and the Generalized Multiplicative Law is:

P(A_1 ∩ A_2 ∩ ... ∩ A_n) = P(A_n | A_1 ∩ ... ∩ A_{n-1}) ··· P(A_2 | A_1) P(A_1)

As an example of probabilities, Table 4.6 shows hypothetical probabilities of a disk crash using a Brand X drive within one year.

| | Brand X | Not Brand X | Total of Rows |
|---|---|---|---|
| Crash C | 0.6 | 0.1 | 0.7 |
| No Crash C' | 0.2 | 0.1 | 0.3 |
| Total of Columns | 0.8 | 0.2 | 1.0 |

The probabilities of 0.6, 0.1, 0.2, and 0.1 inside the middle region in the table are called interior probabilities and represent the intersections of events. The sum of the rows and columns are displayed as Totals, and are called marginal probabilities because they lie on the margin of the table.

Tables 4.7 and 4.8 show the set and probability meanings in more detail. Figure 4.7 shows the Venn diagram of the sample space intersection. From Table 4.8 you can see that the sum of total row probabilities and total column probabilities is 1.

| | X | X' | Total of Rows |
|---|---|---|---|
| C | C ∩ X | C ∩ X' | C = (C ∩ X) ∪ (C ∩ X') |
| C' | C' ∩ X | C' ∩ X' | C' = (C' ∩ X) ∪ (C' ∩ X') |
| Total of Columns | X = (C ∩ X) ∪ (C' ∩ X) | X' = (C ∩ X') ∪ (C' ∩ X') | S (Sample Space) |

| | X | X' | Total of Rows |
|---|---|---|---|
| C | P(C ∩ X) | P(C ∩ X') | P(C) |
| C' | P(C' ∩ X) | P(C' ∩ X') | P(C') |
| Total of Columns | P(X) | P(X') | 1.0 |

### Figure 4.7 The Sample Space Interpretation of Two Sets

![](img/2c460d4de56b7ffaad3834eee20beaa0_226_0.png)

Using Table 4.8, the probabilities of all events can be calculated. Some probabilities are:

- (1) The probability of a crash for both Brand X and not Brand X (the sample space) is:
  P(C) = 0.7

- (2) The probability of no crash for the sample space is:
  P(C') = 0.3

- (3) The probability of using Brand X is:
  P(X) = 0.8

- (4) The probability of not using Brand X is:
  P(X') = 0.2

- (5) The probability of a crash and using Brand X is:
  P(C ∩ X) = 0.6

- (6) The probability of a crash, given that Brand X is used, is:
  P(C | X) = P(C ∩ X) / P(X) = 0.6 / 0.8 = 0.75

- (7) The probability of a crash, given that Brand X is not used, is:
  P(C | X') = P(C ∩ X') / P(X') = 0.1 / 0.2 = 0.50

Probabilities (5) and (6) may appear to have similar meanings when you read their descriptions. However, (5) is simply the intersection of two events, while (6) is a conditional probability. The meaning of the intersection, (5), is the following:

> If a disk drive is picked randomly, then 0.6 of the time it will be Brand X and have crashed.

In other words, we are just picking samples from the population of disk drives. Some of those drives are Brand X and have crashed (0.6), some are not Brand X and have crashed (0.1), some are Brand X and have not crashed (0.2), and some are not Brand X and have not crashed (0.1).

In contrast, the meaning of the conditional probability (6) is very different:

> If a Brand X drive is picked, then 0.75 of the time it will have crashed.

Notice that in the conditional probability we are picking those items (Brand X) of interest to us and considering them as the new sample space.
