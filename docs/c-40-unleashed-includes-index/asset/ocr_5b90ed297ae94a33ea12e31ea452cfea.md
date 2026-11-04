By creating iterators that consume other iterators, you can realize powerful operators that apply on sequences of data. This is exactly what LINQ to Objects does with its standard query operators, as discussed in the “Standard Query Operators” section. Let’s give a simple example of such an operator implementation though, to commit the core concept and execute model of iterators to your memory. The following code realizes a filter, ignoring the code to validate arguments:

```
IEnumerable<T> Filter<T>(IEnumerable<T> source, Func<T, bool> filter) {
    foreach (T item in source)
        if (filter(item))
            yield return item;
}
```

Given an enumerable of objects of type T (which can be realized using an iterator) and a filter delegate, the Filter method can produce a new enumerable of T-typed objects with only those objects that pass the filter. It’s important to realize that calling the Filter method doesn’t trigger any execution yet. Only when the caller starts pulling data out of the returned enumerable (iterator) object will the iterator start making progress. For example, consider the following call:

```
var evens = Filter(new [] { 2, 5, 7, 4, 1, 9, 5, 8 }, n => n % 2 == 0);
```

Once the consumer gets an enumerator and starts calling MoveNext, the loop inside the filter starts to tick. One call to MoveNext on the enumerator for evens will cause the loop to run until the first even number is found, which happens to be the first element of the input. However, the second call to MoveNext causes the inner loop to run a couple more times until the next even number, 4, is found. And the third time, it takes even a bit longer to yield an item back to the consumer, as the iterator’s loop has to run until 8 is found in the input sequence. By making the filter delegate side effecting, you can see how execution takes place:

```
var evens = Filter(new [] { 2, 5, 7, 4, 1, 9, 5, 8 }, n => {
    Console.WriteLine("Filtering " + n);
    return n % 2 == 0;
});
```

On the consuming side, consider a simple foreach loop that drains the whole iterator until the very end:

```
foreach (int n in evens)
    Console.WriteLine(n);
```