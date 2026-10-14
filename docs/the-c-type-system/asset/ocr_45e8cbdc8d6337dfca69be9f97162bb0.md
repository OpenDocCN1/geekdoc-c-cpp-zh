```
private readonly int idx;
private readonly T contained;
}
```

*Listing 2-26: Initializing a default instance of a type parameter*

In the Node constructor, the contained field is assigned the default value of its type by using the target-typed default literal (available since C# v7.1), which is equivalent to the expression default(T). Where T is a class or record, its default value is null, and where T is a struct or record struct, the default value is a default-initialized instance. Note that initializing a value by using default does not invoke a parameterless constructor, if we have defined one. This code is valid because we can always create a default value for a variable of type T: if T is a value type, the value is a default instance of T, and if T is a reference type, a default T is null. The default keyword has many uses outside of generic types and methods, but within generic code it’s indispensable.

Default values are useful, but they’re not sufficient to identify a particular value type instance as invalid. In other words, we can’t use a default when what we really mean is *no value present*. The default value of a struct or record struct is a default-initialized instance and might therefore be a *valid* value. Consider Listing 2-27.

```
int x = default;
int y = 0;

Assert.That(x.Equals(y), Is.True);
```

*Listing 2-27: Default values can be valid.*

The default value for an int type is 0, which we may use to indicate an invalid number in some circumstances but not all. Whether that matters, especially for our own value types, depends on the context in which instances of the type are used, but limiting valid integers to only nonzero values would be very restrictive. Fortunately, we have an alternative.

# Nullable Value Types

*Nullable value types* allow us to have a representation of a value type that means *no value present*. A nullable value type is a wrapper around a value type, and a nullable value type variable may or may not have a value. A nullable value type variable can also be assigned the value null, demonstrated by using a simple test in Listing 2-28.

```
int? x = null;
int y = 0;

Assert.That(x.Equals(y), Is.False);
```

*Listing 2-28: Using nullable values*