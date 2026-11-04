Next, let's discuss about the for loop.

# The for Loop

The function of the for loop is also similar to that of the while loop. The only difference between the two is in the syntax. The syntax of the for loop includes an initializer, condition, and a loop expression. The initializer initializes a variable, the loop expression increments or decrements the value of the variable, and condition refers to a condition specified in the for loop. A for loop repeatedly executes the statement(s) enclosed within it until the specified condition evaluates to false. You can use the for loop when you know how many time you want to execute a statement or a block of statements. The syntax of the for loop is as follows:

```
```
for ( initializer; condition; loop expression)
{
...
...    //statements
}
```
```

In the preceding syntax, initializer is the starting value of a variable, condition is the expression that is checked before the execution of a loop, and loop expression either increments or decrements the loop counter.

Now, let's create a console application named ForLoop to demonstrate the use of the for loop. Perform the following steps to create the ForLoop application:

+   1. Repeat steps 1 to 3 as discussed earlier while creating the If Example application in the The if Statement section of this chapter.
+   2. Enter ForLoop in the Name text box to specify the name of the application, and specify an appropriate location for the application in the Location combo box. In this case, we have selected the default location, which is C:\users\temp\documents\visual studio 2010\Projects.
+   3. Click the OK button. The ForLoop application is created.
+   4. Add the highlighted code given in Listing 3.7 in the Program.cs file:

# Listing 3.7: Using the for Loop

```
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
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine("Welcome to C# 2010 in Simple Steps.");
                Console.Write("\nPress ENTER to quit...");
                Console.ReadLine();
            }
        }
    }
}
```
```

In Listing 3.7, an integer variable, i, is declared and initialized to 0 inside the for loop. The condition for the for loop is set to i<5. In addition, the i variable is incremented by 1 in the for loop expression.

5 Press the F5 key to run the ForLoop application. The output appears, as shown in Fig.C.3.14: