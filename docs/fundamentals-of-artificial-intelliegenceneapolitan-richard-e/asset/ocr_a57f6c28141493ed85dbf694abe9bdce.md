# 5.2 Random Variables

In this section we present the formal definition and mathematical properties of a random variable. In Section 5.4 we show how they are developed in practice.

# 5.2.1 Probability Distributions of Random Variables

Definition 5.5 Given a probability space \((\Omega, P)\), a random variable \(X\) is a function whose domain is \(\Omega\).

The range of \(X\) is called the space of \(X\).

Example 5.9 Let \(\Omega\) contain all outcomes of a throw of a pair of six-sided dice, and let \(P\) assign 1/36 to each outcome. Then \(\Omega\) is the following set of ordered pairs:

\(\Omega = \{(1, 1), (1, 2), (1, 3), (1, 4), (1, 5), (1, 6), (2, 1), (2, 2), \dots, (6, 5), (6, 6)\}\).

Let the random variable \(X\) assign the sum of each ordered pair to that pair, and let the random variable \(Y\) assign \(odd\) to each pair of odd numbers and \(even\) to a pair if at least one number in that pair is an even number. The following table shows some of the values of \(X\) and \(Y\).

| e | X(e) | Y(e) |
|---|---|---|
| (1,1) | 2 | odd |
| (1,2) | 3 | even |
| ... | ... | ... |
| (2,1) | 3 | even |
| ... | ... | ... |
| (6,6) | 12 | even |

The space of \(X\) is \(\{2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12\}\), and that of \(Y\) is \(\{odd, even\}\).

For a random variable \(X\), we use \(X = x\) to denote the subset containing all elements \(e \in \Omega\) that \(X\) maps to the value of \(x\). That is,

\(X = x\) represents the event \(\{e \text{ such that } X(e) = x\}\).

Note the difference between \(X\) and \(x\): small \(x\) denotes any element in the space of \(X\), whereas \(X\) is a function.

Example 5.10 Let \(\Omega, P\), and \(X\) be as in Example 5.9. Then

\(X = 3\) represents the event \(\{(1, 2), (2, 1)\}\) and

\(P(X = 3) = \frac{1}{18}\).