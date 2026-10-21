
```csharp
Console.WriteLine("London");
Console.WriteLine("Bombay");
Console.WriteLine("Paris");
Console.WriteLine("Type your choice");
String name = Console.ReadLine();

switch (name)
{
    case "Bombay":
        Console.WriteLine("Bombay:Guide 5");
        break;
    case "London":
        Console.WriteLine("London:Guide 10");
        break;
    case "Paris":
        Console.WriteLine("Paris:Guide 15");
        break;
    default:
        Console.WriteLine("Invalid choice");
        break;
}
}
```

Output of Program 6.6:

```
Select your choice
London
Bombay
Paris
Type your choice
London
London : Guide 10
```

### 6.7.1 Fallthrough in Switch Statement

In the absence of the break statement in a case block, if the control moves to the next case block without any problem, it is known as ‘fallthrough’. Fallthrough is permitted in C, C++ and Java. But C# does not permit automatic fallthrough, if the case block contains executable code. However, it is allowed if the case block is empty as discussed earlier. For instance,

```csharp
switch (m)
{
    case 1:
        x = y;
    case 2:
        x = y + m;
    default:
        x = y - m;
}
```

is an error in C#. If we want two consecutive case blocks to be executed continuously, we have to force the process by using the goto statement. For example:

```csharp
switch (m)
{
    case 1:
        x = y;
        goto case 2;
    case 2:
        x = y + m;
        goto default;
    default:
        x = y - m;
        break;
}
```

The goto mechanism enables us to jump backward and forward between cases and therefore arrange labels arbitrarily. Example:

```csharp
switch (m)
{
    default:
        x = y - m;
        break;
    case 2:
        x = y + m;
        goto default;
    case 1:
        x = y;
        goto case 2;
}
```

is perfectly valid.

Program 6.7 uses switch case to allow users to select the size of a cola can. Based on the user selection, the program prints the amount the user must pay for the particular type of can selected.

### Program 6.7 | ANOTHER SWITCH EXAMPLE

```csharp
using System;
class SwitchExample
{
    public static void Main()
    {
        Console.WriteLine("Select your Cola Can:");
        Console.WriteLine("S=SMALL M=MEDIUM L=LARGE");
        Console.Write("Please enter your option: ");
        String s = Console.ReadLine();
        int cost = 0;
        switch (s)
        {
            case "S":
                cost += 10;
                break;
            case "M":
                cost += 15;
                goto case "S";
            case "L":
                cost += 30;
                goto case "S";
            default:
                Console.WriteLine("Invalid option. Please select either S, M, or L.");
                break;
        }
        if (cost != 0)
            Console.WriteLine("Please pay {0} Rupees.", cost);
    }
}
```

![](img/bae4ee2c7c29c052feb3b9a9c5659998_112_0.png)

## 6.8 THE ?: OPERATOR

C# has an unusual operator, used for making two-way decisions; it is a combination of ? and : and takes three operands. This operator is popularly known as the conditional operator. The general form of use of the conditional operator is as follows:

```
conditional expression ? expression1 : expression2
```

The conditional expression is evaluated first. If the result is true, expression1 is evaluated and is returned as the value of the conditional expression. Otherwise, expression2 is evaluated and its value is returned. For example, the segment

```csharp
if (x < 0)
    flag = 0;
else
    flag = 1;
```

can be written as

```csharp
flag = (x < 0) ? 0 : 1;
```

Consider the evaluation of the following function:

```
y = 1.5x + 3      for x <= 2
y = 2x + 5        for x > 2
```

This can be evaluated using the conditional operator as follows:

```csharp
y = (x > 2) ? (2*x + 5) : (1.5*x + 3);
```

The conditional operator may be nested for evaluating more complex assignment decisions. For example, consider the weekly salary of a salesgirl who is selling some domestic products. If x is the number of products sold in a week, her weekly salary is given by

```
salary = { 4x + 100 for x < 40
          300 for x = 40
          4.5x + 150 for x > 40 }
```

This complex equation can be written as

```csharp
salary = (x != 40) ? ((x < 40) ? (4*x + 100) : (4.5*x + 150)) : 300; // nesting
```

The same can be evaluated using if...else statements as follows:

```csharp
if (x <= 40)
    if (x < 40)
        salary = 4*x + 100;
    else
        salary = 300;
else
    salary = 4.5*x + 150;
```

When the conditional operator is used, the code becomes more concise and perhaps, more efficient. However, the readability is poor. It is better to use if statements when more than a single nesting of the conditional operator is required.

## Case Study

### Problem Statement

SafeMoney Bank provides loans to individuals at simple and compound interest for a period ranging from 1 to 15 years. Till recently, the staff of the SafeMoney Bank has been manually calculating simple and compound interest for loans provided to individuals by the bank. It has been found by the manager of SafeMoney Bank that for the past two months, a lot of errors have been occurring during the calculation of simple and compound interest by the staff of the Bank. In addition, there has been a lot of delay in approving of loans. As a result, the bank is losing valuable customers. How can the manager of SafeMoney Bank solve this problem?

### Solution

The task of calculating simple and compound interest must be automated in order to decrease the errors in the calculations. The manager of SafeMoney Bank asks Binoy who is a senior programmer in the IT department of SafeMoney Bank to create an application for automating the task of calculating simple and compound interest so that it can be performed efficiently by the bank staff. After a requirement analysis, Binoy decides that decision-making statements such as If Else supported by C# must be used in the application for calculating simple and compound interest. Binoy creates the following C# application.

```csharp
using System;

class InterestCalculator
{
    public static void Main()
    {
        Console.WriteLine("==Interest Calculator==");
        Console.WriteLine("Calculate Simple (S) / Compound (C) Interest: ");
        string choice = Console.ReadLine();

        Console.WriteLine("Enter Principal Amount: ");
        double p = double.Parse(Console.ReadLine());
        Console.WriteLine("Enter Rate of Interest: ");
        double r = double.Parse(Console.ReadLine());
        Console.WriteLine("Enter Duration: ");
        int t = Int32.Parse(Console.ReadLine());

        if (choice == "S")
        {
            double simpleInterest = (double)((p * r * t) / 100);
            Console.WriteLine("The Simple Interest is: {0,0:Rs ###.##}", simpleInterest);
        }
        else
        {
            double compoundInterest = (double)p * (Math.Pow(((r / 100) + 1), t));
            Console.WriteLine("The Compound Interest is: {0,0:Rs ###.##}", compoundInterest);
        }
    }
}
```

### Remarks

The If Else statement in C# can be used to evaluate a condition and on the basis of the result of the evaluation, the control flow of the program must be decided. If the condition given with the If statement evaluates to true then a specific set of program statements must be executed. However if the condition evaluates to false then another set of program statements must be executed.

## Common Programming Errors

- Using `=` in place of `==` sign.
- Dangling else in nested `if` statements.
- Forgetting to initialize variables in some paths of a multiple branch construct.
- Improper and confused use of `&&` and `||` conditional operators.
- Not applying the operator precedence properly.
- Using multiple relational operators like `(a <= x <= b)`.
- Comparing floating point expressions in `if` statements like `if (x == y)`.
- Forgetting to use colon for case labels in `switch` statement.
- Not using `goto` for fallthrough cases in `switch` statement.
- Using operators `<=`, `>=`, and `!=` as `<=`, `>=`, and `=!`.
- Providing spaces between the symbols of operators `==`, `<=`, `>=`, and `!=`.
- Not using braces when the `if` statement blocks contain multiple statements.
- Using integer values in the test expression of an `if` statement, like `if (x).....`.
- Placing semicolon immediately after the right parenthesis after the condition in an `if` statement.
- Improper nesting of `if...else` statements.
