# CHAPTER 2 Flow of Control

Display 2.3 Precedence of Operators (part 2 of 2)

All operators in part 2 are of lower precedence than those in part 1.

| | |
|---|---|
| < | Less than |
| > | Greater than |
| <= | Less than or to |
| >= | Greater than or equal to |
| == | Equal |
| != | Not equal |
| && | And |
| || | Or |
| = | Assignment |
| + | Add and assign |
| - | Subtract and assign |
| *= | Multiply and assign |
| /= | Divide and assign |
| %= | Modulo and assign |
| ? : | Conditional operator |
| throw | Throw an exception |
| , | Comma operator |

![](bbox=[0.68, 0.157, 0.83, 0.574])

If one operation is performed before another, the operation that is performed first is said to have higher precedence. All the operators in a given box in Display 2.3 have the same precedence. Operators in higher boxes have higher precedence than operators in lower boxes.

When operators have the same precedences and the order is not determined by parentheses, unary operations are done right to left. The assignment operations are also done right to left. For example, x = y means x = (y = z). Other binary

higher precedence