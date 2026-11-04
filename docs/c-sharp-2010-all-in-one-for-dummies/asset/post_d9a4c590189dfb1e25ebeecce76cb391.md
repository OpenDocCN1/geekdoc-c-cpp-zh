
named Length that contains its length. `doublesArray.Length` has the same value as `numElements`.

The following for loop is preferable:

```csharp
// Accumulate the values into an array
for (int i = 0; i < doublesArray.Length; i++) ...
```

## Initializing an array

The following lines show an array with its initializer and then one that allocates space but doesn't initialize the elements' values:

```csharp
double[] fixedLengthArray = { 6, 2, 7, 3.5, 6.5, 8, 1, 9, 1, 3 };
double[] variableLengthArray = new double[10];
```

You can do it visually using the following code:

```csharp
double[] fixedLengthArray = new double[10] { 5, 2, 7, 3.5, 6.5, 8, 1, 9, 1, 3 };
```

Here, you have specifically allocated the memory using `new` and then followed that declaration with the initial values for the members of the array. I think I can predict which form you prefer. *(Hint: Line 1?)*

## A Loop Made for foreach Array

Given an array of Student objects, the following loop averages their GPAs:

```csharp
public class Student  // Read about classes in Book 11.
{
    public string name;
    public double gpa;        // Grade point average
}
public class Program
{
    public static void Main(string[] args)
    {
        // . . . create the array somehow . . .
        // Now average the students you have.
        double sum = 0.0;
        for (int i = 0; i < students.Length; i++)
        {
            sum += students[i].gpa;
        }
        double avg = sum / students.Length;
        // . . . do something with the average . . .
    }
}
```

The for loop iterates through the members of the array. (Yes, you can have arrays of any sort of object, not just of simple types such as `double` and `string`. You most likely haven't been formally introduced to classes yet, so bear with me a bit longer. I get into them in the next book.)

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_141_0.png)

students.Length contains the number of elements in the array.

C# provides another loop, named foreach, designed specifically for iterating through collections such as the array. It works this way:

```csharp
// Now average the students that you have.
double sum = 0.0;
foreach (Student student in students)
{
    sum += student.gpa; // This extracts the current student's GPA.
}
double avg = sum / students.Length;
```

The first time through the loop, foreach fetches the first Student object in the array and stores it in the variable student. On each subsequent pass, foreach retrieves the next element. Control passes out of the foreach loop when all elements in the array have been processed.

Notice that no index appears in the foreach statement. The lack of an index greatly reduces the chance of error and is simpler to write than the for statement, although sometimes that index is handy and you prefer a for loop.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_141_1.png)

The foreach loop is even more powerful than it would seem from the example. This statement works on other collection types in addition to arrays. In addition, foreach handles multidimensional arrays (arrays of arrays, in effect), a topic I don't describe in this book. To find out all about multidimensional arrays, look up multidimensional arrays in the C# Help system.

## Sorting Arrays of Data

A common programming challenge is the need to sort the elements within an array. Just because an array cannot grow or shrink doesn't mean that the elements within it cannot be moved, removed, or added. For example, the following code snippet swaps the location of two string elements within the array strings:

```csharp
string temp = strings[i]; // Save the i'th string.
strings[i] = strings[k]; // Replace it with the kth.
strings[k] = temp;       // Replace kth with temp.
```

In this example, the object reference in the ith location in the strings array is saved so that it isn't lost when the second statement replaces it with another element. Finally, the temp variable is saved back into the kth location. Pictorially, this process looks like Figure 6-1.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_141_2.png)

The data collections discussed in the rest of this chapter are more versatile than the array for adding and removing elements.

**Before:**

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_142_0.png)

Figure 6-1: The term swapping two objects means swapping references to two objects.

**After:**

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_142_1.png)

The following program demonstrates how to use the ability to manipulate elements within an array as part of a sort. This particular sorting algorithm is the bubble sort. Though it's not so great on large arrays with thousands of elements, it's simple and effective on small arrays:

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_142_2.png)

```csharp
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

            Console.WriteLine("\nNow listed alphabetically: ");
            // Array.Sort() is a method on the Array class.
            // Array.Sort() does its work in-place in the planets array,
            // which leaves you without a copy of the original array. The
            // solution is to copy the old array to a new one and sort it.
            string[] sortedNames = planets;
            Array.Sort(sortedNames);
            // This demonstrates that (a) sortedNames contains the same
            // strings as planets and (b) that they're now sorted.
            foreach (string planet in sortedNames)
            {
                Console.WriteLine("\t" + planet);
            }

            Console.WriteLine("\nList by name length - shortest first: ");
            // This algorithm is called "Bubble Sort"; it's the simplest
            // but worst-performing sort. The Array.Sort() method is much
            // more efficient, but I couldn't use it directly to sort the
            // planets in order of name length because it sorts strings,
            // not their lengths.
            int outer;  // Index of the outer loop
            int inner;  // Index of the inner loop
            // Loop DOWN from last index to first: planets[4] to planets[0].
            for (outer = planets.Length - 1; outer >= 0; outer--)
            {
                // On each outer loop, loop through all elements BEYOND the
                // current outer element. This loop goes up, from planets[1]
                // to planets[4]. Using the for loop, you can traverse the
                // array in either direction.
                for (inner = 1; inner <= outer; inner++)
                {
                    // Compare adjacent elements. If the earlier one is longer
                    // than the later one, swap them. This shows how you can
                    // swap one array element with another when they're out of order.
                    if (planets[inner - 1].Length > planets[inner].Length)
                    {
                        // Temporarily store one planet.
                        string temp = planets[inner - 1];
                        // Now overwrite that planet with the other one.
                        planets[inner - 1] = planets[inner];
                        // Finally, reclaim the planet stored in temp and put
                        // it in place of the other.
                        planets[inner] = temp;
                    }
                }
            }
            foreach (string planet in planets)
            {
                Console.WriteLine("\t" + planet);
            }

            Console.WriteLine("\nNow listed longest first: ");
            // That is, just loop down through the sorted planets.
            for (int i = planets.Length - 1; i >= 0; i--)
            {
                Console.WriteLine("\t" + planets[i]);
            }

            Console.WriteLine("\nPress Enter to terminate...");
            Console.Read();
        }
    }
}
```
