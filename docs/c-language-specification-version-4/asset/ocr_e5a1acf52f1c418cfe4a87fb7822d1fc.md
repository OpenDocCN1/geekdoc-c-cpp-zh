| Section | Category | Operators |
|---|---|---|
| 7.6 | Primary | x.y f(x) a[x] x++ x-- new typeof default checked unchecked delegate |
| 7.7 | Unary | + - ! ~ ++x --x (T)x |
| 7.8 | Multiplicative | * / % |
| 7.8 | Additive | + - |
| 7.9 | Shift | << >> |
| 7.10 | Relational and type testing | < > <= >= is as |
| 7.10 | Equality | == != |
| 7.11 | Logical AND | & |
| 7.11 | Logical XOR | ^ |
| 7.11 | Logical OR | | |
| 7.12 | Conditional AND | && |
| 7.12 | Conditional OR | || |
| 7.13 | Null coalescing | ?? |
| 7.14 | Conditional | ?: |
| 7.17, 7.15 | Assignment and lambda expression | = *= /= %= += -= <<= >>= &= ^= |= => |

When an operand occurs between two operators with the same precedence, the associativity of the operators controls the order in which the operations are performed:

+   - Except for the assignment operators, all binary operators are left-associative, meaning that operations are performed from left to right. For example, x + y + z is evaluated as (x + y) + z.
+   - The assignment operators and the conditional operator (?:) are right-associative, meaning that operations are performed from right to left. For example, x = y = z is evaluated as x = (y = z).

Precedence and associativity can be controlled using parentheses. For example, x + y * z first multiplies y by z and then adds the result to x, but (x + y) * z first adds x and y and then multiplies the result by z.

# 7.3.2 Operator overloading

All unary and binary operators have predefined implementations that are automatically available in any expression. In addition to the predefined implementations, user-defined implementations can be introduced by including operator declarations in classes and structs (§10.10). User-defined operator implementations always take precedence over predefined operator implementations: Only when no applicable user-defined operator implementations exist will the predefined operator implementations be considered, as described in §7.3.3 and §7.3.4.

The overloadable unary operators are:
    +  -  !  ~  ++  --  true  false

Although true and false are not used explicitly in expressions (and therefore are not included in the precedence table in §7.3.1), they are considered operators because they are invoked in several expression