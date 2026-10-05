# 4 Operators

we do not need to worry about a possible division by 0, because if a is 0, the first operand will have a false value, and therefore the second one will not be evaluated.

If you need to test multiple conditions and some conditions execute faster than others, it'd be better to put them first. The same applies for the || operator. For example:

```
if(a > 0 && (a*a - 20*a > 35))
```

The second, more expensive, will be evaluated only if the first one is true.

# The || Operator

The || performs the logical OR operation. The value of the expression is true, if either of its operands is true. If both operands are false the result is false. For example, if we write: a = (1 < 2) || (5 > 7); it becomes 1, since the first operand is true. If we write: a = (3 != 3) || (5 > 7); it becomes 0, since all operands are false.

> Tip Similar to the && operator, the || performs “short-circuit” evaluation of its operands. If an operand is true, the compiler stops evaluating the other operands and sets the value of the expression true.

For example, in the following program b is not incremented, because the first operand (a > 2) is true.

```
#include <iostream> // Example 4.6
int main() 
{
    int a = 5, b = 8, c;

    c = (a > 2) || ((+b > 3);
    std::cout << c << ' ' << b << '\n';
    return 0;
}
```

Therefore, the program outputs: 1 8.

# EXERCISES

# C.4.2 What is the output of the following program?

```
#include <iostream>
int main() 
{
    int a = -2, b = 2, c;

    c = ((a+b) == !b);
    a = -((a < c) || (-b == c));
std::cout << (!a != -c) && (b+a == c) << ((a+c)%2 || (-(a+c-b)) << '\n';
    return 0;
}
```