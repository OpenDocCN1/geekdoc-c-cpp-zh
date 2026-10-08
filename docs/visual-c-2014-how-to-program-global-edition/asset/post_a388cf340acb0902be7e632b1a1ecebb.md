
## 21.11 Functional Programming with LINQ Method-Call Syntax and Lambdas

A key aspect of functional programming is immutability—not modifying the data source being processed or any other program state, as counter-control variables in loops. Using internal iteration, you eliminate from programs common errors that are caused by modifying data incorrectly. This makes it easier to write correct code.

## Filter, Map and Reduce

Three common functional-programming operations that you'll perform on collections of data are filter, map and reduce:

- filter operation results in a new collection containing only the elements that satisfy a condition. For example, you might filter a collection of ints to locate only the even integers, or you might filter a collection of employees to locate only in a specific department of a large company. Filter operations do not modify the original collection.

- map operation results in a new collection where each element of the original collection is mapped to a new value (possibly of a different type)—e.g., mapping numeric values to the squares of the numeric values. The new collection has the same number of elements as the collection that was mapped. Map operations do not modify the original collection.

- reduce operation combines the elements of a collection into a single new value using a lambda that specifies how to combine the elements. For example, you might reduce a collection of 1st grades from 0 to 100 to an enum number of students with a grade greater than or equal to 60. Reduce operations do not modify the original collection.

In the next section, we'll demonstrate filter, map and reduce operations using class extension methods where Select and Aggregate, respectively. The extension methods defined by class Enumerable on collections that implement the interface IEnumerable<T>.

## C# and Functional Programming

Though C# was not originally designed as a functional-programming language, C#'s query syntax and LINQ extension methods support functional-programming techniques, such as internal iteration and immutability. In addition, C# 6's getter-only, auto-implemented properties make it easier to define immutable types. We expect futures of C# and most other popular programming languages to include more functional-programming capabilities that make implementing programs with a functional style natural.

## 21.11 Functional Programming with LINQ Method-Call Syntax and Lambdas

In Chapter 9, we introduced LINQ, demonstrated LINQ query syntax and introduced some LINQ extension methods. The tasks you can perform with LINQ query syntax can also be performed with various LINQ extension methods and lambdas. In fact, the compiler translates LINQ query into calls to LINQ extension methods that receive lambdas as arguments. For example, lines 21–24 of Fig. 9.2

```csharp
var filtered =
  from value in values // data source is
  where value > 4
  select value;
```

can be written as

```csharp
var filtered = values.Where(value => value > 4);
```

Figure 21.8 demonstrates simple functional programming techniques using a list of integers.

```csharp
// Fig. 21.8: FunctionalProgramming.cs
// Functional programming with LINQ extension methods and lambdas.
using System;
using System.Collections.Generic;
using System.Linq;

namespace FilterMapReduce
{
    class FunctionalProgramming
    {
        static void Main()
        {
            var values = new List<int>{3, 10, 6, 1, 4, 8, 2, 5, 9, 7};
            Console.WriteLine("Original values: ");
            values.Display(); // call extension method

            // display the Min, Max, Sum and Average
            Console.WriteLine($"\nMin: {values.Min()}");
            Console.WriteLine($"\nMax: {values.Max()}");
            Console.WriteLine($"\nSum: {values.Sum()}");
            Console.WriteLine($"\nAverage: {values.Average()}");

            // sum of values via Aggregate
            Console.WriteLine("\nSum via Aggregate method: " +
                values.Aggregate(0, (x, y) => x + y));

            // sum of squares via Aggregate
            Console.WriteLine("\nSum of squares via Aggregate method: " +
                values.Aggregate(0, (x, y) => x + y * y));

            // product of values via Aggregate
            Console.WriteLine("\nProduct via Aggregate method: " +
                values.Aggregate(1, (x, y) => x * y));

            // even values displayed in sorted order:
            Console.Write("\neven values displayed in sorted order: ");
            values.Where(value => value % 2 == 0) // find even integers
                .OrderBy(value => value) // sort remaining values
                .Display(); // show results
        }
    }
}
```

**Figure 21.8** Functional programming with LINQ extension methods and lambdas. (Part I of 2.)

```csharp
// odd values multiplied by 10 and displayed in sorted order
Console.Write(
    "Odd values multiplied by 10 displayed in sorted order: "
);
values.Where(value => value % 2 != 0) // find odd integers
    .Select(value => value * 10) // multiply each by 10
    .OrderBy(value => value) // sort the values
    .Display(); // show results

// display original values again to prove they were not modified
Console.Write("\nOriginal values: ");
values.Display(); // call Display extension method

// declares an extension method
static class Extensions
{
    // extension method that displays all elements separated by spaces
    public static void Display<T>(this IEnumerable<T> data)
    {
        Console.WriteLine(string.Join(" ", data));
    }
}
```

Original values: 3 10 6 1 4 8 2 5 9 7

Min: 1
Max: 10
Sum: 55
Average: 5.5

Sum via Aggregate method: 55
Sum of squares via Aggregate method: 385
Product via Aggregate method: 3628800

Even values displayed in sorted order: 2 4 6 8 10
Odd values multiplied by 10 displayed in sorted order: 10 30 50 70 90

Original values: 3 10 6 1 4 8 2 5 9 7

> Fig. 21.8 Functional programming with LINQ extension methods and lambdas. (Part 2 of 2.)

## Extension Method

Throughout this example, we display the results of various operations by calling our extension method, which is defined in the static class Extensions. At the beginning and end of Main, we call Display on the IEnumerable<T> argument to display the elements in order.

## 21.11.1 LINQ Extension Methods: Min, Max, Sum and Average

Class Enumerable defines various LINQ extension methods for performing common operations including:

- Min (line 19) returns the smallest value in the collection.
- Max (line 20) returns the largest value in the collection.
- Sum (line 21) returns the sum of all the values.
- Average (line 22) returns the average of all values.

## Iteration and Mutation Are Hidden from You

In fact, the LINQ operations have no side effects that modify the original collection or any other variables in the app—

- We simply say what we want to accomplish, not *how* to accomplish it.
- The values collection is *not modified* (confirmed by line 52).

Of course, behind the scenes iteration and mutable variables are required:

- All four extension methods iterate the collection and keep track of the current element.
- While iterating the collection, Min and Average must store the current smallest and largest items, respectively, and Sum and Average must keep track of the total of the elements processed so far—all of these mutating a local variable.

The other operations in Sections 21.11.2–21.11.4 also require iteration and mutable variables, but the *library*—which has already been debugged and tested—handles these details for you. See how LINQ extension methods like Min, Max, Sum and Average implement these concepts, check out Enumerable in the .NET source code for

```
https://github.com/dotnet/corefx/tree/master/src/System.Linq/src/System/Linq
```

## 21.11.2 Aggregate Extension Method for Reduction Operations

You can define your reductions with the *Aggregate* LINQ method. For example, the call to Aggregate in lines 25–26 sums the elements of values. The version of Aggregate used here receives two arguments:

- The first argument (0) is a value that helps you begin the reduction operation. When summing the elements of a collection, begin with the value 0. Shortly, we’ll use 1 to begin calculating the product of the elements.
- The second argument is a delegate of type *Func* (namespace System) represents a method which receives two arguments of the type and returns a value—there are many versions of *Func* that specify from 0 to 16 arguments of any
