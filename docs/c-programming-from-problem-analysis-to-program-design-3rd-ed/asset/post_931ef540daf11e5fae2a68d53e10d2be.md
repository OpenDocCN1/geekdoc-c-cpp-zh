
The same result could have been achieved using

```csharp
while (startValue <= endValue)
```

Both cases call attention to the fact that the value entered by the user as the last number should be added to the total. If the conditional expression read `while(startValue < endValue)`, the loop would not be executed for the last value. An off-by-one error would have occurred. This is a common problem associated with counter-controlled loops. It is important to think through test cases and check endpoints to ensure they have been taken into consideration. You should always check the initial and final values of the loop control variable and verify that you get the expected results at the boundaries. Without adding one onto the endpoint or using the compound relational operator, the result would be incorrect.

Why did the solution print the range of values (`startValue` and `endValue`) before the loop executed? The following statement appeared before the loop:

```csharp
Console.Write("Sum of values {0} through {1} ",
    startValue, endValue);
```

The loop control variable, `startValue`, is changed inside the loop. Its original value is lost and no longer available when the loop is finished. Thus, to display the beginning value, you would need either to store it in a different memory location (that does not change) or to print it before the loop body.

If you are going to print the boundaries before the loop, why not go ahead and place the following statement before the loop in Example 6-2:

```csharp
Console.WriteLine("is {0}", sum);
```

Zero would be printed for sum if you print it before the loop. The variable sum gets the accumulated value from the loop body; thus, it does not make sense to print the value until after the calculations are performed and the loop is completed.

Figure 6-2 shows the results of an execution of Example 6-2 when 14 and 33 are entered as the range of values.

![](img/e33ae760e23d89eac66541252ad65de8_334_0.png)

Figure 6-2 Example of output from user-entered loop boundaries

With Example 6-2, what happens when the user enters a larger value for the `startValue` than the value entered for `endValue`? If you answered the loop body will not get executed, even one time, you are correct. Because the conditional expression evaluates to `false`, the body is skipped and the lines following the loop are executed.

## Sentinel-Controlled Loop

Although you do not always know ahead of time how many times the loop should be performed, this is a requirement for a counter-controlled loop. Another option is a **sentinel-controlled loop**. Sentinel-controlled loops are often used for inputting data when you do not know the exact number of values to be entered. If your program inputs multiple homework scores, for example, you might display a message telling the users to enter a negative value to indicate they are finished entering scores. You would never have a negative score; thus, this would be an appropriate sentinel value.

Sentinel-controlled loops are also referred to as **indefinite loops** because the number of repetitions is not known before the loop’s execution. To design an indefinite loop, select a sentinel value to use in the expression. A **sentinel value** is an extreme value, a dummy value. It is a value that should not be processed—like a negative value when only positive scores are to be processed.

The sentinel value is used as the operand in the conditional expression for an indefinite loop. A sentinel-controlled loop gives you the advantage of not needing to know how many times the loop will be performed. When all the data has been processed, the sentinel value can be entered indicating the loop should terminate normally. Example 6-3 demonstrates how a sentinel-controlled loop can be used to input any number of data values.

### Example 6-3

```csharp
/* InputValuesLoop.cs      Author: Doyle
 * Demonstrates loop for inputting values.
 */
using System;

namespace InputValuesLoop
{
    class InputValuesLoop
    {
        static void Main( )
        {
            string inValue = "";  //Initialized to null

            Console.Write("This program will let you enter");
            Console.Write(" value after value. To Stop, enter");
            Console.WriteLine(" -99");

            while (inValue != "-99")
            {
                Console.WriteLine("Enter value (-99 to exit)");
                inValue = Console.ReadLine();
            }
        }
    }
}
```

As with the counter-controlled loop, it is necessary to set up the conditional expression in Example 6-3. This must be done before the loop executes. This time, the variable used to hold the inputted values, `inValue`, is initialized to `null ("")`; no value is placed between the double quotes. The variable `inValue` could have been initialized to any value, other than `-99`. However, it had to be initialized.

![](img/e33ae760e23d89eac66541252ad65de8_336_0.png)

C# does not allow you to use unassigned values. If you failed to initialize `inValue`, you would have received the error message, “Use of unassigned local variable inValue,” when you attempted to use `inValue` in the conditional expression.

In Example 6-3, the conditional expression continues to evaluate as `true` as long as the user does not enter `-99`. Notice how the input statement is placed as the last statement in the loop body. The placement is important. If calculations were part of the loop body, it would have been necessary to prime the read on the outside of the loop. This means that you would input a value before going into the body of the loop. Doing this allows the first statements in the loop to be the statements processing that entered value. Then, as the last statement in the body of the loop, another `ReadLine()` method is included. If you do not place the `ReadLine()` at the end as the last statement, you end up processing the sentinel value. As soon as the user enters the `-99`, or the sentinel value, you want to stop processing data. Placing the `ReadLine()` as the last line in the body enables the conditional expression to evaluate to `false` as soon as the `-99` is entered. Example 6-4 illustrates this important point by summing the values entered.

### Example 6-4

```csharp
/* PrimeRead.cs                 Author: Doyle
 * Sentinel loop to sum values
 */
using System;

namespace PrimeRead
{
    class PrimeRead
    {
        static void Main( )
        {
            string inValue = "";          //Initialized to null
            int sum = 0,
                intValue;

            Console.Write("This program will let you enter");
            Console.Write(" value after value. To Stop, enter");
            Console.WriteLine(" -99");
            Console.WriteLine("Enter value (-99 to exit)");
            inValue = Console.ReadLine();   // Priming read

            while (inValue != "-99")
            {
                intValue = Convert.ToInt32(inValue);
                sum += intValue;
                Console.WriteLine("Enter value(-99 to exit)");
                inValue = Console.ReadLine( );
            }

            Console.WriteLine("Total values entered {0}", sum);
        }
    }
}
```

Suppose the input is:

- 10
- 12
- 40
- 5
- 1
- -99

The output for this code with the preceding input is:

Total values entered 68

When you implement a sentinel-controlled loop, it is imperative that you tell the user what value to type to end the loop. You should include this information inside the loop body. This is especially true if a large number of values are being entered. You do not want the user to have to guess or try to remember how to terminate the program.

![](img/e33ae760e23d89eac66541252ad65de8_337_0.png)

> To tell users what value to enter to terminate, you display a message using a Write( ) or WriteLine( ) method before the ReadLine( ). Otherwise, how will they know what value to enter to stop?

In Chapter 11, you will learn how to process data batched together and stored on a storage medium, such as your hard drive. Sentinel-controlled loops are useful for loops that process data stored in a file. The sentinel value is placed as the last entry in the file. Here, it is unnecessary to display a message indicating how to stop. The loop conditional expression looks exactly like that used for interactive input of data. The conditional expression matches the selected sentinel value.

## Windows Applications Using Loops

Many C# applications developed in industry today create a Windows application designed with a graphical user interface (GUI). So far, the output you have displayed has been in the form of a console window instead of a Windows form or Web page. Take note that all of the programming concepts you are learning are useful for any type of application; however, as you will learn in later chapters, an event-driven model is used with Windows applications. An **event-driven model** manages the interaction between the user and the GUI by handling the repetition for you. Sending your output to the console made it possible for you to learn the basics of programming before focusing on the interface design.

C# has a predefined class called MessageBox that can be used to display information to users through its Show( ) method member. The output generated by the MessageBox.Show( ) method more closely resembles the windows you are accustomed to seeing and using. In later chapters of this book, all applications are built around windows. The example that follows produces a table showing values 1 through 10 and their squares. The results are displayed in a dialog box window instead of the console to give you the flavor of displaying output to a Windows dialog box.

![](img/e33ae760e23d89eac66541252ad65de8_338_0.png)

When you do not want to see the Command window on console applications, you need to indicate that the Output type should be a Windows Application. Do this by selecting the project in the Solution Explorer window and then selecting that project's Properties option from the Project menu. Select Windows Application as the Output type from the drop-down list. You can also right-click on the project's name in the Solution Explorer window. This window is shown as one of the options. The Alt+Enter shortcut also displays this dialog box when you have the project selected in the Solution Explorer window.

### Example 6-5

```csharp
/* SquaredValues.cs   Author: Doyle
 * Displays values 1 through 10
 * along with their squares.
 */
using System;
using System.Windows.Forms; //Namespace for Windows Forms class
```
