
## 88 Branching Out with if and switch

```csharp
Console.WriteLine("Total = " + total +);\n// Wait for user to acknowledge the results.
Console.WriteLine("Press Enter to terminate . . .");
Console.Read();
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_113_0.png)

The CalculateInterest program begins by prompting the user for his name using WriteLine() to write a string to the console. Tell the user exactly what you want and, if possible, specify the format. Users don't respond well with uninformative prompts, such as >.

The sample program uses the ReadLine() command to read when the user types; the program returns the value, in the form of a string, when the user presses Enter. Because the program is looking for the principal in the form of a decimal, the input string must be converted using the Convert.ToDecimal() command. The result is stored in principalInput.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_113_1.png)

The ReadLine(), WriteLine(), and ToDecimal() commands are examples of method calls. A method call delegates work to another part of the program, called a method. I describe method calls in detail in Book II; these particular method calls are straightforward. You should be able to get the gist of meaning using my extraordinarily insightful explanation. If that's work, ignore the narrative. If it doesn't work, see Book II.

The next line in the example checks principal. If it is negative, the program outputs a polite "nastygram" indicating that the user has fouled up. The program does the same for the interest rate, and then it simplifies the interest calculation outlined earlier, in the "Introducing the If Statement," and spits out using a series of WriteLine() commands.

The program generates the following output with a legitimate principal and an unusual interest rate that is perfectly legal in most cases:

```
Enter principal: 1234
Enter interest: 21%

Principal = 1234
Interest      = 21%

Interest paid = 259.14
Total         = 1493.14
Enter Enter to terminate . . .
```

Executing the program with illegal input generates the following output:

```
Enter principal: 1234
Enter interest: -12.5
Interest cannot be negative

Principal = 1234
Interest      = 0%
```

## Branching Out with if and switch

Interest paid = 0
Total = 1234
Press Enter to terminate ..

Book I
Chapter 5

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_114_0.png)

Getting into the
Program Flow

Indent the lines within an if clause to enhance readability. This type of indentation is ignored by C# but is helpful to us humans. Most programming editors support autointing, whereby the editor automatically inserts as soon as you enter the if command. To set autointing in Visual Studio, choose Tools+Options. Expand the Editor node. From there, expand C#. Finally, click Tabs. On this page, enable Smart Indenting and set the number of spaces per indent to your preference. (I use two spaces per indent in this book.) Set the tab size to the same value.

## Examining the else statement

Sometimes, your code must check for mutually exclusive conditions. For example, the following code segment stores the maximum of two numbers, a and b, in the variable max:

```csharp
// Store the maximum of a and b into the variable max.
int max;
// If a is greater than b . . .
if (a > b)
{
    // . . save a as the maximum.
    max = a;
}
// If a is less than or equal to b . . .
if (a <= b)
{
    // . . save b as the maximum.
    max = b;
}
```

The second if statement causes needless processing because the two conditions are mutually exclusive. If a is greater than b, a can't possibly be less than equal to b. C# defines an else clause for just this case. The else keyword defines a block of code that's executed if the if block is not.

The code segment to calculate the maximum now appears this way:

```csharp
// Store the maximum of a and b into the variable max.
int max;
// If a is greater than b . . .
if (a > b)
{
    // . . save a as the maximum; otherwise . . .
    max = a;
}
else
{
    // . . save b as the maximum.
    max = b;
}
```

## 90 Branching Out with if and switch

If a is greater than b, the first block is executed; otherwise, the second block is executed. In the end, max contains the greater of a or b.

## Avoiding even the else

Sequences of else causes can also be confusing. Some programmers to avoid them when doing so doesn't even cause more confusion. You could write the maximum calculation like this:

```csharp
// Store the maximum of a and b into the variable max.
int max;
// Start by assuming that a is greater than b.
max = a;
// If it is not ...
if (b > a)
{
    // then you can change your mind.
    max = b;
}
```

Some programmers avoid this style like the plague, and I can sympathize. (That doesn't mean I'm going to change; it just means I sympathize.) You see both style and the "else style" in common use.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_115_0.png)

Programmers who like to be and cryptic often use the ternary operator, ?: equivalent to an if/else on one line:

```csharp
bool informal = true;
string name = informal ? "Chuck" : "Charles"; // Returns "Chuck"
```

This chunk evaluates the expression before the colon: If the expression is true, it returns the colon before the question mark. If the expression is false, it returns it after the question mark. This process turns an if/else into an expression.

I general advise using ternary only rarely because it is cryptic.

## Nesting if statements

The CalculateInterest program warns the user of illegal input; however, continuing with the interest calculation, even if one of the values is illogical, doesn't seem right. It causes no harm here because the interest calculation takes little or no time and the user can ignore the results, but some calculations are nearly as quick. In addition, why ask the user for an interest rate after she has already entered an invalid value for the principal? The user knows that the results of the calculation will be invalid no matter what she enters. (You'd be amazed at how much it infuriates users.)

The program should ask the user for an interest rate only if the principal is reasonable and perform the interest calculation only if both values are valid. To accomplish this, you need two if statements, one within the other.

## Branching Out with if and switch 91

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_116_0.png)

An if statement found within the body of another statement is embed-ded, or nested, statement.

The following program, CalculateInterestWithTest, uses embedded if statements to avoid stupid questions if a problem is detected:

```csharp
// CalculateInterestWithTest -- Calculate the interest amount
// paid on a given principal. If either the principal or the
// interest rate is negative, then generate an error message
// and don't proceed with the calculation.
using System;
namespace CalculateInterestWithTest
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // Define a maximum interest rate.
            int maximumInterest = 0;
            // Prompt user to enter source principal.
            Console.Write("Enter principal: ");
            string principalInput = Console.ReadLine();
            decimal principal = Convert.ToDecimal(principalInput);
// If the principal is negative -
            if (principal < 0)
            {
                // generate an error message
                Console.WriteLine("Principal cannot be negative!");
            }
            else
            {
                // otherwise, enter the interest rate.
                Console.Write("Enter interest: ");
                string interestInput = Console.ReadLine();
                decimal interest = Convert.ToDecimal(interestInput);
// If the interest is negative or too large -
                if (interest < 0 || interest > maximumInterest)
                {
                    // generate an error message as well.
                    Console.WriteLine("Interest cannot be negative or greater than " + maximumInterest);
                    interest = 0;
                }
                else
                {
                    // Both the principal and the interest appear to be legal;
                    // calculate the value of the principal plus interest.
                    decimal interestPaid = principal * (interest / 100);
                    // Now calculate the total.
                    decimal total = principal + interestPaid;
                    // Output the result.
                    Console.WriteLine();
                    Console.WriteLine("Principal = " + principal + "*");
                    Console.WriteLine("Interest = " + interest + " **%");
                    Console.WriteLine();
                    Console.WriteLine("Interest paid = " + interestPaid);
                    Console.WriteLine("Total = " + total);
                }
            }
        }
    }
}
```
