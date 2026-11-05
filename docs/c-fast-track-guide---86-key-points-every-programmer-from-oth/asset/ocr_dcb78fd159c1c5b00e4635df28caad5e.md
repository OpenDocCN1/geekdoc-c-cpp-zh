The using statement in C# works with types that implement the IDisposable interface. These are objects that often hold on to system resources (like file handles, network connections, or database sessions). When the code execution leaves the using block—whether normally or because of an exception—C# automatically calls the .Dispose() method on the object.

This helps prevent resource leaks—situations where you forget to manually close files or connections, which can cause bugs or even crash programs in real-world applications.

Even though you can call .Dispose() manually, it's safer and cleaner to let using handle it for you.

As of C# 8.0, you can also use using declarations for shorter syntax:

```
```csharp
using var reader = new StreamReader("example.txt");
Console.WriteLine(reader.ReadToEnd());
```
```

The file will still be disposed at the end of the method.

# [Supplement]

using can nest, so you can manage multiple resources at once.

Any object that implements IDisposable can be used in a using block.

If you forget to use using, you must manually call .Dispose() or risk memory/resource leaks.

This pattern is known as RAII in C++ or try-with-resources in Java.

The compiler turns using blocks into a try-finally under the hood for safe disposal.