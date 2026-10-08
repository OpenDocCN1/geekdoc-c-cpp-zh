# 5.2 Arithmetic Operators

![](bbox=[0.215, 0.115, 0.688, 0.243])

Figure 5.1: PEMDAS rule in mathematics

| Precedence | Operators | Description | Associativity |
| --- | --- | --- | --- |
| 1 | () | Parentheses | Left to right |
| 2 | [] | Array subscript | Left to right |
| 3 | -> | Member access | Left to right |
| 4 | ++ -- | Pre/post increment and decrement | Left to right |
| 5 | + - ! | Unary operators | Right to left |
| (type) | & | Indirection and address | Right to left |
| 6 | * / % | Multiplicative | Left to right |
| 7 | + - | Additive | Left to right |
| 8 | >> | Shift | Left to right |
| 9 | < <= >= | Relational operators | Left to right |
| 10 | == != | Equality and inequality | Left to right |
| 11 | & | Bitwise AND | Left to right |
| 12 | ^ | Bitwise XOR | Left to right |
| 13 | \| | Bitwise OR | Left to right |
| 14 | && | Logical AND | Left to right |
| 15 | || | Logical OR | Left to right |
| 16 | ? | Conditional operator | Left to right |
| 17 | = += -= *= /= | Assignment operators | Right to left |
| % &= \|= ^= &= | | Right to left |
| <<= >>= | | Left to right |

right-to-left based on associativity. Associativity decides the order in which operators at the same precedence level are processed. Table 5.2 lists the C operators sorted by precedence and associativity.

Arithmetic expressions can involve multiple operators to perform intricate calculations. Programmers should be aware of operator precedence and grouping to achieve the desired result.

```
int result = a + b * c; // Multiplication first then addition
```