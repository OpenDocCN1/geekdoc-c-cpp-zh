| `||` | `&&` |
|---|---|
| `!` | `!` |

> **Notice:** Please note that the NOT operator (`!`) remains intact.

For example,
if the original Boolean expression is `$x > 5 && $y == 3`,
the negated Boolean expression becomes `$x <= 5 || $y != 3`.

# Exercise 15.7-1 — *Negating Boolean Expressions*

*Negate the following Boolean expressions using both approaches.*

+   i. `$b != 4`
+   
+   ii. `$a * 3 + 2 > 0`
+   
+   iii. `!($a == 5 && $b >= 7)`
+   
+   iv. `$a == true`
+   
+   v. `$b > 7 && !($x > 4)`
+   
+   vi. `$a == 4 || $b != 2`

# Solution

# First Approach

+   i. `!($b != 4)`
+   
+   ii. `!($a * 3 + 2 > 0)`
+   
+   iii. `!(!($a == 5 && $b >= 7))`, or the equivalent `$a == 5 && $b >= 7`
+   
+   iv. `!($a == true)`
+   
+   v. `!($b > 7 && !($x > 4))`
+   
+   vi. `!($a == 4 || $b != 2)`

> **Notice:** Two negations result in an affirmative. That is, two NOT (`!`) operators in a row negate each other.

# Second Approach

+   i. `$b == 4`
+   
+   ii. `$a * 3 + 2 <= 0`
+   
+   iii. `!($a != 5 || $b < 7)`
+   
+   iv. `$a != true`
+   
+   v. `$b <= 7 || !($x <= 4)`
+   
+   vi. `$a != 4 && $b == 2`

> **Notice:** Please note that arithmetic operators are **not** negated. Don’t you ever *dare* replace the plus (`+`) with a minus (`-`) operator!

> **Notice:** Please note that the NOT operator (`!`) remains intact.