
### EXAMPLE 5.11

```csharp
public static bool TryParse(string someStringValue, out int result)
```

When the TryParse() method is executed, result holds the integer value equivalent to the data stored in the string argument, someStringValue, or result stores a zero. If the string variable’s data is in the correct format and range, the conversion succeeds. Zero is only stored in result when the conversion fails. The conversion fails if the someStringValue parameter is null or has no value, is not of the correct format, or represents a number less than MinValue or greater than MaxValue of the integer.

> **NOTE**
>
> Each of the built-in data types has a TryParse() method. char.TryParse() converts the value of the specified string to its Unicode character equivalent; bool.TryParse() converts the specified string representation of a logical value to its Boolean equivalent. There are also TryParse() methods for decimal, double, and float. With each of these, in addition to doing the conversion, a Boolean value is returned indicating whether the conversion was successful or not.

As you review Example 5–11, notice that the parameter result has an out modifier listed before the data type. `out` parameters are output-only parameters, meaning there is no value in result when the method is invoked. The parameter is considered initially unassigned. After the TryParse() method is executed, the out parameter result will hold either the converted value or zero.

When you input data, instead of just assuming the user will always enter valid characters, an if statement could be written to test the Boolean value returned from TryParse() as illustrated in Example 5–12.

### EXAMPLE 5.12

```csharp
if (int.TryParse(inValue, out v1) == false)
    Console.WriteLine("Did not put a valid integer - " +
                      "0 stored in v1");
```

> **NOTE**
>
> Recall that when you use the special out and ref modifiers as part of the parameter, they must appear as part of the heading for the method and also in the call to the method.

The statement in Example 5–12 attempts to convert the string value stored in inValue into an integer, storing the result of the conversion in the variable v1. If it is successful, the value is stored in v1 and TryParse() returns true. If there is a problem with the data, 0 is stored in v1 and TryParse() returns false.

Consider Example 5-13, which uses a two-way if statement in a class method. The user is prompted to enter two values. A two-way if statement is used to determine which is the largest. That value and its square root are displayed.

### EXAMPLE 5.13

```csharp
/* LargestValue.cs                Author: Doyle
 * Allows the user to input two values.
 * Determine the largest of the two values.
 * Prints the largest and its square root.
 **********************************************/

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace LargestValue
{
    class LargestValue
    {
        static void Main( )
        {
            int value1,
                value2,
                largestOne;

            InputValues(out value1, out value2);
            largestOne = DetermineLargest(value1, value2);
            PrintResults(largestOne);
            Console.ReadKey( );
        }

        public static void InputValues(out int v1, out int v2)
        {
            string inValue;

            Console.Write("Enter the first value: ");
            inValue = Console.ReadLine();
            if (int.TryParse(inValue, out v1) == false)
                Console.WriteLine("Did not input a " +
                    "valid integer - 0 stored in v1");
            Console.Write("Enter the second value: ");
            inValue = Console.ReadLine();
            if (int.TryParse(inValue, out v2) == false)
                Console.WriteLine("Did not input a " +
                    "valid integer - 0 stored in v2");
        }

        public static int DetermineLargest(int value1, int value2)
        {
            int largestOne;        //Local variable declared to
                                   //facilitate single exit from method
            if (value1 > value2)
            {
                largestOne = value1;
            }
            else
            {
                largestOne = value2;
            }
            return largestOne;
        }

        public static void PrintResults(int largestOne)
        {
            Console.WriteLine( );
            Console.WriteLine("The largest value entered was "
                              + largestOne);
            Console.WriteLine("Its square root is {0:f2}",
                              Math.Sqrt(largestOne));
            Console.ReadLine( );
        }
    }
}
```

When you are writing selection statements, try to avoid repeating code. Instead of duplicating statements for both the true and false statements, pull out common statements and place them before or after the selection statement. You might have been tempted to solve the problem presented for Example 5-13 with the following two-way if statement:

```csharp
if (value1 > value2)
{
    Console.WriteLine("The largest value entered was "
                      + value1);
    Console.WriteLine("Its square root is {0:f2}",
                      Math.Sqrt(value1));
}
else
{
    Console.WriteLine("The largest value entered was "
                      + value2);
    Console.WriteLine("Its square root is {0:f2}",
                      Math.Sqrt(value2));
}
```

The calls to the Console.WriteLine() method for displaying the largest value and its square root are included only once in Example 5-13. They appear twice in the last segment.

Another solution that is not modularized, but eliminates the repeating code, is as follows:

```csharp
int largest;
if (value1 > value2)
{
    largest = value1;
}
else
{
    largest = value2;
}
Console.WriteLine("The largest value entered was "
    + largest);
Console.WriteLine("Its square root is {0:f2}",
    Math.Sqrt(largest));
```

All three ways of writing the selection statement produce the same output. The modularized version in Example 5-13 is the preferred approach of the three. In this situation, you may not see a clear advantage of one approach over the other. Modularization becomes more important as the complexity of a computer program increases. Figure 5-6 shows the output produced when the program is run with 25 entered for the first value and 15 entered for the second value.

![](img/36e48639a06772bcb0fa1ea2525b33a3_311_0.png)

### FIGURE 5-6 Output from LargestValue problem

What does the program in Example 5-13 print when the values entered are the same?

Because value1 is not greater than value2, the else statement is executed and value2 is stored in largestOne. If you want to display a message indicating their values are the same, you need to add one more conditional expression as part of the if statement. This additional test would be to determine whether value2 is greater than value1. The expression would be added as the else statement. Adding this second test would enable you to include a second else statement. The last else would not be entered unless both of the conditional expressions evaluated to false—and in this case, the values are the same. If you make this revision, the logic would need to be revised for displaying the largest value. One approach would be to return the negative value of value1 or value2, when they have the same values. It does not matter which one gets returned because their values are the same. The PrintResults() method could test the largestOne variable. When it is negative, a message could be printed indicating the values are the same. The additional test is as follows:

```csharp
if (value1 > value2)
{
    largestOne = value1;
}
else
    if (value1 < value2)
    {
        largestOne = value2;
    }
    else
        largestOne = -(value1);
```

Sometimes, a single variable might need to be tested for multiple values. A nested if...else statement, like that described previously, can be used for this. You might also want to test a different variable inside the true (or false) statements. A nested if...else statement is also used for this. You will learn more about nested if...else statements in the following section.

## Nested if...else Statement

Any statement can be included with the statements to be executed when the expression evaluates to true. The same holds for the false statements. Therefore, it is acceptable to write an if within an if. Many different expressions can be evaluated in a single if statement. When you place an if within an if, you create a nested if...else statement, also referred to as a nested if statement.

With a nested if statement, multiple expressions can be tested. As long as the expressions evaluate to true, the true statements continue to be evaluated. When another if statement is one of the statements in the block being executed, another evaluation is performed. This continues as long as additional if statements are part of the true statements.

As with the two-way, only one segment of code is executed. You never execute the true and its associated false statements. When the block is completed, all remaining conditional expressions and their statements are skipped or bypassed. After completing the execution of that block, control always transfers to the statement immediately following the if block. The syntax for a nested if...else statement, which follows that of the two-way is repeated here. The difference is that with a nested if...else, the statement might be another if statement:
