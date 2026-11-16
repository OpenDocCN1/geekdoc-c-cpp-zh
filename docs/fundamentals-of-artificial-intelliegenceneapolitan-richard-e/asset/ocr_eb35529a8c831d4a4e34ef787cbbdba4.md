![](bbox=[0.17, 0.08, 0.84, 0.38])

Figure 8.3 The decision tree modeling the investment decision concerning NASDIP when the other choice is to buy an option on NASDIP.

After solving it, we show expected utilities above nodes and an arrow to the alternative chosen. The solved decision tree, given the decision tree in Figure 8.1, is shown in Figure 8.2. The entire process of identifying the components of a problem, structuring the problem as a decision tree (or influence diagram), solving the decision tree (or influence diagram), performing sensitivity analysis (discussed in Chapter 6, Section 8.6), and possibly reiterating these steps is called decision analysis.

Example 8.2 Suppose you are in the same situation as in Example 8.1, except, instead of considering leaving your money in the bank, your other choice is to buy an option on NASDIP. The option costs $1000, and it allows you to buy 500 shares of NASDIP at $11 per share in one month. So if NASDIP is at $5 or $0 per share in one month, you would not exercise your option, and you would lose $1000. However, if NASDIP is at $20 per share in one month, you would exercise your option, and your $1000 investment would be worth

```
500($20 - $11) = $4500.
```

Figure 8.3 shows a decision tree representing this problem instance. From that tree, we have

```
EU(Buy option) = EU(NASDIP2) = .25($0) + .25($0) + .5($4500) = $2250.
```

Recall that EU(Buy NASDIP) is only $1375. So our decision would be to buy the option. It is left as an exercise to show the solved decision tree.