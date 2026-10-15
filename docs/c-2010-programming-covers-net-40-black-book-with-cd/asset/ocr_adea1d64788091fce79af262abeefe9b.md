# sing the continue Statement

The continue statement is used to transfer the program control to the beginning of the loop. It continues to transfer the program control until a certain condition satisfies. Let’s create a console application named MyContinueStatement (also available on the CD) to show the use of continue statement. Listing 3.13 shows the code of MyContinueStatement application:

# Listing 3.13: Showing the Code of the MyContinueStatement Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace MyContinueStatement
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
            Console.WriteLine("Series is breaked at number: " + number);
            Console.Write("\nPress ENTER to quit...");
            Console.ReadLine();
        }
    }
}
```

In Listing 3.13, the while loop executes as long as the condition is true. Inside the while loop, the if statement checks whether the entered number is less than 10 and transfers the program control to the continue statement. The continue statement, in turn, transfers the program control to the beginning of the loop as long as the condition is satisfied. If the condition fails, the program control transfers to the else block and the loop breaks.

Figure 3.15 shows the output of Listing 3.13:

![](bbox=[0.27, 0.64, 0.62, 0.82])

# Figure 3.15: Showing the Output of MyContinueStatement Application

# Handling an Exception

Exception handling forms the core of error handling in C#. Suppose you are creating a program to divide two numbers and you want that the program should not be terminated abnormally due to exceptions. To ensure this, you have to handle the exception that is expected to cause abnormal termination even before running the