# Weighing Object Construction Costs

The cost of copying a large struct is not the only aspect to consider when using a type with several fields. For one thing, equality comparisons will usually take every field or property into account, making those comparisons more costly than for a type with only one or two fields. Initializing an instance of a type with several fields also comes with a cost.

The Purchase and Product types in Listing 8-18 are the positional record struct equivalents of the Purchase and Product structs we defined earlier in Listing 8-7. Because they’re record struct types, the compiler generates all the equality comparisons, making them much simpler to define than their struct counterparts.

```
public readonly record struct Product
    (int Id, decimal Price, string Name);

public readonly record struct Purchase
    (Product Item, DateTime Ordered, int Quantity);
```

Listing 8-18: Defining Product and Purchase as record structs

We’ll use the CompareSequences method shown in Listing 8-19 to create a sequence of Purchase instances and record the performance. We return here to profiling a release build so that the results account for any optimizations afforded by the JIT (or AOT) compiler.

```
private static Purchase MakePurchase(int id)
    => new Purchase(new Product(id, id, "Some Description"),
        DateTime.MinValue, id);

public static void CompareSequences(int count)
{
    var items = Enumerable.Range(0, count)
        .Select(MakePurchase)
        .ToList();

    Assert.That(items.SequenceEqual(items));
}
```

Listing 8-19: Creating a sequence of randomly generated objects

The CompareSequences method follows a pattern similar to that we’ve used previously to create a sequence and then call SequenceEqual to compare the elements. For the purposes of making the performance report clear, we use MakePurchase as a method group argument for the Select expression. That way, we can measure its performance directly, without introducing any overhead by using a lambda expression—something we’ll return to in “How Common Idioms and Practices Affect Performance” on page 279. Table 8-15 shows the profiler report for creating 10 million Purchase objects using the MakePurchase method.