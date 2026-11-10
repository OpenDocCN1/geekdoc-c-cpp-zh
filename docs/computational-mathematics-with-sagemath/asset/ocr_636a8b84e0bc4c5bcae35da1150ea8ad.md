```
```text
sage: is_full_hand({(3, 'Clubs'), (3, 'Spades'), (3, 'Hearts'),
....:              (2, 'Clubs'), (2, 'Spades')})
True
```
```

We now estimate experimentally the proportion of full hands. More generally, the following function estimates the proportion of elements of the finite set $S$ satisfying predicate. It assumes that the set has a `random_element` method with uniform distribution.

```
```text
sage: def estimate_proportion(S, predicate, n):
....:     count = 0
....:     for i in range(n):
....:         if predicate(S.random_element()):
....:             count += 1
....:     return count/n
```
```

```
```text
sage: float(estimate_proportion(Hands, is_full_hand, 10000))
0.0014
```
```

Let us now perform the computation symbolically. To identify a full hand, we have to choose a pair of distinct values, one for the three-of-a-kind, one for the pair, and a set of three suits for the three-of-a-kind, and two suits for the pair:

```
```text
sage: FullHands = cartesian_product([Arrangements(Values, 2),
....:     Subsets(Suits, 3), Subsets(Suits, 2)])
```
```

Here is, for example, a full hand with a three-of-a-kind of twos, and a pair of threes:

```
```text
sage: FullHands.first()
([2, 3], {'Hearts', 'Spades', 'Diamonds'}, {'Hearts', 'Diamonds'})
```
```

The probability to draw a full hand is:

```
```text
sage: float(FullHands.cardinality() / Hands.cardinality())
0.0014405762304921968
```
```

**Exercise 53 page 330.** *(Counting by hand complete binary trees)* There is one complete binary tree with one leaf, and one with two leaves. For $n = 3, 4$ and $5$ leaves, we find respectively $2$, $5$ and $14$ trees (for $n = 4$, see Figure 15.1).

**Exercise 54 page 340.** The compositions of $n$ with $k$ parts have a one-to-one correspondence with subsets of size $k - 1$ of $\{1, \ldots, n - 1\}$: to the set $\{i_1, i_2, \ldots, i_{k-1}\}$ where $0 < i_1 < i_2 < \cdots < i_{k-1} < n$, we associate the composition $(i_1, i_2 - i_1, \ldots, i_{k-1} - i_{k-2}, n - i_{k-1})$, and reciprocally. We deduce the enumeration formulas: there are $2^{n-1}$ compositions of $n$, and among these $\binom{n-1}{k-1}$ compositions with $k$ parts.

```
```text
sage: n=6
sage: Compositions(n).cardinality(); 2^(n-1)
32
32
sage: n=6; k=3
```
```