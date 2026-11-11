```
E next();
default void remove() { throw new UnsupportedOperationException("remove"); }
...
}
```

If you implement an iterator, you need to provide the `hasNext` and `next` methods. There are no defaults for these methods—they depend on the data structure that you are traversing. But if your iterator is read-only, you don’t have to worry about the remove method.

A default method can call other methods. For example, a `Collection` interface can define a convenience method

```
public interface Collection
{
    int size(); // an abstract method
    default boolean isEmpty() { return size() == 0; }
    ...
}
```

Then a programmer implementing `Collection` doesn’t have to worry about implementing an `isEmpty` method.

> **NOTE:**
> 
> The Collection interface in the Java API does not actually do this. Instead, there is a class `AbstractCollection` that implements `Collection` and defines `isEmpty` in terms of `size`. Implementors of a collection are advised to extend `AbstractCollection`. That technique is obsolete. Just implement the methods in the interface.

An important use for default methods is *interface evolution*. Consider, for example, the Collection interface that has been a part of Java for many years. Suppose that a long time ago, you provided a class