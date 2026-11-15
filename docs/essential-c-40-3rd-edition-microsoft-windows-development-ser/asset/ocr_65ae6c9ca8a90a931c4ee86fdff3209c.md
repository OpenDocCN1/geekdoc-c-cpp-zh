# TABLE 14.2: Aggregate Functions on System.Linq.Enumerable

| Comment Type | Description |
| :--- | :--- |
| Count() | Provides a total count of the number of items within the collection |
| Average() | Calculates the average value for a numeric key selector |
| Sum() | Computes the sum values within a numeric collection |
| Max() | Determines the maximum value among a collection of numeric values |
| Min() | Determines the minimum value among a collection of numeric values |

Note that each method listed in Tables 14.1 and 14.2 will trigger deferred execution.

# ADVANCED TOPIC

# Queryable Extensions for IQueryable<T>

One virtually identical interface to IEnumerable<T> is IQueryable<T>. Because IQueryable<T> derives from IEnumerable<T>, it has all the members of IEnumerable<T> but only those declared directly (GetEnumerator(), for example). Extension methods are not inherited, so IQueryable<T> doesn't have any of the Enumerable extension methods. However, it has a similar extending class called System.Linq.Queryable that adds to IQueryable<T> virtually all of the same methods that Enumerable added to IEnumerable<T>. Therefore, it provides a very similar programming interface.

What makes IQueryable<T> unique is the fact that it enables custom LINQ providers. A LINQ provider subdivides expressions into their constituent parts. Once divided, the expression can be translated into another language, serialized for remote execution, injected with an asynchronous execution pattern, and much more. Essentially, LINQ providers allow for