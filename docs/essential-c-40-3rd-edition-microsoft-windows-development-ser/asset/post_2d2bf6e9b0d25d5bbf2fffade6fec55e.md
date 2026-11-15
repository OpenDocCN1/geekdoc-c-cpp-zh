
the finally block. The using statement, however, provides a syntax shortcut for the try/finally block.

Within a using statement, you can instantiate more than one variable by separating each variable with a comma. The key is that all variables are of the same type and that they implement IDisposable. To enforce the use of the same type, the data type is specified only once rather than before each variable declaration.

## Garbage Collection and Finalization

The IDisposable pattern contains one additional important call. Back in Listing 9.21, the Close() method included a call to System.GC.SuppressFinalize() (captured again in Listing 9.23). Its purpose was to remove the TemporaryFileStream class instance from the finalization (f-reachable) queue.

### LISTING 9.23: Suppressing Finalization

```
// ...
public void Close()
{
    if(Stream != null)
    {
        Stream.Close();
    }
    if(File != null)
    {
        File.Delete();
    }
    // Turn off calling the finalizer
    System.GC.SuppressFinalize(this);
}
// ...
```

The f-reachable queue is a list of all the objects that are ready for garbage collection and that also have finalization implementations. The runtime cannot garbage-collect objects with finalizers until after their finalization methods have been called. However, garbage collection itself does not call the finalization method. Rather, references to finalization objects are added to the f-reachable queue, thereby ironically delaying garbage collection. This is because the f-reachable queue is a list of “references,” and as such, the objects are not garbage until after their finalization methods are called and the object references are removed from the f-reachable queue.

### Language Contrast: C++—Deterministic Destruction

Although finalizers are similar to destructors in C++, the fact that their execution cannot be determined at compile time makes them distinctly different. The garbage collector calls C# finalizers sometimes after they were last used, but before the program shuts down; C++ destructors are automatically called when the object (not a pointer) goes out of scope.

Although running the garbage collector can be a relatively expensive process, the fact that garbage collection is intelligent enough to delay running until process utilization is somewhat reduced offers an advantage over deterministic destructors, which will run at compile-time-defined locations, even when a processor is in high demand.

### ADVANCED TOPIC

### Resurrecting Objects

By the time an object’s finalization method is called, all references to the object have disappeared and the only step before garbage collection is running the finalization code. However, it is possible to add a reference inadvertently for a finalization object back into the root reference’s graph. In so doing, the referenced object is no longer inaccessible, and therefore, it is not ready for garbage collection. However, if the finalization method for the object has already run, it will not necessarily be run again unless it is explicitly marked for finalization (using the GC.ReRegisterForFinalize() method).

Obviously, resurrecting objects like this is peculiar behavior and you should generally avoid it. Finalization code should be simple and should focus on cleaning up only the resources that it references.

## Resource Utilization and Finalization Guidelines

When defining classes that manage resources, you should consider the following.

- 1. Implement Finalize only on objects with resources that are scarce or expensive. Finalization delays garbage collection.
- 2. Objects with finalizers should implement IDisposable to support deterministic finalization.
- 3. Finalization methods generally invoke the same code called by IDisposable, perhaps simply calling the Dispose() method.
- 4. Finalizers should avoid causing any unhandled exceptions.
- 5. Deterministic finalization methods such as Dispose() and Close() should call System.GC.SuppressFinalize() so that garbage collection occurs sooner and resource cleanup is not repeated.
- 6. Code that handles resource cleanup may be invoked multiple times and should therefore be reentrant. (For example, it should be possible to call Close() multiple times.)
- 7. Resource cleanup methods should be simple and should focus on cleaning up resources referenced by the finalization instance only. They should not reference other objects.
- 8. If a base class implements Dispose(), then the derived implementation should call the base implementation.
- 9. Generally, objects should be coded as unusable after Dispose() is called. After an object has been disposed, methods other than Dispose() (which could potentially be called multiple times) should throw an ObjectDisposedException().

## Lazy Initialization

In the preceding section, we discussed how to deterministically dispose of an object with a using statement and how the finalization queue will dispose of resources in the event that no deterministic approach is used.

A related pattern is lazy initialization or lazy loading. Using lazy initialization, you can create (or obtain) objects when you need them rather than beforehand—especially when they were never used. Consider the FileStream property of Listing 9.24.

### LISTING 9.24: Lazy Loading a Property

```
using System.IO;

class DataCache
{
    // ...

    public TemporaryFileStream FileStream
    {
        get
        {
            if (_FileStream == null)
            {
                _FileStream = new TemporaryFileStream();
            }
            return _FileStream;
        }
    }

    private TemporaryFileStream _FileStream = null;

    // ...
}
```

In the FileStream property, we instantiate the TemporaryFileStream object only when the getter on the property is called. If the getter is never invoked, the TemporaryFileStream object would not get instantiated and we would save whatever execution time such an instantiation would cost. Obviously, if the instantiation is negligible or inevitable (and postponing the inevitable is less desirable), then simply assigning it during declaration or in the constructor makes sense. Deferring the initialization of an object until it is required is called lazy initialization.

### ADVANCED TOPIC

### Lazy Loading with Generics and Lambda Expressions

Starting with .NET Framework 4.0, a new class was added to the CLR to assist with lazy initialization: System.Lazy<T>. Listing 9.25 demonstrates how to use it.

### LISTING 9.25: Lazy Loading a Property

```
using System.IO;

class DataCache
{
    // ...

    public string FileStreamName { get; set; }

    public DataCache()
    {
        _FileStream = new Lazy<TemporaryFileStream>(
            () => new TemporaryFileStream(FileStreamName));
    }

    public TemporaryFileStream FileStream
    {
        get
        {
            return _FileStream.Value;
        }
    }

    private Lazy<TemporaryFileStream> _FileStream;

    // ...
}
```

The System.Lazy<T> class takes a type parameter (T) that identifies what type the Value property on System.Lazy<T> will return. Instead of assigning a fully constructed TemporaryFileStream to the _FileStream field, an instance of Lazy<TemporaryFileStream> is assigned (a lightweight call), delaying the instantiation of the TemporaryFileStream itself, until the Value property (and therefore the FileStream property) is accessed.

If in addition to type parameters (generics) you use delegates, you can even provide a function for how to initialize an object when the Value property is accessed. Listing 9.25 demonstrates passing the delegate, a lambda expression in this case, into the constructor for System.Lazy<T>.

It is important to note that the lambda expression itself, () => new TemporaryFileStream(FileStreamName), does not execute until Value is called. Rather, the lambda expression provides a means of passing the instructions for what will happen, but not actually performing those instructions until explicitly requested.
