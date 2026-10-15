In Listing 3.4, we have grouped the months having equal number of days, such as January and March. The reason for keeping all the cases producing the similar output at one place is that we can apply a single break statement to them. The default statement is executed, in case a user enters an invalid month.

Figure 3.6 shows the output of Listing 3.4:

![](bbox=[0.22, 0.16, 0.77, 0.22])

Figure 3.6: Showing the Output of the DaysInMonth Application

As shown in Figure 3.6 on entering the incorrect month, we get a message, stating You have entered an invalid month name.

# Using the while Loop

The while loop in C# is used to repeat a process until the specified condition becomes true. Let’s create a console application named MyWhileLoop (also available on the CD) that shows how to use a while loop. Listing 3.5 shows the code of the MyWhileLoop application:

Listing 3.5: Showing the Code of the MyWhileLoop Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace MywhileLoop
{
    class Program
    {
        static void Main(string[] args)
        {
            // Example 1
            // An example of a simple while loop
            Console.WriteLine("Loop 1:");
            int i = 0;
            while (i < 5)
            {
                Console.WriteLine("I = {0}", i);
                i++;
            }
            // Example 2
            // A while loop with a boolean
            boolean flag = false;
            i = 0;
            Console.WriteLine("\nLoop 2:");
            while (!flag)
            {
                if (i > 5)
                    flag = true;
                Console.WriteLine("I = {0}", i);
                i++;
            }
            // Example 3
            // A loop that will never execute
            Console.WriteLine("\nLoop 3: ");
            while (i <= 0)
            {
                Console.WriteLine("I = {0}", i);
                i++;
            }
            Console.Write("\nPress ENTER to quit...");
            Console.ReadLine();
        }
    }
}
```