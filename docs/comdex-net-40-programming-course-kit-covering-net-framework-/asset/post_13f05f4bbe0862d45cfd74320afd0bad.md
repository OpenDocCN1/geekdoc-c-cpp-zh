
Let’s now learn about the for loop.

## Using the For Loop

The for loop is one of the most popular loops. The condition in the for loop is checked at the beginning of the loop. This implies that the set of statements inside the for loop is executed only when the condition is true. Therefore, the set of statements inside the for loop is executed zero or more number of times. The for loop is suitable either to traverse through the elements of arrays or to execute a set of statements predefined number of times.

The syntax of the for loop is as follows:

```csharp
for (initializer; condition; update)
{
    //statements
}
```

In the preceding syntax,

- **for:** Refers to the for keyword that indicates a for loop.
- **initializer:** Refers to the *initializer expression*, which is an expression that initializes the loop control variable(s). A *loop control variable* is a local variable whose value controls the execution of the for loop.
- **condition:** Refers to the *condition expression*, which is a Boolean expression. This expression uses the loop control variable to determine whether the set of statements inside the for loop is executed or not.
- **update:** Refers to the *update expression*, which is an expression that increments or decrements the value of the loop control variable. This expression is executed at the end of each iteration of the for loop.
- **statements:** Refers to the set of statements inside the for loop that is executed when the condition expression evaluates to **true**.

When the for loop executes, the initializer expression is executed first. After this, the condition expression is executed. If the condition expression is true, then the set of statements inside the for loop is executed. This is followed by the execution of update expression. The control again passes to the condition expression, where it is evaluated again. This process continues as long as the condition is true. When the condition becomes false, the for loop is terminated and the control goes to the statement that succeeds the for loop. Note that the initializer expression executes only once; whereas, the condition and update expressions may execute more than once.

Perform the following steps to understand the use of the for loop:

- 1. *Start* Visual Studio 2010.
- 2. *Select* **File→New→Project** from the menu bar. The **New Project** dialog box opens.
- 3. *Select* **Visual C#→Windows** from the **Installed Templates** section in the left pane of the **New Project** dialog box.
- 4. *Select* **Console Application** from the middle pane to create a Console application.
- 5. Enter the name of the application as **ForLoop** (also available on the CD) in the **Name** text box and an appropriate location for the application in the **Location** box.
- 6. *Click* the **OK** button to close the **New Project** dialog box and create the **ForLoop** application.
- 7. *Add* the highlighted code snippet, shown in Listing 1.9, to the **Program.cs** file.

**Listing 1.9:** Showing the code to Demonstrate the Use of the For Loop

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace ForLoop
{
    class Program
    {
        static void Main(string[] args)
        {
            int i;
            for (i = 1; i <= 10; ++i)
            {
                Console.WriteLine("Iteration " + i);
            }
            Console.WriteLine("For loop terminated");
            Console.ReadLine();
        }
    }
}
```

In the highlighted code of Listing 1.9, we first declare an int type variable, i. The i variable acts as the loop control variable for the for loop. It is declared before the for loop but initialized to 1 in the for loop. After initializing the i variable, the for loop checks the expression, i <= 10, which is the condition of the for loop. If this condition is true, then the number of the current iteration is displayed. After this, the i variable is incremented by 1. This completes one iteration of the for loop. The control now goes to the condition where the updated value of the i variable is checked again. In this way, the for loop iterates 10 times. At the end of the tenth iteration, the i variable is equal to 11. Therefore, in the eleventh iteration, the condition becomes false. As a result, the control terminates the for loop, and the message For loop terminated is displayed.

- 8. Press the F5 key on the keyboard to run the application. The output of the application appears, as shown in Fig.C#-1.25:

![](img/9862a98a1a2d3bb14334137965a1ec60_315_0.png)

Fig.C#-1.25

Note that you can omit any or all of the initializer, condition, or update expressions. However, you cannot omit the semicolon that separates the three expressions. You can omit the initializer expression only when you declare and initialize the loop control variable before the for loop. If you omit the condition expression in a for loop, then by default, the condition is assumed to be true and the for loop keeps executing infinitely. The loops that keep executing forever are called infinite loops. You can also create an infinite loop by omitting the update expression of the for loop. However, you should avoid creating infinite loops while developing programs.

Let's look at the example of an infinite for loop given in the following code snippet:

```csharp
for (int i=0;i<3;)
{
    Console.WriteLine("Infinite Loop");
}
```

In the preceding code snippet, the loop control variable, i, is declared and initialized to zero. In the for loop, the expression, i<3, is the condition. Note that there is no update expression in the for loop. Therefore, in this case, the i<3 condition is always true because the value of the i variable does not change and is always less than 3. This implies that this for loop executes an infinite number of times, displaying the message Infinite Loop.

## Using the foreach Loop

The foreach loop is similar to the for loop with a slight difference. The foreach loop allows you to iterate through arrays and collections (collections are similar to arrays but unlike arrays, they can store different types of objects together). Unlike the for loop, the foreach loop does not check any condition. The foreach loop simply goes through the items or elements of an array or collection and executes a set of statements for every element. The foreach loop automatically terminates after the execution of statements for the last element of the array or collection.

The syntax for the foreach loop is as follows:

```csharp
foreach (Data_Type Item_Variable in Collection_Name)
{
    //statements
}
```

In the preceding syntax,

- `foreach`: Refers to the foreach keyword that indicates a foreach loop
- `Data_Type`: Refers to the data type of the items of the array or collection
- `Item_Variable`: Refers to an item or element of the array or collection
- `in`: Refers to the in keyword
- `Collection_Name`: Refers to an array or collection
- `statements`: Refers to the set of statements that is executed for every item in the array or collection

Perform the following steps to understand the use of the **foreach** loop:

- 1. *Start Visual Studio 2010.*
- 2. *Select* **File→New→Project** from the menu bar. The **New Project** dialog box opens.
- 3. *Select* **Visual C#→Windows** from the **Installed Templates** section in the left pane of the **New Project** dialog box.
- 4. *Select* **Console Application** from the middle pane to create a Console application.
- 5. *Enter* the name of the application as **ForEachLoop** (also available on the CD) in the **Name** text box and an appropriate location for the application in the **Location** box.
- 6. *Click* the **OK** button to close the **New Project** dialog box and create the **ForEachLoop** application.
- 7. *Add* the highlighted code snippet, shown in Listing 1.10, to the **Program.cs** file.

**Listing 1.10:** Showing the Code to Demonstrate the Use of the **foreach** Loop

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace ForEachLoop
{
    class Program
    {
        static void Main(string[] args)
        {
            string[] Days = { "Sunday", "Monday", "Tuesday", "Wednesday",
                "Thursday", "Friday", "Saturday" };
            Console.WriteLine("Days of week:");
            foreach (string day in Days)
            {
                Console.WriteLine(day);
            }
            Console.ReadLine();
        }
    }
}
```

In Listing 1.10, we first create an array of string type, **Days**, with the names of the days in a week. After this, we use a **foreach** loop to display the array elements on the console. In the **foreach** loop, the string variable, **day**, represents a single element of the **Days** array.

- 8. *Press* the **F5** key on the keyboard to run the application. The output of the application appears, as shown in Fig.C#-1.26:
