```
using System;
using System.Collections.Generic;
Stack<int> numbers = new Stack<int>();
// fill the stack
Console.WriteLine("Pushing items onto the stack:");
foreach (int number in new int[4]{9, 3, 7, 2})
{
    numbers.Push(number);
    Console.WriteLine($"{number}\} has been pushed on the stack");
}
// iterate through the stack
Console.WriteLine("\n The stack now contains:");
foreach (int number in numbers)
{
    Console.WriteLine(number);
}
// empty the stack
Console.WriteLine("\n Popping items from the stack:");
while (numbers.Count > 0)
{
    int number = numbers.Pop();
    Console.WriteLine($"{number}\} has been popped off the stack");
}
```