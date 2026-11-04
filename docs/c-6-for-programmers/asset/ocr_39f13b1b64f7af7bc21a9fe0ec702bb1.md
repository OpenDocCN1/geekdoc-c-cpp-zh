| Assignment operator | Sample expression | Explanation | Assigns |
| --- | --- | --- | --- |
| *= | e *= 5 | e = e * 5 | 20 to e |
| /= | f /= 3 | f = f / 3 | 2 to f |
| %= | g %= 9 | g = g % 9 | 3 to g |

Fig. 5.10 | Arithmetic compound assignment operators. (Part 2 of 2.)

# 5.11 Increment and Decrement Operators

C# provides two unary operators for adding 1 to or subtracting 1 from the value of a numeric variable (summarized in Fig. 5.11). These are the unary increment operator, ++, and the unary decrement operator, --, respectively. An app can increment by 1 the value of a variable called c using the increment operator, ++, rather than the expression c = c + 1 or c += 1. An increment or decrement operator that's prefixed to (placed before) a variable is referred to as the prefix increment operator or prefix decrement operator, respectively. An increment or decrement operator that's postfixed to (placed after) a variable is referred to as the postfix increment operator or postfix decrement operator, respectively.

| Operator | Sample expression | Explanation |
| --- | --- | --- |
| ++ (prefix increment) | ++a | Increments a by 1 and uses the new value of a in the expression in which a resides. |
| ++ (postfix increment) | a++ | Increments a by 1, but uses the original value of a in the expression in which a resides. |
| -- (prefix decrement) | --b | Decrements b by 1 and uses the new value of b in the expression in which b resides. |
| -- (postfix decrement) | b-- | Decrements b by 1, but uses the original value of b in the expression in which b resides. |

Fig. 5.11 | Increment and decrement operators.

Using the prefix increment (or decrement) operator to add 1 to (or subtract 1 from) a variable is known as preincrementing (or predecrementing). This causes the variable to be incremented (decremented) by 1; then the new value of the variable is used in the expression in which it appears.

Using the postfix increment (or decrement) operator to add 1 to (or subtract 1 from) a variable is known as postincrementing (or postdecrementing). This causes the current value of the variable to be used in the expression in which it appears; then the variable's value is incremented (decremented) by 1.