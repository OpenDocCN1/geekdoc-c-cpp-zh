# 3.2.2 Relational Operators

# Concept

+   1. Relation operators are used for the relative comparison between two values.
+   2. Here is the list of table containing the various relational operators

# Explanation

| Relational Operator | Description | Example |
|---|---|---|
| < | Is less than | 10<20 is true |
| <= | Is greater or equal to | 10<=5 is false |
| > | Is greater than | 5>2 is true. |
| >= | Is greater than or equal to | 2>=2 is true. |
| == | Is equal to | 5==12 is false. |
| != | Is not equal to | 5!=12 is true. |

# Example

```
```csharp
//Illustration of use of relational operators.
using System;
namespace CSharpOperators
{
class Relational
{
static void Main()
{
int num1 = 20;
int num2 = 25;
int num3 = 5;
Console.WriteLine("\n num1 < num2 is {0}",(num1 < num2));
Console.WriteLine("\n num1 <=b is {0}",(num1 <= num2));
Console.WriteLine("\n num1 > num3 is {0}",(num1 > num3));
Console.WriteLine("\n num1 >= num3 is {0}",(num1 >= num2));
Console.WriteLine("\n num1 ==b is {0}",(num1 == num2));
Console.WriteLine("\n num1!=b is {0}",(num1 != num2));
Console.ReadLine();
}
}
}
```
```

Input
nil