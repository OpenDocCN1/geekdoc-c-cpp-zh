# 4.6. INTRODUCTION TO LR PARSING: SIMPLE LR

**Example 4.48:** Every SLR(1) grammar is unambiguous, but there are many unambiguous grammars that are not SLR(1). Consider the grammar with productions

```
S → L = R | R
L → * R | id
R → L                                      (4.49)
```

Think of L and R as standing for l-value and r-value, respectively, and * as an operator indicating “contents of.”⁵ The canonical collection of sets of LR(0) items for grammar (4.49) is shown in Fig. 4.39.

![](bbox=[0.298, 0.351, 0.704, 0.626])

*Figure 4.39: Canonical LR(0) collection for grammar (4.49)*

Consider the set of items I₂. The first item in this set makes ACTION[2, =] be “shift 6.” Since FOLLOW(R) contains = (to see why, consider the derivation S ⇒ L = R ⇒ *R = R), the second item sets ACTION[2, =] to “reduce R → L.” Since there is both a shift and a reduce entry in ACTION[2, =], state 2 has a shift/reduce conflict on input symbol =.

Grammar (4.49) is not ambiguous. This shift/reduce conflict arises from the fact that the SLR parser construction method is not powerful enough to remember enough left context to decide what action the parser should take on input =, having seen a string reducible to L. The canonical and LALR methods, to be discussed next, will succeed on a larger collection of grammars, including

> ⁵ As in Section 2.8.3, an l-value designates a location and an r-value is a value that can be stored in a location.