a passing familiarity for the language and its idioms. Listing 8-23 shows an example of using the fluent syntax to create a list of Purchase objects.

```
private static Purchase MakePurchase(int id)
    => new Purchase(new Product(id, id, "Some Description"),
        DateTime.MinValue, id);

var items = Enumerable.Range(0, count)
    .Select(i => MakePurchase(i))
    .ToList();
```

Listing 8-23: LINQ fluent syntax

LINQ has an alternative query syntax that some C# programmers find more agreeable. Listing 8-24 shows the equivalent query syntax for creating the items sequence in Listing 8-23.

```
var query = from i in Enumerable.Range(0, count)
    select MakePurchase(i);

var items = query.ToList();
```

Listing 8-24: LINQ query syntax

The compiler generates identical CIL for both Listings 8-23 and 8-24, so the choice between them is primarily driven by which we find clearer to read. One optimization is possible, although it can be applied only to the fluent version: avoiding the lambda as an argument to the Select method. That lambda needs to capture the i variable so the compiler will generate a closure object, which results in an extra level of indirection to call the MakePurchase method. To avoid the closure, we can instead pass MakePurchase as a method group argument, as shown in Listing 8-25.

```
var items = Enumerable.Range(0, count)
    .Select(MakePurchase)
    .ToList();
```

Listing 8-25: Optimizing LINQ by using a method group

To compare the efficiency of each approach, first we profile the version from Listing 8-23, which uses a lambda. Table 8-22 shows the report for creating a list of 10 million items.

# Table 8-22: Performance of Creating a Sequence Using LINQ with a Lambda

| Method | Time (ms) | Signature |
|---|---|---|
| 98.1% ToList | 415 | System.Linq.Enumerable .ToList(IEnumerable) |
| 36.0% MakePurchase | 152 | MakePurchase(Int32) |
| 31.3% <Closure> b__3_0 | 132 | <>c.<Closure> b__3_0(Int32) |
| 31.3% MakePurchase | 132 | MakePurchase(Int32) |