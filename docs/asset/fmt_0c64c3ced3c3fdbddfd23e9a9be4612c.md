
Our `Color` struct is a relatively simple data type, and its `Equals` method is already quite efficient. To probe the characteristics of `Equals`, we’ll make a much more complex `Purchase` value type, shown in Listing 8-7. The `Purchase` struct overrides both `Equals` and `GetHashCode` with custom implementations but doesn’t yet implement the `IEquatable<Purchase>` interface. We’ll implement that interface for `Purchase` later to see how that affects the performance of `Equals`.

```
public readonly struct Purchase
{
    public Purchase(Product item, DateTime ordered, int quantity)
        => (Item, Ordered, Quantity) = (item, ordered, quantity);

    public Product  Item { get; }
    public DateTime Ordered { get; }
    public int      Quantity { get; }

    public override bool Equals(object? obj)
        => obj is Purchase other &&
           Item.Equals(other.Item) &&
           Ordered == other.Ordered && Quantity == other.Quantity;

    public override int GetHashCode()
        => HashCode.Combine(Item, Ordered, Quantity);
}
```

Listing 8-7: Defining a more complex data type, `Purchase`

The `Purchase` type has three fields, one of which is another nontrivial type named `Product`, shown here:

```
public readonly struct Product
{
    public Product(int id, decimal price, string name)
        => (Id, Price, Name) = (id, price, name);

    public int      Id { get; }
    public decimal  Price { get; }
    public string   Name { get; }
}
```

```
public override bool Equals(object? obj)
    => obj is Product other &&
        Id == other.Id && Price == other.Price && Name == other.Name;

public override int GetHashCode()
        => HashCode.Combine(Id, Price, Name);
}
```

The `Equals` method of `Purchase` needs to do a little more work than the `Equals` method for the `Color` type back in Listing 8-5. When we compare two `Purchase` instances for equality, the `Equals` method must also ensure that the `Item` properties match, which involves a method call to `Product.Equals`.

**NOTE**

> The `Purchase` type is quite large—40 bytes plus padding, assuming a 64-bit architecture—so we should expect copying instances around to be less efficient than for the smaller `Color` type. That won’t affect our profiling, though, as we’ll still be comparing reports for the same types. We’ll return to the cost of copying large struct instances in “Copying Large Instances” on page 272.

Instead of a `HashSet`, we’ll use the `SequenceEqual` method to compare two very large lists of `Purchase` objects, as shown in Listing 8-8. This process will exercise the `Equals` method, allowing us to measure its efficiency. To magnify the performance of `Equals` compared to the cost of the surrounding code, we increase the number of elements to 10 million.

```
var items = Enumerable.Range(0, 10_000_000)
    .Select(id => new Purchase(new Product(id, id, "Some Description"),
                DateTime.MinValue, id))
    .ToList();

Assert.That(items.SequenceEqual(items), Is.True);
```

Listing 8-8: Testing to exercise equality

In the `Enumerable.Range` method, we use digit separators, available since C# v7.0, to make the large literal number easy for human readers to parse. Digit separators make no difference to the compiler: the number we use for the length of the initial sequence is still a plain `int` value.

The `SequenceEqual` method compares two sequences and returns true if they have the same elements in the same order. The algorithm obtains an element from each sequence and compares those elements by using the `Equals` method. `SequenceEqual` doesn’t try to optimize its result by checking if the two sequences are in fact the same sequence, so here we create only one sequence of 10 million elements and compare it with itself. Table 8-7 shows the profiler report for the call to `SequenceEqual`.

**Table 8-7: Exercising the Equals Method**

| Method | Time (ms) | Signature |
|---|---|---|
| 77.5% `SequenceEqual` | 1,227 | `System.Linq.Enumerable.SequenceEqual(IEnumerable, IEnumerable)` |
| 49.3% `Equals` | 781 | `Purchase.Equals(Object)` |
| 24.3% [Garbage collection] | 384 |  |
| 10.6% `Equals` | 168 | `Product.Equals(Object)` |
| 0.75% `get_Item` | 12 | `Purchase.get_Item()` |
| 0.38% `Unbox` | 6.0 | `System.Runtime.CompilerServices.CastHelpers.Unbox(Void*, Object)` |

We can see that garbage collection contributes a significant portion of the time required by `Equals`. Each call to `Equals` with a `Purchase` instance results in the argument being boxed, as `Purchase` is a struct and the parameter type of the `Equals` override is `object`, a reference type. Furthermore, the `Purchase.Equals` method calls `Product.Equals`, which also requires its argument to be boxed. The consequence is that we’re allocating many boxed objects on the heap, placing the garbage collector under fairly significant pressure to keep memory usage under control.

In each `Equals` method, the parameter needs to be unboxed back to its original type so that its properties can be compared; the cost of unboxing the object parameter for each of the `Equals` methods is tiny but has a measurable impact. We can avoid the costs of boxing, and much of the associated cost of garbage collection, by implementing `IEquatable<T>` for both `Purchase` and `Product` types.

## The Effect of `IEquatable<T>`

The `SequenceEqual` method automatically selects the best (the most efficient) implementation of `Equals` available to perform the comparisons. Internally, `SequenceEqual` uses the `EqualityComparer` helper class from Chapter 5 to determine how to compare elements. If the element type `T` implements `IEquatable<T>`, it’s guaranteed to implement a type-safe overload of `Equals`, and that overload will be called by `SequenceEqual`.

If we implement the `IEquatable<Purchase>` interface and provide our own type-safe overload of `Equals`, the `SequenceEqual` method will use the `IEquatable<Purchase>` interface method by default, avoiding the need for boxing and then unboxing the argument to `Equals`. In turn, this reduces memory pressure because the arguments aren’t copied to the heap, resulting in fewer objects for the garbage collector to inspect. In our example, those reductions are considerable, so implementing the `IEquatable<Purchase>` interface should produce a measurable benefit. Listing 8-9 shows the changes required in `Purchase`.

```
public readonly struct Purchase : IEquatable<Purchase>
{
    --snip--

    public bool Equals(Purchase other)
        => Item.Equals(other.Item) &&
           Ordered == other.Ordered && Quantity == other.Quantity;

    public override bool Equals(object? obj)
        => obj is Purchase other && Equals(other);
}
```

Listing 8-9: The `IEquatable<Purchase>` implementation

We’ve added an `Equals(Purchase other)` overload to perform the comparisons between each of the property values. The original `Equals` override still needs to unbox its object parameter in order to call the type-safe `Equals` overload, but the `SequenceEqual` method won’t call `Equals(object?)` because we’ve also changed the `Purchase` declaration to implement the `IEquatable<Purchase>` interface. In Listing 8-10, we make similar changes in `Product` so that calling `Product.Equals` from the `Purchase.Equals` method won’t require boxing the `Product` instance.

```
public readonly struct Product : IEquatable<Product>
{
    --snip--

    public bool Equals(Product other)
        => Id == other.Id && Price == other.Price && Name == other.Name;

    public override bool Equals(object? obj)
        => obj is Product other && Equals(other);
}
```

Listing 8-10: Implementing `IEquatable<Product>`

The results of the test from Listing 8-8, incorporating the changes from Listings 8-9 and 8-10, still with 10 million `Purchase` elements, are shown in Table 8-8.

**Table 8-8: Measuring the Type-Safe Equals Method**

| Method | Time (ms) | Signature |
|---|---|---|
| 62.6% `SequenceEqual` | 546 | `System.Linq.Enumerable.SequenceEqual(IEnumerable, IEnumerable)` |
| 13.0% `Equals` | 114 | `Purchase.Equals(Purchase)` |
| 5.48% `Equals` | 48 | `Product.Equals(Product)` |
