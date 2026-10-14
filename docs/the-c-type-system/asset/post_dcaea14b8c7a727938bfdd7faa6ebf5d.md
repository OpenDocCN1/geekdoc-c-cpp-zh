
**Table 8-9: Comparing the Performance of Fields vs. Properties**

| % | Method | Time (ms) | Signature |
|---|---|---|---|
| 51.2% | SequenceEqual | 442 | System.Linq.Enumerable.SequenceEqual(IEnumerable, IEnumerable) |
| 9.73% | Equals | 84 | Purchase.Equals(Purchase) |
| 3.47% | Equals | 30 | Product.Equals(Product) |
| 1.41% | op_Equality | 12 | System.DateTime.op_Equality(DateTime, DateTime) |

Although replacing automatic properties with fields shows a small improvement, it’s an example of a micro-optimization. We’ve cut the time needed for SequenceEqual by more than half compared to the version that didn’t implement IEquatable<Purchase>, but we’re still talking about only a few hundred milliseconds in absolute time. We had to dramatically increase the size of the sequence to amplify the results enough to be observable, and most applications don’t routinely need to compare lists of 10 million elements.

Implementing the IEquatable<T> interface is a much more important step. Not only do we benefit from an increase in speed, but our type makes much more efficient use of memory by not needing to box the argument to Equals. Implementing IEquatable<T> for value types is more than a performance optimization; it establishes that our type follows that protocol, enabling certain library features to operate more efficiently and signaling efficiency to human readers too.

## The Equality Operators

The final part of implementing a full set of equality comparisons for a type is to write our own operator== with its companion operator!=. Listing 8-12 shows those operators implemented for Purchase.

```
public readonly struct Purchase : IEquatable<Purchase>
{
    --snip--

    public bool Equals(Purchase other)
        => item == other.item &&
           ordered == other.ordered && quantity == other.quantity;

    public static bool operator==(Purchase left, Purchase right)
        => left.Equals(right);

    public static bool operator!=(Purchase left, Purchase right)
        => !left.Equals(right);
}
```

Listing 8-12: Implementing equality operators for Purchase

Again, we also add equality operators to the Product type (not shown), allowing us to compare the item field in Purchase by using == instead of calling its Equals method. Each operator implementation simply forwards to our type-safe Equals method, where the comparison is performed.

While we can write a test to call operator== in order to measure its performance characteristics, we can also arrange for the SequenceEqual method to call the operator rather than Equals by providing our own equality comparer.

## The Generic IEqualityComparer<T> Interface

The SequenceEqual method doesn’t invoke Equals directly on the sequence elements to compare them. Instead, it relies on an implementation of IEqualityComparer<T>, which is part of the Standard Library and declared in the System.Collections.Generic namespace.

An implementation of IEqualityComparer<T> requires an Equals method taking two parameters of type T, and a GetHashCode method with a single T parameter. The Standard Library provides some default implementations of IEqualityComparer<T>, including one for instances of T that implement the IEquatable<T> interface, which is what our uses of SequenceEqual have relied upon thus far.

The SequenceEqual method has an overload that takes a second parameter whose type is IEqualityComparer<T>, so we can provide our own implementation to be used instead of the default comparer. In Listing 8-13, we create our own implementation of the IEqualityComparer<T> interface, substituting Purchase as the generic parameter, and pass an instance of our custom comparer to SequenceEqual.

```
public sealed class EqualsOperatorComparer : IEqualityComparer<Purchase>
{
    public bool Equals(Purchase x, Purchase y)
        => x == y;

    public int GetHashCode(Purchase obj)
        => obj.GetHashCode();
}

var items = Enumerable.Range(0, 10_000_000)
    .Select(MakePurchase)
    .ToList();

Assert.That(items.SequenceEqual(items, new EqualsOperatorComparer()));
```

Listing 8-13: Creating a custom IEqualityComparer<T> implementation

Our implementation of IEqualityComparer<Purchase> defines its Equals method to compare its two parameter values with == instead of the parameter type’s Equals method. We don’t need a separate implementation for Product because the Equals member method in Purchase uses == directly to compare the Product values. Now, when we use SequenceEqual to compare two sequences of Purchase items, the algorithm will use operator== for the comparisons. Table 8-10 shows the profiler report for comparing 10 million Purchase items.

**Table 8-10: How operator== Performs**

| % | Method | Time (ms) | Signature |
|---|---|---|---|
| 48.8% | SequenceEqual | 475 | System.Linq.Enumerable.SequenceEqual [...] |
| 22.2% | Equals | 216 | EqualsOperatorComparer.Equals(Purchase, Purchase) |
| 9.28% | op_Equality | 90 | Purchase.op_Equality(Purchase, Purchase) |
| 9.28% | Equals | 90 | Purchase.Equals(Purchase) |
| 5.53% | op_Equality | 54 | Product.op_Equality(Product, Product) |
| 3.69% | Equals | 36 | Product.Equals(Product) |

When we define operator== for any type, the compiler translates it to a static method named op_Equality, shown in this profiler report. That method takes both of its parameters by value, so we're making a lot of copies of both Purchase and Product instances. We can reduce the number of copies needed by changing the operator== methods to take their parameters by reference instead.

## Read-Only in Parameters

To reap the benefits of altering our operator== methods to take their parameters by reference rather than by value, we can use read-only in parameters. They are specifically intended for avoiding copies of large value type instances and are appropriate when we don't need to mutate the parameter variables.

We shouldn't expect a huge improvement, however, because we can't avoid all the copies being made when comparing the Purchase elements in our sequence. In particular, the EqualsOperatorComparer.Equals method must take its parameters by value to match the signature defined in the IEqualityComparer<T> interface.

Similarly, as shown in Listing 8-14, the type-safe Equals method defined in Purchase itself takes its parameter by value according to the IEquatable<T> interface, but we can add a new overload of Equals that uses an in parameter and use the same mechanism to alter the equality operators to take all their parameters by reference.

```
public readonly struct Purchase : IEquatable<Purchase>
{
    --snip--

    public bool Equals(in Purchase other)
        => item == other.item &&
           ordered == other.ordered && quantity == other.quantity;

    public bool Equals(Purchase other)
        => Equals(in other);

    public static bool operator==(in Purchase left, in Purchase right)
        => left.Equals(in right);

    public static bool operator!=(in Purchase left, in Purchase right)
        => !left.Equals(in right);
}
```

Listing 8-14: Overloading using in parameters

We make the Equals method with an in parameter the main implementation and forward to it from the equality operators and the implementation of IEquatable<Purchase>. Although in parameters are transparent to calling code, the rules for overloading will give preference to the method with no parameter modifiers, unless we add an in modifier to the argument when calling the method. Therefore, we explicitly select the overload with in parameters by adding the in keyword to the argument we pass wherever we call Equals.

> NOTE
> *Replacing value parameters with in parameters is a version-breaking change, requiring extra care if binary compatibility is a consideration.*

We don’t need to change the implementation of our EqualsOperatorComparer to pass the arguments by reference, since our operator== method doesn’t have an overload taking parameters by value. We can reuse the EqualsOperatorComparer from Listing 8-13 to run the test, with the results shown in Table 8-11.

**Table 8-11: Results of Passing by Reference to operator==**

| % | Method | Time (ms) | Signature |
|---|---|---|---|
| 45.1% | SequenceEqual | 437 | System.Linq.Enumerable.SequenceEqual [...] |
| 20.9% | Equals | 203 | EqualsOperatorComparer.Equals(Purchase, Purchase) |
| 10.5% | op_Equality | 102 | Purchase.op_Equality(in Purchase, in Purchase) |
| 9.23% | Equals | 90 | Purchase.Equals(in Purchase) |
| 7.38% | op_Equality | 72 | Product.op_Equality(in Product, in Product) |
| 7.38% | Equals | 72 | Product.Equals(in Product) |

Comparing these results to Table 8-10, we can see the improvement is quite modest. While we certainly get some benefit from avoiding copying Purchase objects, that benefit is limited to operator== actually being called. Table 8-12 shows a tracing report with counts of the number of method
