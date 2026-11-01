```
Console.WriteLine();
```

Of course the result now looks like this:

1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20

![](bbox=[0.15, 0.26, 0.85, 0.4])

You can combine the result with other extension methods to get a different result — for example, using the Select() extension method:

```
var values = Enumerable.Range(1, 20).Select(n => n * 3);
```

The Empty() method returns an iterator that does not return values. This can be used for parameters that require a collection where you can pass an empty collection.

The Repeat() method returns an iterator that returns the same value a specific number of times.

# PARALLEL LINQ

.NET 4 contains a new class ParallelEnumerable in the System.Linq namespace to split the work of queries across multiple threads. Although the Enumerable class defines extension methods to the IEnumerable<T> interface, most extension methods of the ParallelEnumerable class are extensions for the class ParallelQuery<TSource>. One important exception is the AsParallel() method that extends IEnumerable<TSource> and returns ParallelQuery<TSource>, so a normal collection class can be queried in a parallel manner.

# Parallel Queries

To demonstrate Parallel LINQ, a large collection is needed. With small collections you will not see any effect when the collection fits inside the CPU's cache. In the following code, a large int array is filled with random values:

```
const int arraySize = 10000000;
var data = new int[arraySize];
var r = new Random();
for (int i = 0; i < arraySize; i++)
{
    data[i] = r.Next(40);
}
```

code snippet ParallelLinqSample/Program.cs

Now you can use a LINQ query to filter the data and get a sum of the filtered data. The query defines a filter with the where clause to summarize only the items with values < 20, and then the aggregation function sum is invoked. The only difference to the LINQ queries you've seen so far is the call to the AsParallel() method.

```
var sum = (from x in data.AsParallel()
           where x < 20
           select x).Sum();
```

As with the LINQ queries you've seen so far, the compiler changes the syntax to invoke the methods AsParallel(), Where(), Select(), and Sum(). AsParallel() is defined with the ParallelEnumerable class to extend the IEnumerable<T> interface, so it can be called with a simple array. AsParallel()