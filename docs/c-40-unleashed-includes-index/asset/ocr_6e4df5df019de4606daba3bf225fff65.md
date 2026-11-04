How about implementing this interface? Different possibilities exist, one of which is to carry on the type parameter to the implementing type, which will become generic by itself in that case. List<T> is a good example because it implements IEnumerable<T>:

```
public class List<T> : ..., IEnumerable<T> {
    ...
}
```

Notice that the choice of the name for a type parameter is not tied to the declaring type. For example, when implementing to IEnumerable<T>, you are not required to use T as the name for the type parameter on the implementing type. In other words, at the use site, you can choose a different name:

```
public class List<TElement> : ..., IEnumerable<TElement> {
    ...
}
```

In fact, Visual Studio will show you the mapping between the type parameter names at the declaration site and use site. Figure 15.8 shows IntelliSense revealing parameter names and their mapping.

![](bbox=[0.15, 0.73, 0.85, 0.82])

FIGURE 15.8 Naming of type parameters is flexible.

Instead of propagating type parameters, you can also implement a generic interface by supplying any of its type parameters:

```
class Numbers : IEnumerable<int> {
    public IEnumerator<int> GetEnumerator() {
        ...
    }
    ...
}
```

Because a type parameter can be substituted for any type (though, as you see later, this can be restricted by use of constraints), it can be filled in with a generic type by itself, too. A good example is found on IDictionary<TKey, TValue>, a generic interface of arity two, meaning it has two type parameters: