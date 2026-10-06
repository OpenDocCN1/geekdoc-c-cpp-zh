(predicate is a function that takes a single argument and returns true or false based on the value of the parameter), that element is returned. Otherwise, element is skipped. The yield return statement will only ever return one element and suspend execution until the next element is requested, either manually (calling the MoveNext method) or by using a foreach loop.
The Where operator (with the argument checking code removed for clarity) is implemented in the following general form:

```
public static IEnumerable<T> Where<T>(n    IEnumerable<T> source,
    Func<T, bool> predicate)
{
    foreach (T element in source)
    {
        if (predicate(element))
            yield return element;
    }
}
```

# Building the TakeRange Operator

To demonstrate how to write a sequence operator, we can write an operator called TakeRange, which will return elements in a sequence after an element satisfies the start predicate in a sequence until an element satisfies the end predicate in the same sequence.

The TakeRange operator has the following requirements:

+   - Take an input source and return elements that fall between the first element that passes a “start” predicate until the first element that passes the “end” predicate.
- Allow the start predicate to be optional. In this case all elements in the sequence are returned until the end predicate is satisfied.
- Not fail if the start or end predicate is never satisfied; just return an empty sequence.
- Throw an ArgumentNullException if the source sequence is null.
- Throw an ArgumentNullException if either the start or end predicate is null in the appropriate overloads.

The TakeRange operator will extend any collection that implements IEnumerable<T>, as the LINQ to Objects standard query operators always do. Due to this knowledge, the only certainty we have about the source