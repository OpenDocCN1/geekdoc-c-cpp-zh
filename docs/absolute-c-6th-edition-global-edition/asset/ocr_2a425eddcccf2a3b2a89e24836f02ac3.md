# Display 2.3  Precedence of Operators (part 2 of 2)

*All operators in part 2 are of lower precedence than those in part 1.*

| Operator | Description |
|---|---|
| `<` | Less than |
| `>` | Greater than |
| `<=` | Less than or equal to |
| `>=` | Greater than or equal to |
| `==` | Equal |
| `!=` | Not equal |
| `&&` | And |
| `||` | Or |
| `=` | Assignment |
| `+=` | Add and assign |
| `-=` | Subtract and assign |
| `*=` | Multiply and assign |
| `/=` | Divide and assign |
| `%=` | Modulo and assign |
| `? :` | Conditional operator |
| `throw` | Throw an exception |
| `,` | Comma operator |

lowest precedence
(done last)

If one operation is performed before another, the operation that is performed first is said to have **higher precedence**. All the operators in a given box in Display 2.3 have the same precedence. Operators in higher boxes have higher precedence than operators in lower boxes.

When operators have the same precedences and the order is not determined by parentheses, then unary operations are done right to left. The assignment operations are also done right to left. For example, `x = y = z` means `x = (y = z)`. Other binary

higher precedence