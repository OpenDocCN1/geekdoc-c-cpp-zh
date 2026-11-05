
The final application listing for both files is as follows:

```csharp
/* Ticket.cs        Author:    Doyle
 * Describes the characteristics of a
 * speeding ticket to include the speed
 * limit, ticketed speed, and fine amount.
 * The Ticket class is used to set the
 * amount for the fine.
 * ****************************************/
using System;

namespace TicketSpace
{
    public class Ticket
    {
        private const decimal COST_PER_5_OVER = 87.50M;
        private int speedLimit;
        private int speed;
        private decimal fine;

        public Ticket()
        {
        }

        public Ticket(int speedLmt, int reportedSpeed)
        {
            speedLimit = speedLmt;
            speed = reportedSpeed - speedLimit;
        }

        public decimal Fine
        {
            get
            {
                return fine;
            }
        }

        public void SetFine(char classif)
        {
            fine = (speed / 5 * COST_PER_5_OVER) + 75.00M;
            if (classif == '4')
                if (speed > 20)
                    fine += 200;
                else
                    fine += 50;
            else
                if (classif == '1')
                    if (speed < 21)
                        fine -= 50;
                    else
                        fine += 100;
                else
                    if (speed > 20)
                        fine += 100;
        }
    }
}
```

```csharp
/* TicketApp.cs        Author:      Doyle
 * Instantiates a Ticket object
 * from the inputted values of
 * speed and speed limit. Uses
 * the year in school classification
 * to set the fine amount.
 * ***********************************/
using System;

namespace TicketSpace
{
    public class TicketApp
    {
        static void Main()
        {
            int speedLimit,
                speed;
            char classif;

            speedLimit = InputSpeed("Speed Limit", out speedLimit);
            speed = InputSpeed("Ticketed Speed", out speed);
            classif = InputYearInSchool();

            Ticket myTicket = new Ticket(speedLimit, speed);

            myTicket.SetFine(classif);
            Console.WriteLine("Fine: {0:C}", myTicket.Fine);
            Console.ReadLine();
        }

        public static int InputSpeed(string whichSpeed, out int s)
        {
            string inValue;
            Console.Write("Enter the {0}: ", whichSpeed);
            inValue = Console.ReadLine();
            s = Convert.ToInt32(inValue);
            return s;
        }

        public static char InputYearInSchool()
        {
            string inValue;
            char yrInSchool;

            Console.WriteLine("Enter your classification: ");
            Console.WriteLine("\tFreshmen (enter 1)");
            Console.WriteLine("\tSophomore (enter 2)");
            Console.WriteLine("\tJunior (enter 3)");
            Console.Write("\tSenior (enter 4)");
            Console.WriteLine();
            inValue = Console.ReadLine();
            yrInSchool = Convert.ToChar(inValue);
            return yrInSchool;
        }
    }
}
```

Figure 5-13 shows the output produced for a ticket issued to a junior traveling at a speed of 45 MPH in a 35 MPH zone.

![](img/e33ae760e23d89eac66541252ad65de8_312_0.png)

Figure 5-13 Output from the SpeedingTicket example

As indicated in Table 5-10, a number of different test cases should be run to verify the correctness of your solution. Just because you are getting output does not mean your solution is correct. Compare your results with the desk checked calculated results. Are they the same? Have you considered all possible combinations?

## CODING STANDARDS

It is important to follow coding standards when you design solutions involving selection statements. Developing standards that you consistently adhere to will increase your coding efficiency and make your code more maintainable. One of the most important considerations with selection statements relates to readability. The best practices are described next as they relate to the consistent placement of curly braces and the proper use of white space.

### Guidelines for Placement of Curly Braces

Curly braces are required when the body following an if or else statement has more than one statement. Many developers use curly braces with all selection statements—even single if/else statements. In this book, curly braces are added when there are two or more executable statements. For single statements, curly braces were omitted. Whether you use curly braces with all cases or just for multistatement executables, be consistent with your usage.

Open braces should always be at the beginning of the line after the statement that begins the block.

The contents of the brace should be indented by four spaces. For example:

```csharp
if (someExpression)
{
    ExecuteMethod1();
    ExecuteMethod2();
}
else
{
    ExecuteMethod3();
    ExecuteMethod4();
}
```

### Guidelines for Placement of else with Nested if Statements

Many developers place an else...if on the same line when a nested if is written. In this book, the else is placed on a line by itself. The if statement appears on the line below as shown in the following example:

```csharp
if (someExpression)
    DoSomething();
else
    if
    {
        DoSomethingElse();
    }
```

### Guidelines for Use of White Space with a Switch Statement

Place curly braces on separate lines with a switch statement. Indent the case statements. Do not place curly braces around multiline executables as shown in the following example:

```csharp
switch (someExpression)
{

    case 0:
        DoSomething();
        break;
    case 1:
        DoSomethingElse();
        break;
    default:
        break;

}
```

### Spacing Conventions

Use a single space before and after comparison operators as shown next: `if (x == y)`

Do not place an extra space before or after the expression as shown in the next example:

`if (x == y)` // Incorrect – Extraneous spaces before the x and after the y

Use tabs instead of spaces for indentation.

Use white space (one blank line) to separate and organize logical groups of code within the block.

### Advanced Selection Statement Suggestions

Readability and maintainability are improved when you avoid writing compound selection statements. Instead of writing `<=` or `>=`, add or subtract 1 from the endpoint (i.e., `if (a >= 100)` is the same as `if (a > 99)`). Additional thought will normally help you to eliminate this type of compound statement.

Write a nested `if` as opposed to combining two expressions with `&&`. This enables you to provide an `else` to each separately. For example, replace `if ((a > b) && (b > c))` with

```csharp
if (a > b)
    if (b > c)
```

When possible use short-circuit evaluation to improve efficiency.

Switch statements should include a `default` label as the last `case` label.

Do not make explicit comparisons to `true` or `false` in a conditional expression.

Do not use the equality operators with floating-point values. Most floating-point values have no exact binary representation and have a limited precision.

Avoid using complex or compound ternary operations. Use the ternary conditional operator only for trivial conditions.

## RESOURCES

Additional sites you might want to explore:

- C# Coding Style Guide—TechNotes, HowTo Series
  http://www.isharpc.../TechNotes/SharpDevelopCodingStyle03.pdf
- Microsoft C# if statement Tutorial
  http://csharp.net-tutorials.com/basics/if-statement/
- if-else (C# Reference)
  http://msdn.microsoft.com/en-us/library/5011f09h.aspx
- switch (C# Reference)
  http://msdn.microsoft.com/en-us/library/06tc147t(vs.80).aspx

## QUICK REVIEW

- 1. The three basic programming constructs include simple sequence, selection, and iteration.
- 2. The selection statement allows you to deviate from the sequential path and perform different statements based on the value of one or more variables.
- 3. The two types of selection statements are the if...else and switch statements. C# also provides the ternary operator ? : for conditional expressions.
- 4. With selection statements, properly used indentation is for readability only. Curly braces are used when you have more than one expression to be evaluated.
- 5. The result of expressions used with selection statements is either true or false.
- 6. Testing a Boolean variable does not require the use of an equality operator. If salariedEmployee is of type bool, you can write if (salariedEmployee). It is not necessary to include the == operator.
- 7. When you compare characters or strings, the Unicode character set is used.
- 8. You can compare string operands using the equality operators == and !=. The relational symbols >, <, >=, or <= are not defined for strings.
- 9. Conditional expressions can be combined with logical conditional operators, && or ||, to form more complex expressions.
- 10. C# uses the && and || operators to represent AND and OR, respectively.
