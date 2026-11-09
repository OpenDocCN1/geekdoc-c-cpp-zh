
Phenomenon of the switch statements, which occurs when the default statement gets executed even after executing the case statement that matches the expression. This happens because of the absence of a programming construct in the case statement to break the execution after executing the case statement. To counter the fall through of case statements, the **break** statement is used. In some of the earlier object-oriented programming languages such as C++, the **break** statement is optional. However, C# makes it mandatory to use the **break** statements.

Note that if you have an empty **case** statement, that is, when the case statement has no statements to be executed, you can omit the **break** statement. In the absence of a **break** statement in the case statement, the execution falls through from an empty case statement to the next case statement. In such scenarios, you can execute a single set of statements for multiple empty case statements.

Let’s consider an example given in the following code snippet:

```csharp
Console.Write("Enter a letter: ");
char mychar = System.Convert.ToChar(Console.ReadLine());
char x = char.ToUpper(mychar);
switch (x)
{
    default:
        Console.WriteLine("Not a vowel");
        break;
    case 'A':
    case 'E':
    case 'I':
    case 'O':
    case 'U':
        Console.WriteLine("It is a vowel");
        break;
}
Console.ReadLine();
```

In the preceding code snippet, the expression of the switch statement is the value of the x variable. The value of x is compared with the case labels—A, E, I, O, and U. The case statements with the case labels A, E, I, O, and U are consecutive. Among these case statements, those with the case labels A, E, I, and O are empty. This implies that if x is equal to A, E, I, or O, then the execution falls through to the next case statement until it reaches the case statement with the case label U displaying the message It is a vowel. If x is not equal to A, E, I, O, or U, then the default statement is executed, which displays the message Not a vowel. Note that the default statement is written before the case statements.

## Iteration Statements

Iteration statements or loops are those control flow statements that allow you to execute a set of statements repeatedly, based on whether a given condition is met or not. The set of statements can execute any number of times, for example, you can execute the set of statements zero, one, two, fifty, or hundred times.

The condition used in loops is a **Boolean** expression that evaluates to **true** or **false**. It is checked either at the beginning or at the end of the loop. If the condition is **true**, then the control of execution passes to the set of statements inside the loop. This is referred to as one iteration of the loop. After the completion of one iteration, control passes to the next iteration of the loop, where the condition is checked again. The loop continues as long as the condition is **true**. If the condition is **false**, control passes out of the loop and executes the statement that immediately follows the loop.

The loops that are available in C# are as follows:

- The **while** loop
- The **do** loop
- The **for** loop
- The **foreach** loop

Let’s discuss the use of each of these loops, one by one.

days of a week at locations indexed from 0 to 6. After this, we use a **while** loop to display the names of the days of a week on the console. The **while** loop first checks whether the current value of the loop control variable, *i*, is less than or equal to 6. If the condition in the **while** loop evaluates to **true**, then the name of the day of the week that is stored at the index value, which is the same as the current value of the loop control variable, is displayed on the console. The last statement in the loop body increments the value of the loop control variable by one.

- 8. Press the **F5** key on the keyboard to run the application. The output of the application appears as shown in Fig.C#-1.23:

![](img/9862a98a1a2d3bb14334137965a1ec60_312_0.png)

Fig.C#-1.23

You can notice that each iteration of the **while** loop writes the name of a day of a week and the loop ends after the names of all the days of a week have been written on the console.

### Using the do Loop

As you know, the condition in a **while** loop is checked at the beginning of the loop meaning that the loop can execute zero or more number of times. This implies if the condition in the **while** loop is **false** in the first iteration itself, then the **while** loop is not executed at all. However, there can be situations when you want to execute a set of statements at least once, for instance, when you want to display the initial bidding price for an auction. In such situations, you can use the **do** loop.

In the **do** loop, the set of statements appear before the condition, which is checked at the end of the loop. This implies that the first set of statements is executed and then the condition is checked. If the condition is **true**, then control goes to the beginning of the loop executing the set of statements again. The **do** loop executes as long as the condition is **true**. When the condition becomes **false**, the **do** loop terminates and control goes to the statement following the **do** loop. Therefore, the set of statements in a **do** loop is executed at least once irrespective of the value of the condition.

The syntax of the **do** loop is as follows:

```csharp
do
{
    //statements
}
while (condition);
```

In the preceding syntax,

- **do:** Refers to the do keyword that indicates the start of the **do** loop
- **statements:** Refers to the set of statements that is executed as a part of the **do** loop
- **while:** Refers to the while keyword that indicates the **while** statement in the **do** loop
- **condition:** Refers to the expression that is used as a condition for the **do** loop

Perform the following steps to understand the use of the **do** loop:

- 1. *Start* Visual Studio 2010.
- 2. *Select* **File→New→Project** on the menu bar. The **New Project** dialog box opens.
- 3. *Select* **Visual C#→Windows** from the **Installed Templates** section in the left pane of the **New Project** dialog box.
- 4. *Select* **Console Application** from the middle pane to create a Console application.
- 5. Enter the name of the application as **DoLoop** (also available on the CD) in the **Name** text box and an appropriate location for the application in the **Location** box.
- 6. Click the **OK** button to close the **New Project** dialog box and create the **DoLoop** application.
- 7. Add the highlighted code snippet, shown in Listing 1.8, to the **Program.cs** file:

### Listing 1.8: Showing the Code to Demonstrate the Use of the do Loop

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace DoLoop
{
    class Program
    {
        static void Main(string[] args)
        {
            int i = 0;
            int[] Numbers = {24, 13, 17, 34, 55, 86};
            Console.WriteLine("Array elements:");
            do
            {
                if (Numbers[i] % 2 == 0)
                    Console.WriteLine(Numbers[i] + ": even number");
                else
                    Console.WriteLine(Numbers[i] + ": odd number");
                i++;
            }
            while (i <= 5);
            Console.ReadLine();
        }
    }
}
```

In the highlighted code of Listing 1.8, we first declare an int type variable i, and initialize it with the value 0. The i variable acts as the loop control variable for the do loop. Then, we create an array of int type, Numbers, with a set of integer values. The Numbers array stores the integer values at locations indexed from 0 to 5. After this, we use a do loop to display the array elements on the console. Inside the do loop, we use an if statement to check whether the current array element is an even number or odd number, and display the element on the console marking it as even or odd. The loop control variable, i, is used to determine the current array element. The last statement in the loop body increments the value of the loop control variable by one. At the end of the loop, the current value of the loop control variable is checked whether it is less than or equal to 5.

- 8. Press the **F5** key on the keyboard to run the application. The output of the application appears as shown in Fig.C#-1.24:

![](img/9862a98a1a2d3bb14334137965a1ec60_313_0.png)
