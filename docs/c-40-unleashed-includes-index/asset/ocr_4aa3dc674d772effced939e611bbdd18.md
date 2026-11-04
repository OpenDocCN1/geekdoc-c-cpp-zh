```
}
public IEnumerable<T> Where<T>(Func<T, bool> predicate) {
    /* common implementation */
}
...
abstract IEnumerable<T> GetEnumerator();
}
```

Now if you want to make existing collections queryable, you would have to make them inherit from this new base type. Not only is this tedious, it's often impossible because they already have a base class for other legitimate reasons.

Extension methods effectively provide a means to layer default behavior on top of an interface without changing it or having to rely on abstract base classes. Also, the fact they can be imported through a namespace allows logical grouping of the orthogonal interface features (for example, querying, serialization, and so forth). Although the interface itself stays clean and simple, you can add centrally implemented functionality just by importing an additional namespace.

# Iterators

![](bbox=[0.1, 0.62, 0.17, 0.7])

As a precursor to the LINQ feature set, C# 2.0 introduced the concept of iterators to make the definition of IEnumerable<T> and IEnumerator<T> objects easier. You've seen before how powerful custom implementations of those interfaces can be (for example, to yield a sequence of numbers to a consumer, in an on-demand basis). All you need to do is respond properly to MoveNext method and Current property getter calls.

Conceptually though, your task is even simpler: You just want to hand out objects to a consumer when asked to do so. This feels quite a bit like returning data from a method, the difference being you don't just return a single object but a sequence of objects, one at a time.

Iterators precisely enable you to do this, using regular familiar control flow primitives. You just write a method from which you can produce multiple objects, which gets translated into an implementation of IEnumerable<T>. When the user calls MoveNext on the iterator, either directly or through the foreach loop, code inside it ticks until the next object is given back to the consumer.

An iterator is simply declared as a regular method, returning either IEnumerable<T> or IEnumerator<T> as indicated in its signature. However, instead of using the regular return keyword, one uses the yield return keyword. Our handcrafted Integers example can be rewritten using an iterator as follows:

```
public IEnumerable<int> GetIntegers() {
    int n = 0;
    while (true)
        yield return n++;
}
```