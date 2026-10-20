| Assignment operator | Sample expression | Explanation | Assigns |
|---|---|---|---|
| *Assume: int c = 3, d = 5, e = 4, f = 6, g = 12;* |  |  |  |
| += | c += 7 | c = c + 7 | 10 to c |
| -= | d -= 4 | d = d - 4 | 1 to d |
| *= | e *= 5 | e = e * 5 | 20 to e |
| /= | f /= 3 | f = f / 3 | 2 to f |
| %= | g %= 9 | g = g % 9 | 3 to g |

# Fig. 4.13 | Arithmetic compound assignment operators.

called c using the increment operator, ++, rather than the expression c = c + 1 or c += 1. An increment or decrement operator that's prefixed to (placed before) a variable is referred to as the prefix increment or prefix decrement operator, respectively. An increment or decrement operator that's postfixed to (placed after) a variable is referred to as the postfix increment or postfix decrement operator, respectively.

| Operator | Operator name | Sample expression | Explanation |
|---|---|---|---|
| ++ | prefix increment | ++a | Increment a by 1, then use the new value of a in the expression in which a resides. |
| ++ | postfix increment | a++ | Use the current value of a in the expression in which a resides, then increment a by 1. |
| -- | prefix decrement | --b | Decrement b by 1, then use the new value of b in the expression in which b resides. |
| -- | postfix decrement | b-- | Use the current value of b in the expression in which b resides, then decrement b by 1. |

# Fig. 4.14 | Increment and decrement operators.

Using the prefix increment (or decrement) operator to add 1 to (or subtract 1 from) a variable is known as preincrementing (or predecrementing). This causes the variable to be incremented (decremented) by 1; then the new value of the variable is used in the expression in which it appears. Using the postfix increment (or decrement) operator to add 1 to (or subtract 1 from) a variable is known as postincrementing (or postdecrementing). This causes the current value of the variable to be used in the expression in which it appears; then the variable's value is incremented (decremented) by 1.

> Good Programming Practice 4.4
> Unlike binary operators, the unary increment and decrement operators should be placed next to their operands, with no intervening spaces.

Figure 4.15 demonstrates the difference between the prefix increment and postfix increment versions of the ++ increment operator. The decrement operator (-- ) works similarly.