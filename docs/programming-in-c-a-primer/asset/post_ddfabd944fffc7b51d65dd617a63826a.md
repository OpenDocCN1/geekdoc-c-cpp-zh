
The assignment operators and the conditional operator are right-associative. For example, x = y = z is evaluated as x = (y = z)

Precedence and associativity can be controlled using parentheses. For example, x + y * z and (x + y) * z will give different results. In the first case, y * z is done first and in the second case, x + y is done first.

Program 5.7 illustrates the use of different types of expressions.

## Program 5.7 DEMONSTRATION OF C# EXPRESSIONS

```
using System;
class Expressions
{
    public static void Main()
    {
        // Declaration and Initialization
        int a = 10, b = 5, c = 8, d = 2;
        float x = 6.4F, y = 3.0F;
        // Order of Evaluation
        int answer1 = a * b + c / d;
        int answer2 = a * (b + c) / d;
        // Modulo Operations
        int answer3 = a % c;
        float answer4 = x % y;
        // Logical Operations
        bool bool1 = a > b && c > d;
        bool bool2 = a < b && c > d;
        bool bool3 = a < b || c > d;
        bool bool4 = !(a-b == c);
        Console.WriteLine("Order of Evaluation");
        Console.WriteLine(" a * b + c / d = " + answer1);
        Console.WriteLine(" a * (b + c) / d = " + answer2);
        Console.WriteLine("Modulo Operations");
        Console.WriteLine(" a % c = " + answer3);
        Console.WriteLine(" x % y = " + answer4);
        Console.WriteLine("Logical Operations");
        Console.WriteLine(" a > b && c > d = " + bool1);
        Console.WriteLine(" a < b && c > d = " + bool2);
        Console.WriteLine(" a < b || c > d = " + bool3);
        Console.WriteLine(" !(a-b == c) = " + bool4);
    }
}
```

Program 5.7 outputs the following:

Order of Evaluation
    a * b + c / d = 54
    a * (b + c) / d = 65
Modulo Operations
    a % c = 2
    x % y = 0.4

### Logical Operations

-   a > b && c > d = true
-   a < b && c > d = false
-   a < b || c > d = true
-   !(a-b == c) = true

## MATHEMATICAL FUNCTIONS

Often, we may need to use trigonometric functions and logarithms. The System namespace defines a class known as Math class with a rich set of static methods that makes math-oriented programming easy and efficient. It also contains two static members, E and PI, representing the values of mathematical constants e and pi. Table 5.11 lists some of the mathematical methods contained in the Math class.

## Table 5.11 Main mathematical methods

| Method | Description |
|---|---|
| Sin () | sine of an angle in radians |
| Cos () | cosine of an angle in radians |
| Tan () | tangent of an angle in radians |
| Asin () | inverse of sine |
| Acos () | inverse of cosine |
| Atan () | inverse of tangent |
| Atan2 () | inverse tangent, with x and y co-ordinates specified |
| Sinh () | hyperbolic sine |
| Cosh () | hyperbolic cosine |
| Tanh () | hyperbolic tangent |
| Sqrt () | square root |
| Pow () | number raised to a given power |
| Exp () | exponential |
| Log () | natural logarithm (base e) |
| Log10 () | base 10 logarithm |
| Abs () | absolute value of a number |
| Min () | lower of two numbers |
| Max () | higher of two numbers |
| Sign () | sign of the number |

Note that all the methods take double type parameters and return a double type value. However, the parameters of Abs (), Min (), Max (), and Sign () may of any numeric type.

Program 5.8 demonstrates the use of Math class with a simple application.

## Program 5.8 USE OF MATH CLASS METHODS

```
using System;
class MathTest
{
    public static void Main ()
    {
        Console.WriteLine("sines of angles from 0 to 90 degrees");
        for ( double theta = 0.0; theta <= 90.00; theta += 15)
        {
            double x = Math.Sin (theta * Math.PI/180);
            Console.Write ("Sin" + theta);
            Console.WriteLine(" ={0:F4}", x);
        }
    }
}
```

Program 5.8 will produce the following output.

Sines of angles from 0 to 90 degrees
Sin0 = 0.0000
Sin15 = 0.2588
Sin30 = 0.5000
Sin45 = 0.7071
Sin60 = 0.8660
Sin75 = 0.9659
Sin90 = 1.0000

{0:F4} is an output format that prints output with four decimal places. Output formats are discussed in Chapter 17.

Since the data members and methods of Math class are static type, they are accessed using the class name itself instead of its objects. Note that we need to convert degrees to radians by multiplying by (π/180) since all trigonometric functions take radians as parameters.

At present, there is no support for complex numbers and vectors. However, we can build these types using the concept of operator overloading. See Chapter 15 for details on operator overloading.

## Case Study

## Problem Statement

Martin is working as a junior programmer in HighFi Software Solutions which is a software development company involved in developing applications in C, Java and C# programming languages. The Project Manager of Martin has asked him to create an application for converting a number into its equivalent binary format. Martin has to develop the application for an overseas client, TechSoft Solutions. How should Martin create the application?

## Solution

To satisfy the overseas client, Martin should use an object oriented language such as C# to create the application for converting a number into a binary format. C# provides bitwise operators that can be easily used in a C# application to perform manipulation on binary data. After much research, Martin develops the following application in C# for automating the task of converting a number into binary format.

```
using System;
class Convert
{
    public int nobits;
    public Convert(int n)
    {
        nobits = n;
    }
    public void ConvertToBinary(int num)
    {
        int mask = 1;
        mask <<= nobits-1;
        int spaceVal = 0;
        for(; mask != 0; mask >>= 1)
        {
            if((num & mask) != 0)
                Console.Write("1");
            else
                Console.Write("0");
            spaceVal++;
            if((spaceVal % 8) == 0)
            {
                Console.Write(" ");
                spaceVal = 0;
            }
        }
        Console.WriteLine();
    }
}
public class BitWiseDemo
{
    public static void Main()
    {
        Console.WriteLine("Enter a Number for Conversion to Binary Form: ");
        int num=int.Parse(Console.ReadLine());
        Convert con = new Convert(8);
        Console.WriteLine("The Number in Binary Form is: ");
        con.ConvertToBinary(num);
    }
}
```

The bitwise operators can be easily used in a C# application to shift the bits from left to right and vice versa. Manually performing the task of bit manipulation is time-consuming and error-prone.

## Common Programming Errors

-   Forgetting to declare a variable used in an expression.
-   Mixing data types in expressions without clear understanding of their effect on the result.
-   Using a variable in an expression before a value has been assigned.
-   Attempting to store one data type in a variable declared for different type.
-   Using expressions that may result in round-off errors.
-   Using expressions that may result in overflow errors.
-   Applying integer division accidently.
-   Applying implicit conversions incorrectly.
-   Unbalanced parentheses.
-   Improper use of parentheses.
-   Not using parentheses, where necessary.
-   Improper understanding of operators precedence.
-   Lack of understanding of associativity of operators.
-   Improper construction of logical or a compound relational expression.
-   Improper use of increment or decrement operators in expressions.

## Review Questions

5.1 State whether the following statements are true or false.

-   (a) The sign of the result of the module division is always positive.
-   (b) The modulus operator % can be applied to both the integer type and floating point type data.
-   (c) When one of the operand is real and the other is integer is an expression, the integer type is converted to real, before the expression is evaluated.
-   (d) All the bitwise operators have the same level of precedence in C#.
-   (e) If a = 10 and b = 15, then the statement x = (a>b)?a:b assigns the value 15 to x.
-   (f) In evaluating a logical expression of type (boolean_expression1 && boolean_expression2) both the boolean expressions are not always evaluated.
-   (g) In evaluating the expression (x == y && a<b), the boolean expression x == y is evaluated first and then a<b is evaluated.
-   (h) The behaviour of expressions m++ and ++m are identical always.
-   (i) All arithmetic operators enjoy the same level of predence.
-   (j) Casting operations never result in loss of data.

5.2 Arrange the given operators in the order of precedence as defined in C#:

-   !=
-   &&
-   ?:
-   ++
-   &&

5.3 What are the special operators available in C#?

5.4 Which of the following arithmetic expressions are valid? If valid, give the value of the expression; otherwise give reason.

-   (a) 25/3 % 2
-   (b) +9/4 + 5
-   (c) 7.5%3
-   (d) 14%3 + 7%2
-   (e) -14%3
-   (f) 15.25+-5.0
-   (g) (5/3)*3+5%3
-   (h) 21%(int)4.5
