# 20.2 Motivation for Generic Methods 857

generic Stack class, then instantiate Stack objects for a stack of ints, a stack of doubles,
a stack of strings and so on. The compiler performs type checking to ensure the Stack
stores only elements of the correct type.

This chapter presents examples of generic methods and generic classes. Chapter 21,
Generic Collections; Functional Programming with LINQ/PLINQ, discusses the .NET
Framework's generic collections. A collection is a data structure that maintains a
group of related objects or values. The .NET Framework collection uses generics to
allow you to specify the exact types of object that a particular collection will store.

# 20.2 Motivation for Generic Methods

Overloaded methods are often used to perform similar operations on different types ofndata. To understand the motivation for generic methods, let's begin with an example
(Fig. 20.1) that contains three overloaded DisplayArray methods (lines 23–31, lines
34–42 and lines 45–53). These methods display the elements of an int array, a double
array and a char array, respectively. Soon, we'll implement this program more concisely
and using a single generic method.

```
 // Fig. 20.1: OverloadedMethods.cs
// Using overloaded methods to display arrays of different types.
using System;
class OverloadedMethods
{
    static void Main(string[] args)
    {
        // create arrays of int, double and char
        int[] intArray = {1, 2, 3, 4, 5, 6};
        double[] doubleArray = {1.1, 2.2, 3.3, 4.4, 5.5, 6.6, 7.7};
        char[] charArray = {'H', 'E', 'L', 'L', 'O'};

        Console.Write("Array contains: ");
        DisplayArray(intArray); // pass an int array argument
        Console.Write("Array contains: ");
        DisplayArray(doubleArray); // pass a double array argument
        Console.Write("Array contains: ");
        DisplayArray(charArray); // pass a char array argument
    }

    // output array
    private static void DisplayArray(int[] inputArray)
    {
        foreach (var element in inputArray)
        {
            Console.Write($"{element} ");
        }
        Console.WriteLine();
    }

```

> Fig. 20.1 | Using overloaded methods to display arrays of different types. (Part I of 2.)