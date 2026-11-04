
However, if the condition is changed such that student price applies only if a person is less than 12 years old and with height less than 120cm, the statement would be rewritten as:

```
if (age < 12 && height < 120)
{
    Console.WriteLine("Student price applies");
}
```

The truth table for the And (&&) operator follows.

| Operand A | Operand B | Result |
|---|---|---|
| false | false | false |
| false | true | false |
| true | false | false |
| true | true | true |

The Not operator (!) negates the result of an expression. For example, if student price does not apply to those more than 12 years old, you could write the expression like this:

```
if (!(age <= 12))
    Console.WriteLine("Student price does not apply");
```

Following is the truth table for the Not operator.

| Operand A | Result |
|---|---|
| false | true |
| true | false |

## Short-Circuit Evaluation

C# uses short-circuiting when evaluating logical operators. In short-circuiting, the second argument in a condition is evaluated only when the first argument is not sufficient to determine the value of the entire condition. Consider the following example:

```
int div = 0;
int num = 5;
if ((div == 0) || (num / div == 1))
{
    Console.WriteLine(num); //---5---
}
```

Here the first expression evaluates to true, so there is no need to evaluate the second expression (because an Or expression evaluates to true as long as at least one expression evaluates to true). The second expression, if evaluated, will result in a division-by-zero error. In this case, it won't, and the number 5 is printed.

## Part I: C# Fundamentals

If you reverse the placement of the expressions, as in the following example, a division-by-zero error occurs:

```
if ((num / div == 1) || (div == 0))
{
    Console.WriteLine(num);
}
```

Short-circuiting also applies to the && operator — if the first expression evaluates to false, the second expression will not be evaluated because the final evaluation is already known.

## Mathematical Operators

C# supports five mathematical operators, shown in the following table.

| Operator | Description |
|---|---|
| + | Addition |
| - | Subtraction |
| / | Division |
| * | Multiplication |
| % | Modulus |

One interesting thing about the division operator (/) is that when you divide two integers, the fractional part is discarded:

```
int num1 = 6;
int num2 = 4;
double result = num1 / num2;
Console.WriteLine(result); //---1---
```

Here both num1 and num2 are integers and hence after the division result only contains the integer portion of the division. To divide correctly, one of the operands must be a noninteger, as the following shows:

```
int num1 = 6;
double num2 = 4;
double result = num1 / num2;
Console.WriteLine(result); //---1.5---
```

Alternatively, you can use type casting to force one of the operands to be of type double so that you can divide correctly:

```
int num1 = 6;
int num2 = 4;
double result = (double) num1 / num2;
Console.WriteLine(result); //---1.5---
```

The modulus operator (%) returns the remainder of a division:

```
int num1 = 6;
int num2 = 4;
int remainder = num1 % num2;
Console.WriteLine(remainder);  //---2---
```

The % operator is commonly used for testing whether a number is odd or even, like this:

```
if (num1 % 2 == 0)
    Console.WriteLine("Even");
else
    Console.WriteLine("Odd");
```

## Operator Precedence

When you use multiple operators in the same statement, you need to be aware of the precedence of each operator (that is, which operator will evaluate first). The following table shows the various C# operators grouped in the order of precedence. Operators within the same group have equal precedence (operators include some keywords).

| Category | Operators |
|---|---|
| Primary | x.y f(x) a[x] x++ x-- new typeof checked unchecked |
| Unary | + - ! ~ ++x --x (T) x |
| Multiplicative | * / % |
| Additive | + - |
| Shift | << >> |
| Relational and type testing | < > <= >= is as |
| Equality | == != |
| Logical AND | & |
| Logical XOR | ^ |
| Logical OR | \| |
| Conditional AND | && |
| Conditional OR | || |
| Conditional | ? : |
| Assignment | = *= /= %= += -= <<= >>= &= ^= |= |

When you are in doubt of the precedence of two operators, always use parentheses to force the compiler to evaluate the expression first. For example, the formula to convert a temperature from Fahrenheit to Celsius is:

```
Tc = (5/9)*(TF-32);
```

When implemented in C#, the formula looks like this:

```csharp
double fahrenheit = 100;
double celcius = 5.0 / 9.0 * fahrenheit - 32;
Console.WriteLine("{0:##.##} degrees C",celcius);  //---23.56 degrees C---
```

But this produces a wrong answer because 5.0 / 9.0 and fahrenheit - 32 must be evaluated separately before the results are added to get the final answer. What's happened is that, according to the precedence table, 5.0 / 9.0 * fahrenheit is evaluated first and then 32 is subtracted from the result. This gives the incorrect answer of 23.56 degrees C.

To correct this, you use parentheses to group all the expressions that need to be evaluated first, like this:

```csharp
double fahrenheit = 100;
double celcius = (5.0 / 9.0) * (fahrenheit - 32);
Console.WriteLine("{0:##.##} degrees C",celcius);  //---37.78 degrees C---
```

This code gives the correct answer of 37.78 degrees C.

## Preprocessor Directives

So far the programs you have seen in this chapter are pretty straightforward; you compile the entire program and run it from beginning until end. However, there are times when you want to inject debugging statements into your program — generally using methods such as Console.WriteLine() or MessageBox.Show() — and then remove them when the program is ready for deployment. But one common mistake is that programmers often forget to remove all those statements after debugging. The end result is that production code often contains many redundant code statements.

A better way is to instruct the C# compiler to conditionally omit some of the code during compilation. For example, you can delineate some parts of your code as debugging statements that should not be present in the production code. To do so, you can use preprocessor directives, which are special instructions to a special program (known as the processor) that will prepare your code before sending it to the compiler. C# supports the following preprocessor directives, most of which are discussed in the following sections:

| #define | #elif | #line | #pragma warning |
|---|---|---|---|
| #undef | #endif | #region | #pragma checksum |
| #if | #warning | #endregion |  |
| #else | #error | #pragma |  |

## #define and #undef

The #define preprocessor directive allows you to define a symbol so that you can use the #if preprocessor directive to evaluate and then make conditional compilation. To see how the #define preprocessor directive works, assume that you have a console application named TestDefine (saved in C:\ ) created using Visual Studio 2008 (see Figure 3-12).

![](img/a977a875c7c627b45d939729705a252e_134_0.png)

Figure 3-12

The Main() method is located in the Program.cs file. The program basically asks the user to enter a number and then sums up all the odd number from 1 to that number:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace TestDefine
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.Write("Please enter a number: ");
            int num = int.Parse(Console.ReadLine());
            int sum = 0;
            for (int i = 1; i <= num; i++)
            {
                //--- sum up all odd numbers---
                if (i % 2 == 1)
                    sum += i;
            }
            Console.WriteLine(
                "Sum of all odd numbers from 1 to {0} is {1}",
                num, sum);
            Console.ReadLine();
        }
    }
}
```

## Part I: C# Fundamentals

Suppose that you want to add some debugging statements to the program so that you can print out the intermediate results. The additional lines of code are highlighted:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace TestDefine
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.Write("Please enter a number: ");
            int num = int.Parse(Console.ReadLine());
            int sum = 0;
            for (int i = 1; i <= num; i++)
            {
                //---sum up all odd numbers---
                if (i % 2 == 1)
                {
                    sum += i;
                    Console.WriteLine("i={0}, sum={1}", i, sum);
                }
            }
            Console.WriteLine(
                "Sum of all odd numbers from 1 to {0} is {1}",
                num, sum);
            Console.ReadLine();
        }
    }
}
```

You do not want the debugging statements to be included in the production code so you first define a symbol (such as DEBUG) using the #define preprocessor directive and wrap the debugging statements with the #if and #endif preprocessor directives:

```csharp
#define DEBUG
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace TestDefine
{
    class Program
    {
        static void Main(string[] args)
        {
```
