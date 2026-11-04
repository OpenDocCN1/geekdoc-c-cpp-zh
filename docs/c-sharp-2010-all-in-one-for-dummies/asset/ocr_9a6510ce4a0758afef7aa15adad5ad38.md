# Before:

![](bbox=[0.25, 0.2, 0.6, 0.42])

Figure 6-1:
The term swapping two objects means swapping references to two objects.

# After:

![](bbox=[0.25, 0.46, 0.6, 0.68])

The following program demonstrates how to use the ability to manipulate elements within an array as part of a sort. This particular sorting algorithm is the bubble sort. Though it's not so great on large arrays with thousands of elements, it's simple and effective on small arrays:

![](bbox=[0.05, 0.78, 0.18, 0.92])

```
// BubbleSortArray -- Given a list of planets, sort their
// names: first, in alphabetical order.
// Second, by the length of their names, shortest to longest.
// Third, from longest to shortest.
// This demonstrates using and sorting arrays, working with
// them by array index. Two sort algorithms are used:
// 1. The Sort algorithm used by class Array's Sort() method.
// 2. The classic Bubble Sort algorithm.
using System;

namespace BubbleSortArray
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("The 5 planets closest to the sun, in order: ");
            string[] planets = 
                new string[] { "Mercury", "Venus", "Earth", "Mars", "Jupiter" };
            foreach (string planet in planets)
            {
                // Use the special char \t to insert a tab in the printed line.
                Console.WriteLine("\t" + planet);
            }
        }
    }
}
```