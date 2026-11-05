| Category | Expression | Description |
|---|---|---|
| Multiplicative | `x * y` | Multiplication |
|  | `x / y` | Division |
|  | `x % y` | Remainder |
| Additive | `x + y` | Addition, string concatenation, delegate combination |
|  | `x - y` | Subtraction, delegate removal |
| Shift | `x << y` | Shift left |
|  | `x >> y` | Shift right |
| Relational and type testing | `x < y` | Less than |
|  | `x > y` | Greater than |
|  | `x <= y` | Less than or equal |
|  | `x >= y` | Greater than or equal |
|  | `x is T` | Return true if x is a T, false otherwise |
|  | `x as T` | Return x typed as T, or null if x is not a T |
| Equality | `x == y` | Equal |
|  | `x != y` | Not equal |
| Logical AND | `x & y` | Integer bitwise AND, boolean logical AND |
| Logical XOR | `x ^ y` | Integer bitwise XOR, boolean logical XOR |
| Logical OR | `x | y` | Integer bitwise OR, boolean logical OR |
| Conditional AND | `x && y` | Evaluates y only if x is true |
| Conditional OR | `x || y` | Evaluates y only if x is false |
| Null coalescing | `x ?? y` | Evaluates to y if x is null, to x otherwise |
| Conditional | `x ? y : z` | Evaluates y if x is true, z if x is false |