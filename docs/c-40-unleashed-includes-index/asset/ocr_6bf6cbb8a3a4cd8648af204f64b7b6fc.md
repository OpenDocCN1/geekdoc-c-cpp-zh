# Projection

To transform objects in a sequence into corresponding objects in an output sequence, projection operators are used. While those preserve the element count of the source sequence, they transform each element, potentially realizing vertical partitioning. The typical example from the database world is the selection of a subset of columns.

# Select

The basic projection operator is Select, surfaced through the C# language using the select clause we've seen before. Two overloads exist, one of which takes in an extra integer argument to the selector delegate, representing the index of the element in the sequence. Notice that the transformative characteristic surfaces through the presence of two generic parameters (one to represent the type of the input sequence elements and one to represent the type of the output sequence elements):

```
static IEnumerable<R> Select<T,R>(this IEnumerable<T> source,
Func<T, R> selector);
static IEnumerable<R> Select<T,R>(this IEnumerable<T> source,
Func<T, int, R> selector);
```

Although the Select method can transform the type of the input objects, it's obvious this is not a required use. For example:

```
IEnumerable<int> twice = Enumerable.Range(0, 10).Select(n => n * 2);
IEnumerable<string> s = Enumerable.Range(0, 10).Select(n => n.ToString());
```

Notice how generic type parameters are inferred from the lambda expression used as the selector function. Although this is merely a convenience most of the time, it becomes a necessity when anonymous types are used.

Finally, an example of the use of the index-supplying overload to create a numbered list of items:

```
// { "0 is Zero", "1 is One", "2 is Two", "3 is Three" }
IEnumerable<string> numbers = new [] { "Zero", "One", "Two", "Three" }
    .Select((s, i) => i + " is " + s);
```

# Cast

The Cast operator is fairly similar to the OfType operator we saw before. It transforms input elements in a similar way but doesn't drop elements that aren't compatible with the specified target type. If such an element is encountered during enumeration, it will throw an InvalidCastException instead:

```
foreach (int x in new object[] { 1, "2", 3 }) {
    // Will blow up on the second iteration.
}
```