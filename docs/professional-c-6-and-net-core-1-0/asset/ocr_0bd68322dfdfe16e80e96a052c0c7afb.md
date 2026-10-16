```
theInstance?.Dispose();
}
```

# The using Statement

Using `try/finally` ensures that `Dispose` is always called on `theInstance` and that any resources consumed by it are always freed, even if an exception occurs during processing. However, if you always had to repeat such a construct, it would result in confusing code. C# offers a syntax that you can use to guarantee that `Dispose` is automatically called against an object that implements `IDisposable` when its reference goes out of scope. The syntax to do this involves the `using` keyword—though now in a very different context, which has nothing to do with namespaces. The following code generates IL code equivalent to the `try` block just shown:

```
using (var theInstance = new ResourceGobbler())
{
    // do your processing
}
```

The `using` statement, followed in brackets by a reference variable declaration and instantiation, causes that variable to be scoped to the accompanying statement block. In addition, when that variable goes out of scope, its `Dispose` method is called automatically, even if an exception occurs.

> **NOTE** *The `using` keyword has multiple uses with C#. The `using` declaration is used to import namespaces. The `using` statement works with objects implementing `IDisposable` and invokes the `Dispose` method with the end of the using scope.*

> **NOTE** *With several classes of the .NET Framework both a `Close` and a `Dispose` method exists. If it is common to close a resource (such as a file and a database), both `Close` and `Dispose` have been implemented. Here, the `Close` method simply calls `Dispose`. This approach provides clarity in the use of these classes and supports the `using` statement. Newer classes only implement the `Dispose` method as we’re already used to it.*

# Implementing IDisposable and a Destructor

The previous sections discussed two alternatives for freeing unmanaged resources used by the classes you create:

+   - The execution of a destructor is enforced by the runtime but is nondeterministic and places an unacceptable overhead on the runtime because of the way garbage collection works.