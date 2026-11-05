# Chapter 43: Singleton Implementation

# Section 43.1: Statically Initialized Singleton

```
public class Singleton
{
    private readonly static Singleton instance = new Singleton();
    private Singleton() { }
    public static Singleton Instance => instance;
}
```

This implementation is thread-safe because in this case instance object is initialized in the static constructor. The CLR already ensures that all static constructors are executed thread-safe.

Mutating instance is not a thread-safe operation, therefore the readonly attribute guarantees immutability after initialization.

# Section 43.2: Lazy, thread-safe Singleton (using Lazy<T>)

.Net 4.0 type Lazy guarantees thread-safe object initialization, so this type could be used to make Singletons.

```
public class LazySingleton
{
    private static readonly Lazy<LazySingleton> _instance =
        new Lazy<LazySingleton>(() => new LazySingleton());

    public static LazySingleton Instance
    {
        get { return _instance.Value; }
    }

    private LazySingleton() { }
}
```

Using Lazy<T> will make sure that the object is only instantiated when it is used somewhere in the calling code.

A simple usage will be like:

```
using System;

public class Program
{
    public static void Main()
    {
        var instance = LazySingleton.Instance;
    }
}
```

Live Demo on .NET Fiddle

# Section 43.3: Lazy, thread-safe Singleton (using Double Checked Locking)

This thread-safe version of a singleton was necessary in the early versions of .NET where static initialization was not guaranteed to be thread-safe. In more modern versions of the framework a statically initialized singleton is