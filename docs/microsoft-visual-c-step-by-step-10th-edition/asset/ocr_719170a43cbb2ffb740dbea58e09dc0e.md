+   - The Select method is not actually a method of the Array type; it's an extension method of the Enumerable class. The Enumerable class is located in the System.Linq namespace and provides a substantial set of static methods for querying objects that implement the generic Iumerable<T> interface.

The preceding example uses the Select method of the customers array to generate an IEnumerable<string> object named customerFirstNames.(It is of type IEnumerable<string> because the Select method returns an enumerable collection of customer first names, which are strings). The foreach statement iterates through this collection of strings, printing out the first name of each customer in the following sequence:

+   Kim
Jeff
Charlie
Chris
Dave
Ann
John
David
Greg
Tim

You can now display the first name of each customer. Fetching the first and last names of each customer is slightly trickier, however. If you examine the definition of the Enumerable.Select method in the System.Linq namespace in the documentation supplied with Microsoft Visual Studio 2022, you’ll see that it looks like this:

Click here to view code image

```
public static IEnumerable<TResult> Select<TSource, TResult> (
    this IEnumerable<TSource> source,
    Func<TSource, TResult> selector
```

What this actually is that Select is a generic method that takes two type parameters named TSource and TResult as well as two ordinary parameters named source and selector. TSource is the type of the collection for which you’re generating an enumerable set of results (customer objects in