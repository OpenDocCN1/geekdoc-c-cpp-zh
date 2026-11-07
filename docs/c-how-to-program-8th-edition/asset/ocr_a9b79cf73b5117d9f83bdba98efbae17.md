Thus the assignment c += 3 adds 3 to c. Figure 4.17 shows the arithmetic assignment operators, sample expressions using these operators and explanations.

| Assignment operator | Sample expression | Explanation | Assigns |
|---|---|---|---|
| *Assume: int c = 3, d = 5, e = 4, f = 6, g = 12;* | | | |
| += | c += 7 | c = c + 7 | 10 to c |
| -= | d -= 4 | d = d - 4 | 1 to d |
| *= | e *= 5 | e = e * 5 | 20 to e |
| /= | f /= 2 | f = f / 2 | 2 to f |
| %= | g %= 9 | g = g % 9 | 3 to g |

**Fig. 4.17**  |  Arithmetic assignment operators.

# 4.12 Increment and Decrement Operators

In addition to the arithmetic assignment operators, C++ also provides two unary operators for adding 1 to or subtracting 1 from the value of a numeric variable. These are the unary increment operator, ++, and the unary decrement operator, --, which are summarized in Fig. 4.18. A program can increment by 1 the value of a variable called c using the increment operator, ++, rather than the expression c = c + 1 or c += 1. An increment or decrement operator that’s prefixed to (placed *before*) a variable is referred to as the **prefix increment** or **prefix decrement** operator, respectively. An increment or decrement operator that’s postfixed to (placed *after*) a variable is referred to as the **postfix increment** or **postfix decrement** operator, respectively.

| Operator | Called | Sample expression | Explanation |
|---|---|---|---|
| ++ | preincrement | ++a | Increment by 1, then use the new value of a in the expression in which a resides. |
| ++ | postincrement | a++ | Use the current value of a in the expression in which a resides, then increment a by 1. |
| -- | predecrement | --b | Decrement b by 1, then use the new value of b in the expression in which b resides. |
| -- | postdecrement | b-- | Use the current value of b in the expression in which b resides, then decrement b by 1. |

**Fig. 4.18**  |  Increment and decrement operators.

Using the prefix increment (or decrement) operator to add (or subtract) 1 from a variable is known as a preincrementing (or predecrementing) the variable. Preincrementing (or predecrementing) causes the variable to be incremented (decremented) by 1, then the new value of the variable is used in the expression in which it appears. Using the postfix incre-