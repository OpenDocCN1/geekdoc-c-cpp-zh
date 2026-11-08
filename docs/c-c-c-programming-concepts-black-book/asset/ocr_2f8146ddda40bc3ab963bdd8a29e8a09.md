```
```csharp
Console.WriteLine("The element at the sixth position is {0}", elementAt);

var firstAt = set1.First(i=> i%5 == 0);
Console.WriteLine("The first element which is divisible by 5 is {0}", firstAt);

var single = set2.Single();
Console.WriteLine("The collection has a single value {0}", single);
    }
}
```
```

In the preceding example, we have declared an integer array and a string array. Then, we have fetched the first and last elements of the integer array by using the *First()* and *Last()* extension methods, respectively. Next, by using the *ElementAt()* method, we have retrieved the element at the sixth position and then fetched the first occurrence of an element, which is divisible by 5. At the end, the *Single()* method is applied on the string array. The output of the program is given as follows:

```
```text
The first element in the collection is 1
The last element in the collection is 9
The element at the sixth position is 7
The first element which is divisible by 5 is 5
The collection has a single value Hello
```
```

# Aggregation Operators

Aggregation operators provide the basic math operations, such as sum, min, max, and average, over a collection of elements. Listing 19.38 shows the implementation of aggregation operators:

**Listing 19.38:** Showing the Implementation of Aggregation Operators

```
```csharp
using System;
using System.Linq;

class program
{
    public static void Main()
    {
        int[] set = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };

        var count = set.Count();
        Console.WriteLine("The count of element in the collection is {0}", count);

        var max = set.Max();
        Console.WriteLine("The maximum number in the collection is {0}", max);

        var min = set.Min();
        Console.WriteLine("The minimum number in the collection is {0}", min);

        var sum = set.Sum();
        Console.WriteLine("The sum of the collection is {0}", sum);

        var avg = set.Average();
        Console.WriteLine("The average of the collection is {0}", avg);
    }
}
```
```