Table 4-3 defines the operator `!` (not). When you use the `!` operator, `!true` is `false` and `!false` is `true`. Putting `!` in front of a logical expression reverses the value of that logical expression.

# TABLE 4-3  The `!` (Not) Operator

| Expression | !(Expression) |
|---|---|
| `true` (nonzero) | `false` (0) |
| `false` (0) | `true` (1) |

# EXAMPLE 4-10

| Expression | Value | Explanation |
|---|---|---|
| `!('A' > 'B')` | `true` | Because `'A' > 'B'` is `false`, `!('A' > 'B')` is `true`. |
| `!(6 <= 7)` | `false` | Because `6 <= 7` is `true`, `!(6 <= 7)` is `false`. |

Table 4-4 defines the operator `&&` (and). From this table, it follows that Expression1 && Expression2 is `true` if and only if both Expression1 and Expression2 are `true`; otherwise, Expression1 && Expression2 evaluates to `false`.

# TABLE 4-4  The `&&` (And) Operator

| Expression1 | Expression2 | Expression1 && Expression2 |
|---|---|---|
| `true` (nonzero) | `true` (nonzero) | `true` (1) |
| `true` (nonzero) | `false` (0) | `false` (0) |
| `false` (0) | `true` (nonzero) | `false` (0) |
| `false` (0) | `false` (0) | `false` (0) |

# EXAMPLE 4-11

| Expression | Value | Explanation |
|---|---|---|
| `(14 >= 5) && ('A' < 'B')` | `true` | Because `(14 >= 5)` is `true`, `('A' < 'B')` is `true`, and `true && true` is `true`, the expression evaluates to `true`. |
| `(24 >= 35) && ('A' < 'B')` | `false` | Because `(24 >= 35)` is `false`, `('A' < 'B')` is `true`, and `false && true` is `false`, the expression evaluates to `false`. |