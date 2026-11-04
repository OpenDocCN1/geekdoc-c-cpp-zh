```
public string Name { get; private set; }
public int Age { get; private set; }

public int CompareTo(Person other) {
    return this.Age - other.Age;
}
}
```

# A DIFFERENT LOOK AT ORDERING

Our SortedList<T> follows the ordering semantics implemented on T by means of an IComparable<T> implementation. For types like Person, it's highly unlikely to see an implementation of IComparable<T> because it would require to "prefer" a certain ordering key over another. In the preceding example, we chose the Age property for the natural order of Person objects, but there isn't really a "natural" ordering defined here. IComparable<T> usually makes much more sense for value types.

With LINQ, as you'll see in Chapter 19, "Language Integrated Query Essentials," query operators will be layered on top of IEnumerable<T>, allowing arbitrary ordering keys to be specified by the user, rather than the person who implemented (or forgot to do so) the IComparable<T> interface on the objects in the collection to be sorted.

As you've seen in this example, the use of interfaces as constraints on type parameters is a very useful feature. Once more, I want to emphasize the importance of the IL-level representation because it provides the essential glue required to work with generic types across multiple languages, without losing any of its expressive power. After all, if you define a constrained generic type, you don't want users of any language in the .NET arsenal to be able to violate that constraint. So let's see how the generic type carries along its constraints by looking in ILDASM in Figure 15.18.

![](bbox=[0.1, 0.82, 0.6, 0.96])

FIGURE 15.18 Generic constraints survive in IL, making them work cross-language.