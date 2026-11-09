> **Note** Variance applies only if the compiler can verify that a reference conversion exists between types. In other words, variance is not possible for value types because boxing would be required. In my opinion, this restriction is what makes these variance features not that useful. For example, if I have the following method:
> 
>     void ProcessCollection(IEnumerable<Object> collection) { ... }
> 
> I can’t call it passing in a reference to a `List<DateTime>` object since a reference conversion doesn’t exist between the `DateTime` value type and `Object` even though `DateTime` is derived from `Object`. You solve this problem by declaring `ProcessCollection` as follows:
> 
>     void ProcessCollection<T>(IEnumerable<T> collection) { ... }
> 
> Plus, the big benefit of `ProcessCollection(IEnumerable<Object> collection)` is that there is only one version of the JITted code. However, with `ProcessCollection<T>(IEnumerable<T> collection)`, there is also only one version of the JITted code shared by all Ts that are reference types. You do get other versions of JITted code for Ts that are value types, but now you can at least call the method passing it a collection of value types.
> 
> Also, variance is not allowed on a generic type parameter if an argument of that type is passed to a method using the `out` or `ref` keyword. For example, the line of code below causes the compiler to generate the following error message: 'Invalid variance: The type parameter 'T' must be invariantly valid on 'SomeDelegate<T>.Invoke(ref T)'. 'T' is contravariant.'
> 
>     delegate void SomeDelegate<T>(ref T t);

When using delegates that take generic arguments and return values, it is recommended to always specify the `in` and `out` keywords for contravariance and covariance whenever possible, as doing this has no ill effects and enables your delegate to be used in more scenarios.

Like delegates, an interface with generic type parameters can have its type parameters be contravariant or covariant. Here is an example of an interface with a contravariant generic type parameter:

```
    public interface IEnumerator<out T> : IEnumerator {
        Boolean MoveNext();
        T Current { get; }
    }
```

Since `T` is contravariant, it is possible to have the following code compile and run successfully:

```
    // This method accepts an IEnumerable of any reference type
    Int32 Count(IEnumerable<Object> collection) { ... }

    ...

    // The call below passes an IEnumerable<String> to Count
    Int32 c = Count(new[] { "Grant" });
```