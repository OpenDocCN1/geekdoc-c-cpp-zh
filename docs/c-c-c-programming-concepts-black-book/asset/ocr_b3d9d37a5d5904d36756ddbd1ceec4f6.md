# Table 17.2: Operator Precedence

| Category | Operators | Associativity |
|---|---|---|
| Primary | (x), x.y, f(x), x++, x--, new, typeof, sizeof, checked, unchecked | Left associative |
| Unary | +(unary), -(unary), ~, ++x, --x, (T)x | Left associative |
| Multiplicative | *, /, % | Left associative |
| Additive | +, - | Left associative |
| Shift | <<, >> | Left associative |
| Relational and type testing | >, <, >=, <=, is, as | Left associative |
| Equality | ==, != | Left associative |
| Logical AND | & | Left associative |
| Logical XOR | ^ | Left associative |
| Logical OR | \| | Left associative |
| Conditional OR | \|\| | Left associative |
| Conditional AND | && | Left associative |
| Conditional | ?: | Right associative |
| Assignment | = *= /= %= += -= <<= >>= &= ^= \|= | Right associative |

In Table 17.2, the operators in the top rows have the higher precedence over the operators in the lower rows. Moreover, the operators on the left side on each row have the higher order of precedence over the operators in the right side of each row.

Associativity in C# can be of two types; left and right. Operators with left associativity are evaluated from left to right and operators with right associativity are evaluated from right to left. As an example of left associativity, we can consider the plus operation where the left expression is evaluated first and then the expression at the right is evaluated. On the other hand, assignment operator is right associative, as the expression to its right is evaluated before the assignment operation is invoked. The operator precedence and their associativity ensures certainty and integrity of the evaluation. Listing 17.7 shows an example of the operator precedence:

# Listing 17.7: Showing an Example to Illustrate Operator Precedence

```
```csharp
using System;
class Program
{
    public static void Main()
    {
        int firstNumber = 50;
        int secondNumber = 30;
        int thirdNumber = 10;
        Console.WriteLine("Calculating firstNumber * secondNumber / thirdNumber");
        Console.WriteLine(firstNumber * secondNumber / thirdNumber);
        Console.WriteLine("Calculating firstNumber / secondNumber * thirdNumber");
        Console.WriteLine(firstNumber / secondNumber * thirdNumber);
        Console.WriteLine("Calculating (firstNumber / secondNumber) * thirdNumber");
        Console.WriteLine((firstNumber / secondNumber) * thirdNumber);
    }
}
```
```