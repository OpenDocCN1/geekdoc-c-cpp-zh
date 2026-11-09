```
```csharp
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace ContinueStatement
{
    class Program
    {
        static void Main(string[] args)
        {
            for (int i = 1; i <= 5; i++)
            {
                Console.WriteLine("Iteration " + i + " begins");
                if (i == 4)
                    continue;
                Console.WriteLine("Iteration " + i + " ends");
            }
            Console.ReadLine();
        }
    }
}
```
```

In the highlighted code of Listing 1.12, a for loop is used to iterate a set of statements five times. Inside the for loop, two statements are used that display two messages indicating the start and end of the current iteration on the console. An if statement is used between these two statements in order to check if the current value of the loop control variable, i, is 4, and also a continue statement is written immediately after the if condition. The continue statement will be executed only if the condition in the if statement evaluates to true. This implies that during the fourth iteration, the statement that indicates the end of the current iteration is not executed.

+   8. Press the F5 key on the keyboard to run the application. The output of the application appears, as shown in Fig.C#-1.28.

![](bbox=[0.375, 0.51, 0.648, 0.645])

In Fig.C#-1.28, you can notice that the message for indicating the end of the fourth iteration is not displayed.

# Summary

In this chapter, you have first learned about new features C# 2010. You have also learned about keywords, identifiers, and operators. Next, data types and conversion of data types have been discussed. In addition, you have learned about variables, constants, and arrays. Finally, you have learned about control flow statements, including selection, iteration, and jump statements, available in C# 2010.

In the next chapter, you learn about the concept of object-oriented programming.