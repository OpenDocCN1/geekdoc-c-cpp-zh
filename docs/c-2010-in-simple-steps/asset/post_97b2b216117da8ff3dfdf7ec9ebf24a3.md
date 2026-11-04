
![](img/2db4b8b2cb67e7ccc52477a61fe289ab_95_0.png)

Fig.C# 3.14

In Fig.C# 3.14, the for loop displays the statement "Welcome to C# 2010 in Simple Steps." for a fixed number of times. This is an example of using the for loop for a fixed number of times.

> **Note**
>
> You can also create an infinite for loop. For creating an infinite for loop, you do not need to specify the loop expression. This implies that you need not to specify the value with which you want to increment or decrement the value of a variable in the for loop.

Next, let's discuss about the foreach loop.

## The foreach Loop

The foreach loop iterates through all the items in a collection, such as an array, which is an organized collection of variables of the same data type. The working of foreach loop is similar to that of the for loop. The statements in the foreach loop continue to execute for each element in a collection. After the foreach loop completes iterating through all the elements in a collection, the program control transfers to the next block of code. The syntax of the foreach loop is as follows:

```
foreach(<type> <item name> in <list>)
{
    ...    //statements
}
```

In the preceding syntax, type refers to the type of item contained in the list, item name is the meaningful name for a variable, in is a keyword, and list is the name of the collection of objects referred to in the foreach loop.

Now, let's create a console application named ForEachLoop to demonstrate the use of the foreach loop. Perform the following steps to create the ForEachLoop application:

- 1. Repeat steps 1 to 3 as discussed earlier while creating the IfExample application in the “The if Statement” section of this chapter.
- 2. Enter ForEachLoop in the Name text box to specify the name of the application, and specify an appropriate location for the application in the Location combo box. In this case, we have selected the default location, which is C:\users\temp\documents\visual studio 2010\Projects.
- 3. Click the OK button. The ForEachLoop application is created.
- 4. Add the highlighted code given in Listing 3.8 in the Program.cs file:

### Listing 3.8: Using the foreach Loop

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
            string[] bookTitles = new string[] { "Alice in wonderland",
            "Pelican Brief",
            "Ignited Minds" };
            Console.WriteLine("The available book titles are: ");
            foreach (string i in bookTitles)
            Console.WriteLine("\t" + i);
            Console.WriteLine("\nPress ENTER to quit...");
            Console.ReadLine();
        }
    }
}
```

In Listing 3.8, the foreach loop iterates through all the items in the string array, bookTitles, and displays the result in the output window.

- 5. Press the F5 key to run the ForEachLoop application. The output appears, as shown in Fig.C# 3.15:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_96_0.png)

Fig.C# 3.15

Now, let's discuss about different jump statements in C#.

## Exploring Jump Statements

The jump statements allow you to move the program control from one point to another at any particular instance during the execution of the program. The jump statements used in C# are break, continue, default, goto, and return. In this chapter, we discuss only the first two jump statements - break and continue, in the following sections.

## The break Statement

The break statement terminates the loop in which it exists. It also changes the flow of the execution of a program. After the loop is terminated, the program control is transferred to the next block of statements following the break statement. For instance, you can use the break statement within a switch statement to exit a case block. You can also use the break statement with the iteration statements.

Now, let's create a console application named BreakStatement to demonstrate the use of the break statement. Perform the following steps to create the BreakStatement application:

- 1. Repeat steps 1 to 3 as discussed earlier while creating the IfExample application in the “The if Statement” section of this chapter.
- 2. Enter BreakStatement in the Name text box to specify the name of the application, and specify an appropriate location for the application in the Location combo box. In this case, we have retained the default location, which is C:\users\temp\documents\visual studio 2010\Projects.
- 3. Click the OK button. The BreakStatement application is created.
- 4. Add the highlighted code given in Listing 3.9 in the Program.cs file:

### Listing 3.9: Using the break Statement

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace BreakStatement
{
    class Program
    {
        static void Main(string[] args)
        {
            for (int i = 0; i < 10; ++i)
            {
                if (i == 7)
                break;
                Console.WriteLine("Number {0}", i);
            }
            Console.ReadLine();
            Console.Write("\nPress ENTER to quit...");
        }
    }
}
```

In Listing 3.9, the break statement terminates the for loop when the value of i becomes 7.

- 5. Press the F5 key to run the BreakStatement application. The output appears, as shown in Fig.C# 3.16:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_97_0.png)

Fig.C# 3.16

Now let's learn about the continue statement.

## The continue Statement

The continue statement is used to transfer the program control to the beginning of the loop till a specific condition is satisfied. When the specified condition evaluates to false, the continue statement transfers the program control to the next statement.

Now, let's create a console application named ContinueStatement to demonstrate the use of the continue statement. Perform the following steps to create the ContinueStatement application:

- 1. Repeat steps 1 to 3 as discussed earlier while creating the IfExample application in the “The if Statement” section of this chapter.
- 2. Enter ContinueStatement in the Name text box to specify the name of the application, and specify an appropriate location for the application in the Location combo box. In this case, we have retained the default location, which is C:\users\temp\documents\visual studio 2010\Projects.
- 3. Click the OK button. The ContinueStatement application is created.
- 4. Add the highlighted code given in Listing 3.10 in the Program.cs file:

### Listing 3.10: Using the continue Statement

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace ContinueStatement
{
    class Program
    {
        static void Main(string[] args)
        {
            int number = 1;
            while (true)
            {
                Console.WriteLine(number);
                number++;
                if (number <= 10)
                    continue;
                else
                    break;
            }
            Console.WriteLine("Series is broken at number: " + number);
            Console.Write("\nPress ENTER to quit...");
            Console.ReadLine();
        }
    }
}
```

In Listing 3.10, the while loop will iterate infinitely, until the break keyword is executed. Inside the while loop, the if statement checks the condition whether the value of the variable is less than or equal to 10, and if this condition is evaluated to true, then the program control is transferred to the continue statement. The continue statement, in turn, transfers the program control to the beginning of the loop as long as the condition is satisfied. If the condition is evaluated to false, the program control is transferred to the else block and the execution of the while loop terminates. The break keyword inside the else block causes the program to terminate.

- 5. Press the F5 key to run the ContinueStatement application. The output of the application appears, as shown in Fig.C# 3.17:

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_98_0.png)

Fig.C# 3.17

Let's now learn about exceptions.

## Working with Exceptions

An exception is a runtime error that arises because of some unexpected situation. The exception handling feature in C# helps you to deal with any unexpected situation or abnormal condition that might occur when a program is being executed. For example, dividing a number by zero or passing a string value to an integer variable. During the execution of a program, if an exception occurs you can terminate the program explicitly by using the throw statement.
