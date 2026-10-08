| Table 4-1 | Simple Operators |
| --- | --- |
| Operator | What It Means |
| - (unary) | Take the negative of |
| * | Multiply |
| / | Divide |
| + | Add |
| - (binary) | Substract |
| % | Modulo |

Most of these operators in the table are binary operators because they operate on two values: one on the left side of the operator and one on the right side. The exception is the unary negative. However, it's just straightforward as the others, as shown in this example:

```
int n1 = 5;
int n2 = -n1; // n2 now has the value -5.
```

The value of -n is the negative of the value of n.

The modulo operator may not be as familiar to you as the others. Modulo is similar to the remainder after division. Thus, 5 % 3 is (5 / 3 = 1, remainder 2), and 25 % 3 is (25 / 3 = 8, remainder 1). Read it "five modulo three" or "five mod third." Even numbers mod 2 are 0: 6 % 2 = 0 (6/2 = 3, remainder 0).

The arithmetic operators other than modulo are defined for all numeric types. The modulo operator is not defined for floating-point numbers because you have no remainder after division of floating-point values.

# Operating orders

The value of some expressions may not be clear. Consider, for the example:

```
int n = 5 * 3 + 2;
```

Does the programmer "multiply 5 times and then add 2," which is 17, or "multiply 5 times the sum of 3 and 2," which gives you 25?

C# generally executes common operators from left to right. So, the preceding example assigns the value 17 to the variable n.

![](bbox=[0.145, 0.815, 0.225, 0.905])