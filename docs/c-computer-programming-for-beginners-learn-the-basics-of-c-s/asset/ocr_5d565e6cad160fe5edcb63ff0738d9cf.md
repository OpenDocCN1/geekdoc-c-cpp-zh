of the else statement. It is the basics of English after all. The else statement serves as a companion to the if statement. Its job is to offer an alternative to the execution of the code when the condition stated by the if statement has not been met.

# Understanding the Usage of the if Statement

In order to understand how the if statement and the else statement is used in C#, an example application can be of great help. As such, here is one such example that demonstrates the use of conditional logic in C#.

using System;

```
namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            Int number;
            Console.WriteLine("Please enter a number between 0 and 10 : ");
            number = int.Parse(Console.ReadLine());
            if (number > 10)
            {
                Console.WriteLine("Hey! The number should be 10 or less!");
            }
            else
            {
                if (number < 0)
                {
                    Console.WriteLine("Hey! The number should be 0 or more!");
                }
                else
                {
                    Console.WriteLine("Good job!");
                }
            }
            Console.ReadLine();
        }
    }
}
```