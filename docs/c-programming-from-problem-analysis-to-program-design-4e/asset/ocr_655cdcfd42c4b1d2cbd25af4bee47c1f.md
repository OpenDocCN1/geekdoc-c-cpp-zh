+   22. Write methods to do the following:
+   
+       a. Display three full lines of asterisks on the screen.
+       b. Accept as an argument your age, and display that value along with an appropriate label.
+       c. Accept two floating-point values as arguments. Display the values formatted with three digits to the right of the decimal.
+       d. Accept three `int` arguments and return their sum.
+       e. Accept no arguments and return no values. Initialize a local Boolean variable to `true`. Have the method print the Boolean’s value.

+   23. What will be produced from the following predefined `Math` class method calls?
+   
+       a. `Console.WriteLine(Math.Abs(-98887.234));`
+       b. `Console.WriteLine(Math.Pow(4,3));`
+       c. `Console.WriteLine(Math.Sign(-56));`
+       d. `Console.WriteLine(Math.Sqrt(81));`
+       e. `Console.WriteLine(Math.Min(-56, 56));`

+   24. The following program has several syntax errors as well as style inconsistencies. Correct the syntax errors and identify the style violations.

```
~~~csharp
/* ********************************************
 * AgeIncrementer.cs                       Author: Doyle
 * Prompts the users for their ages in
 * a class method. Prints the value
 * entered back in the Main() method.
 */

using System;

namespace AgeExample
{
    public class AgeIncrementer
    {
        public static void Main()
        {
            int AGE;
            string aValue;

            age = GETAge(aValue);
            Console.WriteLine("Your age next year will be {0}",
                              ++age);
            Console.Read();
        }
        public static GETAge()
        {
            Console.Write("Enter your age: ");
            aValue = Console.ReadLine();
        }
    }
}
~~~
```