```
public override bool Equals(object? obj)
    => obj is Product other &&
        Id == other.Id && Price == other.Price && Name == other.Name;

public override int GetHashCode()
    => HashCode.Combine(Id, Price, Name);
}
```

The Equals method of Purchase needs to do a little more work than the Equals method for the Color type back in Listing 8-5. When we compare two Purchase instances for equality, the Equals method must also ensure that the Item properties match, which involves a method call to Product.Equals.

NOTE

> The Purchase type is quite large—40 bytes plus padding, assuming a 64-bit architecture—so we should expect copying instances around to be less efficient than for the smaller Color type. That won’t affect our profiling, though, as we’ll still be comparing reports for the same types. We’ll return to the cost of copying large struct instances in “Copying Large Instances” on page 272.

Instead of a HashSet, we’ll use the SequenceEqual method to compare two very large lists of Purchase objects, as shown in Listing 8-8. This process will exercise the Equals method, allowing us to measure its efficiency. To magnify the performance of Equals compared to the cost of the surrounding code, we increase the number of elements to 10 million.

```
var items = Enumerable.Range(0, 10_000_000)
    .Select(id => new Purchase(new Product(id, id, "Some Description"),
                DateTime.MinValue, id))
    .ToList();

Assert.That(items.SequenceEqual(items), Is.True);
```

Listing 8-8: Testing to exercise equality

In the Enumerable.Range method, we use digit separators, available since C# v7.0, to make the large literal number easy for human readers to parse. Digit separators make no difference to the compiler: the number we use for the length of the initial sequence is still a plain int value.

The SequenceEqual method compares two sequences and returns true if they have the same elements in the same order. The algorithm obtains an element from each sequence and compares those elements by using the Equals method. SequenceEqual doesn’t try to optimize its result by checking if the two sequences are in fact the same sequence, so here we create only one sequence of 10 million elements and compare it with itself. Table 8-7 shows the profiler report for the call to SequenceEqual.