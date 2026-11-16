# 8.2.2 Solving Influence Diagrams

We first illustrate how influence diagrams can be solved by presenting some examples. Then we show solving influence diagrams using the package Netica.

# 8.2.3 Techniques for Solving Influence Diagrams

Next, we show how to solve influence diagrams.

Example 8.16 Consider the influence diagram in Figure 8.13, which was developed in Example 8.9. To solve the influence diagram, we need to determine which decision choice has the largest expected utility. The expected utility of a decision choice is the expected value E of U given the choice is made. We have

```
EU(d1) = E(U|d1)
= P($5|d1)U(d1, $5) + P($10|d1)U(d1, $10) + P($20|d1)U(d1, $20)
= (.25)($500) + (.25)($1000) + (.5)($2000)
= $1375
```

```
EU(d2) = E(U|d2)
= P($5|d2)U(d2, $5) + P($10|d2)U(d2, $10) + P($20|d2)U(d2, $20)
= (.25)($1005) + (.25)($1005) + (.5)($1005)
= $1005.
```

The utility of our decision is therefore

```
EU(D) = max(EU(d1), EU(d2))
= max($1375, $1005) = $1375,
```

and our decision choice is d1.

Notice in the previous example that the probabilities do not depend on the decision choice. This is because there is no edge from D to NASDIP. In general, this is not always the case, as the next example illustrates.

Example 8.17 Consider the influence diagram in Figure 8.15, which was developed in Example 8.11. We have

```
EU(d1) = E(U|d1)
= P($5|d1)U(d1, $5) + P($20|d1)U(d1, $20)
= (.32)($50,000) + (.68)($200,000)
= $152,000
```

```
EU(d2) = E(U|d2)
= P($5|d2)U(d2, $5) + P($20|d2)U(d2, $20)
= (.42)($0) + (.58)($250,000)
= $145,000
```