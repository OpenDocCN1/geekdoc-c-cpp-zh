Relational and logical operators have a hierarchy of execution similar to arithmetic operators. Table 4.2 lists the precedence of these operators in relation to the other operators you have used.

Table 4.2 Operator Precedence and Associativity

| Operator | Associativity |
| ! unary -- ++ | Right to left |
| * / | Left to right |
| + | Left to right |
| <= == >= | Left to right |
| == != | Left to right |
| && | Left to right |
| || | Left to right |
| += -= *= /= | Right to left |

The following chart illustrates an operator's precedence and associativity to evaluate relational expressions, assuming the following declarations:

```
char key = 'm';
 i = 5, j = 7, k = 12;
double x = 22.5;
```

| Expression | Equivalent Expression | Value | Interpretation |
| i + 2 == k - 1 | (i + 2) == (k - 1) | 0 | false |
| 3 * i - j < 22 | (3 * i) < 22 | 1 | true |
| i + 2 * j > k | (i + (2 * j)) > (3k) | 1 | true |
| k + 3 <= -j + 3 * i | (k + 3) <= (-j) + (3*i)) | 0 | false |
| 'a' + 1 | ('a' + 1) | 1 | true |
| key - 1 > 'p' | (key - 1) > 'p' | 0 | false |
| key + 1 == 'n' | (key + 1) == 'n' | 1 | true |
| 25 >= x + 1.0 | 25 >= (x + 1.0) | 1 | true |

With all expressions, parentheses can be used to alter the assigned operator priority and improve the reliability of relational expressions. By evaluating the expressions in parentheses first, the following compound is evaluated as:

```
(6 * 3 == 36 / 2) | (13 < 3 * 3 + 4) && (6 - 2 < 5)
(18 == 18) | (13 < 9 + 4) && (4 < 5)
| (13 < 13) && !1
| 0
| 0
```