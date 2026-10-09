As indicated, the `Playlist` type contains a list of `Songs` as a private member field.

```
private readonly List<Song> list; .
```

Note that we also mark it as `readonly`. As a general rule, you should always *try to make your internal data readonly or immutable by default, unless it is required otherwise. In the modern multi-threaded, multi-processed runtime environments, dealing with mutable data is much more complicated. (Clearly, it is not always possible to make all data immutable, however.)*

Declaring the variables of a collection type as `readonly` provides only limited protection. For example, even though the variable `list` is `readonly` and cannot be changed, one can easily *change its elements*.

In fact, this is true for all reference types. The language constructs like `readonly` only provides protection for the variable itself. But, for reference type variables, we mostly do not care about the reference values. We primarily care about the values that they reference. But, C# has no fundamental support at the language level to make the underlying data immutable that the references point to. (This is not only for C# but in general for all C-style languages.)

This is one of the reasons why the (immutable) values, and the value types, might be preferred over the references, and the reference types, in many situations.