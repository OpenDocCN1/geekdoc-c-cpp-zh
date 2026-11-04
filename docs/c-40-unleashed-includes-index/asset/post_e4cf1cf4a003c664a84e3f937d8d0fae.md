
```csharp
namespace System.Linq {
    public static class Enumerable {
        ...
        public static IEnumerable<R> Select<T, R>(this IEnumerable<T> source,
            Func<T, R> selector);
        public static IEnumerable<T> Where<T>(this IEnumerable<T> source,
            Func<T, bool> predicate);
        ...
    }
}
```

One important thing about those `IEnumerable<T>` extension methods is the fact they take in generic `Func` delegate objects for certain parameters. In other words, things such as filter clauses (from where) and selectors (from select) are represented as delegates that can be invoked by the query operator to carry out certain jobs. For example, the `Where` method will, as you will see when talking about iterators, iterate over the source's objects and evaluate the filter function for all of those using delegate invocation.

Knowing where to look for the extension methods gives you a direct ticket to further exploration of the various query operators, simply by looking at the extension methods defined in the `Enumerable` static class. Or we can run our grouping example we saw earlier, to display all the `Enumerable` methods together with the overload count. Adding a few more clauses to only show static methods (because extension methods are always static) and to order operators alphabetically, we get to the following query:

```csharp
var queryOperators = from m in typeof(Enumerable).GetMethods()
    where m.IsStatic
    group m by m.Name into queryOperator
    orderby queryOperator.Key /* Key is method name m.Name */
    select new { Name = queryOperator.Key,
        Overloads = queryOperator.Count() };
foreach (var queryOperator in queryOperators) {
    Console.WriteLine("{0} has {1} overload(s)", queryOperator.Name,
        queryOperator.Overloads);
}
```

Viewing LINQ operators using LINQ, can it get any better? Either way, the result of this query is shown in Table 20.1.

**TABLE 20.1 LINQ to Objects Query Operator Methods**

| Method | # | Method | # | Method | # |
|---|---|---|---|---|---|
| Aggregate | 3 | GroupBy | 8 | SequenceEqual | 2 |
| All | 1 | GroupJoin | 2 | Single | 2 |
| Any | 2 | Intersect | 2 | SingleOrDefault | 2 |
| AsEnumerable | 1 | Join | 2 | Skip | 1 |
| Average | 20 | Last | 2 | SkipWhile | 2 |
| Cast | 1 | LastOrDefault | 2 | Sum | 20 |
| Concat | 1 | LongCount | 2 | Take | 1 |
| Contains | 2 | Max | 22 | TakeWhile | 2 |
| Count | 2 | Min | 22 | ThenBy | 2 |
| DefaultIfEmpty | 2 | OfType | 1 | ThenByDescending | 2 |
| Distinct | 2 | OrderBy | 2 | ToArray | 1 |
| ElementAt | 1 | OrderByDescending | 2 | ToDictionary | 4 |
| ElementAtOrDefault | 1 | Range | 1 | ToList | 1 |
| Empty | 1 | Repeat | 1 | ToLookup | 4 |
| Except | 2 | Reverse | 1 | Union | 2 |
| First | 2 | Select | 2 | Where | 2 |
| FirstOrDefault | 2 | SelectMany | 4 | Zip | 1 |

We discuss the query operator methods in more detail in the section, “Standard Query Operators,” later in this chapter. First, let’s get a feeling for how they are implemented in a way that makes them lazily executed.

## Extension Methods Philosophy

Extension methods are not just a way to extend existing interfaces with new members (for example, because they were omitted when the interface was created). They provide a whole new dimension to API design by themselves.

Because the CLR doesn’t provide a means to have nonvirtual methods on interfaces, it becomes hard to expose common, centrally implemented functionality through an interface. One way to stick default methods on a “contract” is by using abstract classes instead. That works but is often undesirable because of the CLR’s single inheritance model. You don’t want to sacrifice your single base class just because you want to inherit some convenience methods that come with something that should have been an interface. Querying functionality could be exposed like this:

```csharp
abstract class QueryableEnumerable<T> : IEnumerable<T> {
    ...
    public QueryableEnumerable<R> Select<T, R>(Func<T, R> selector) {
        /* common implementation */
    }

    public IEnumerable<T> Where<T>(Func<T, bool> predicate) {
        /* common implementation */
    }

    ...

    abstract IEnumerable<T> GetEnumerator();
}
```

Now if you want to make existing collections queryable, you would have to make them inherit from this new base type. Not only is this tedious, it’s often impossible because they already have a base class for other legitimate reasons.

Extension methods effectively provide a means to layer default behavior on top of an interface without changing it or having to rely on abstract base classes. Also, the fact they can be imported through a namespace allows logical grouping of the orthogonal interface features (for example, querying, serialization, and so forth). Although the interface itself stays clean and simple, you can add centrally implemented functionality just by importing an additional namespace.

## Iterators

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1003_0.png)

As a precursor to the LINQ feature set, C# 2.0 introduced the concept of iterators to make the definition of `IEnumerable<T>` and `IEnumerator<T>` objects easier. You’ve seen before how powerful custom implementations of those interfaces can be (for example, to yield a sequence of numbers to a consumer, on an on-demand basis). All you need to do is respond properly to the `MoveNext` method and `Current` property getter calls.

Conceptually though, your task is even simpler: You just want to hand out objects to a consumer when asked to do so. This feels quite a bit like returning data from a method, the difference being you don’t just return a single object but a sequence of objects, one at a time.

Iterators precisely enable you to do this, using regular familiar control flow primitives. You just write a method from which you can produce multiple objects, which gets translated into an implementation of `IEnumerable<T>`. When the user calls `MoveNext` on the iterator, either directly or through the `foreach` loop, code inside it ticks until the next object is given back to the consumer.

An iterator is simply declared as a regular method, returning either `IEnumerable<T>` or `IEnumerator<T>` as indicated in its signature. However, instead of using the regular `return` keyword, one uses the `yield return` keyword. Our handcrafted Integers example can be rewritten using an iterator as follows:

```csharp
public IEnumerable<int> GetIntegers() {
    int n = 0;
    while (true)
        yield return n++;
}
```

The execution model of an iterator is intrinsically lazy. Just calling the `GetIntegers` method returns an object that offers the potential to enumerate the data produced by the iterator. It’s not until you start pulling data out of the iterator object by making calls to the `MoveNext` method and `Current` property that any code inside the iterator starts to execute. This can be visualized nicely under a debugger, as shown in Figure 20.3.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1004_0.png)

FIGURE 20.3 An iterator executes piecemeal when someone enumerates over it.

If you simply step through the `Main` method, you won’t see the breakpoint (or any other code) in the `GetIntegers` iterator getting triggered before the `foreach` loop starts to pull data out of the iterator.

For every call to `MoveNext`, the code in the iterator runs until the next `yield return` statement is encountered. The expression to the right of the `yield return` keywords gets computed and surfaced to the consumer through the `Current` property generated for the `IEnumerator<T>` interface implementation. In this particular case, the iterator has an infinite characteristic, never reaching the end of the iterator block. The compiler comes to this conclusion itself by means of flow analysis (“can the iterator ever reach the end of the block?”), resulting in a `MoveNext` method that always returns `true` to the caller.

To make this more digestible, we’ll write a simpler iterator and analyze how it executes and gets turned into executable code by the compiler. Consider the following fragment:

```csharp
public IEnumerable<int> CountDown() {
    yield return 3;
    yield return 2;
    yield return 1;
    yield return 0;
}
```
