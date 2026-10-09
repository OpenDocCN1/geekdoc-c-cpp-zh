implements, which requires "boxing" and "unboxing". More on this later.

As stated earlier, we can only use the polymorphic behavior for reference types since the polymorphism requires some kind of "indirection", and a reference, by definition, "points to" its underlying data, which is a one-level indirection.

![](bbox=[0.1, 0.24, 0.15, 0.28])

This is a lot to take in, if you are new to C#. But, these "rules" will seem natural after getting some experiences in programming in C#. You do not have to "memorize" them at this point.

The (ultimate) base type, System.Object, defines the following three virtual methods, among other things,

```
public virtual bool Equals (object? obj);
public virtual int GetHashCode ();
public virtual string? ToString ();
```

These methods are defined, and available, in all types, whether builtin or user-defined, since every single type in .NET inherits from System.Object, or object in C#. In other words, these "behaviors" are included in all types in C#/.NET.

Note that these three methods are declared as virtual (but, not as abstract), indicating that they provide certain default implementations, which may or may not be entirely appropriate for the particular derived types.

System.ValueType "overrides" the following two methods, among other things, to provide a value type with the default "value semantics".

This is done using the override modifier in C#.

```
public override bool Equals (object? obj);
public override int GetHashCode ();
```