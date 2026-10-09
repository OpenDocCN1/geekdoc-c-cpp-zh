
Second, Dispose() calls Dispose(bool disposing) with an argument of true. The result is that the Dispose() method on Stream is invoked (cleaning up its resources and suppressing its finalization). Next, the temporary file itself is deleted immediately upon calling Dispose(). This important call eliminates the need to wait for the finalization queue to be processed before cleaning up potentially expensive resources.

Third, rather than calling Close(), the finalizer now calls Dispose(bool disposing) with an argument of false. The result is that Stream is not closed (disposed) even though the file is deleted. The condition around closing Stream ensures that if Dispose(bool disposing) is called from the finalizer, the Stream instance itself will also be queued up for finalization processing (or possibly it would have already run depending on the order). Therefore, when executing the finalizer, objects owned by the managed resource should not be cleaned up, as this action will be the responsibility of the finalization queue.

Fourth, you should use caution when creating both a Close() type and a Dispose() method. It is not clear by looking at only the API that Close() calls Dispose(), so developers will be left wondering whether they need to explicitly call Close() and Dispose().

## Guidelines

- DO implement a finalizer method only on objects with resources that are scarce or expensive, even though finalization delays garbage collection.
- DO implement IDisposable to support deterministic finalization on classes with finalizers.
- DO implement a finalizer method on classes that implement IDisposable in case Dispose() is not invoked explicitly.
- DO refactor a finalization method to call the same code as IDisposable, perhaps simply calling the Dispose() method.
- DO NOT throw exceptions from finalizer methods.
- DO call System.GC.SuppressFinalize() from Dispose() to avoid repeating resource cleanup and delaying garbage collection on an object.
- DO ensure that Dispose() is idempotent (it should be possible to call Dispose() multiple times).
- DO keep Dispose() simple, focusing on resource cleanup required by finalization.
- AVOID calling Dispose() on owned objects that have a finalizer. Instead, rely on the finalization queue to clean up the instance.
- AVOID referencing other objects that are not being finalized during finalization.
- DO invoke a base class's Dispose() method when overriding Dispose().
- CONSIDER ensuring that an object becomes unusable after Dispose() is called. After an object has been disposed, methods other than Dispose() (which could potentially be called multiple times) should throw an ObjectDisposedException.
- DO implement IDisposable on types that own disposable fields (or properties) and dispose of said instances.

### Language Contrast: C++—Deterministic Destruction

Although finalizers are similar to destructors in C++, the fact that their execution cannot be determined at compile time makes them distinctly different. The garbage collector calls C# finalizers some time after they were last used but before the program shuts down; C++ destructors are automatically called when the object (not a pointer) goes out of scope.

Although running the garbage collector can be a relatively expensive process, the fact that garbage collection is intelligent enough to delay running until process utilization is somewhat reduced offers an advantage over deterministic destructors, which will run at compile-time–defined locations, even when a processor is in high demand.

### ADVANCED TOPIC

#### Exception Propagating from Constructors

Even when an exception propagates out of a constructor, the object is still instantiated, although no new instance is returned by the new operator. If the type defines a finalizer, the method will run when the object becomes eligible for garbage collection (providing additional motivation to ensure the finalize method can run on partially constructed objects). Also note that if a constructor prematurely shares its this reference, it will still be accessible even if the constructor throws an exception. Do not allow this scenario to occur.

### ADVANCED TOPIC

## Resurrecting Objects

By the time an object’s finalization method is called, all references to the object have disappeared and the only step before garbage collection is running the finalization code. Even so, it is possible to add a reference inadvertently for a finalization object back into the root reference’s graph. In such a case, the re-referenced object will no longer be inaccessible; in turn, it will not be ready for garbage collection. However, if the finalization method for the object has already run, it will not necessarily run again unless it is explicitly marked for finalization (using the GC.ReRegisterFinalize() method).

Obviously, resurrecting objects in this manner is peculiar behavior, and you should generally avoid it. Finalization code should be simple and should focus on cleaning up only the resources that it references.

## Lazy Initialization

In the preceding section, we discussed how to deterministically dispose of an object with a using statement and how the finalization queue will dispose of resources in the event that no deterministic approach is used.

A related pattern is called *lazy initialization* or *lazy loading*. Using lazy initialization, you can create (or obtain) objects when you need them rather than beforehand—the latter can be an especially problematic situation when those objects are never used. Consider the `FileStream` property of Listing 10.23.

### LISTING 10.23: Lazy Loading a Property

```csharp
using System.IO;

class DataCache
{
    // ...
    public TemporaryFileStream FileStream =>
        InternalFileStream ?? (InternalFileStream = new TemporaryFileStream());
}

private TemporaryFileStream InternalFileStream
{ get; set; } = null;

// ...
```

In the `FileStream` expression-bodied property, we check whether `InternalFileStream` is null or not null before returning its value directly. If `InternalFileStream` is null, we first instantiate the `TemporaryFileStream` object and assign it to `InternalFileStream` before returning the new instance. Thus, the `TemporaryFileStream` required in the `FileStream` property is created only when the getter on the property is called. If the getter is never invoked, the `TemporaryFileStream` object would not be instantiated and we would save whatever execution time such an instantiation would cost. Obviously, if the instantiation is negligible or inevitable (and postponing the inevitable is less desirable), simply assigning it during declaration or in the constructor makes sense.

### ADVANCED TOPIC

## Lazy Loading with Generics and Lambda Expressions

Starting with Microsoft .NET Framework 4.0, a new class was added to the CLR to assist with lazy initialization: `System.Lazy<T>`. Listing 10.24 demonstrates how to use it.

### LISTING 10.24: Lazy Loading a Property with System.Lazy<T>

```csharp
using System.IO;

class DataCache
{
    // ...
    public TemporaryFileStream FileStream =>
        InternalFileStream.Value;
    private Lazy<TemporaryFileStream> InternalFileStream { get; }
        = new Lazy<TemporaryFileStream>(
            () => new TemporaryFileStream());
    // ...
}
```

The `System.Lazy<T>` class takes a type parameter (T) that identifies which type the `Value` property on `System.Lazy<T>` will return. Instead of assigning a fully constructed `TemporaryFileStream` to the `_FileStream` field, an instance of `Lazy<TemporaryFileStream>` is assigned (a lightweight call), delaying the instantiation of the `TemporaryFileStream` itself until the `Value` property (and therefore the `FileStream` property) is accessed.

If in addition to type parameters (generics) you use delegates, you can even provide a function for how to initialize an object when the `Value` property is accessed. Listing 10.24 demonstrates passing the delegate—a lambda expression in this case—into the constructor for `System.Lazy<T>`.

Note that the lambda expression itself, `() => new TemporaryFileStream (FileStreamName)`, does not execute until `Value` is called. Rather, the lambda expression provides a means of passing the instructions for what will happen; it does not actually execute those instructions until explicitly requested to do so.

One obvious question is when you should use the `System.Lazy<T>` rather than the approach outlined in Listing 10.23. The difference is negligible: In fact, Listing 10.23 may actually be simpler. That is, it is simpler until there are multiple threads involved, such that a race condition might occur regarding the instantiation. In Listing 10.23, more than one check for null might potentially occur before instantiation, resulting in multiple instances being created. In contrast, `System.Lazy<T>` provides a thread-safe mechanism ensuring that one and only one object will be created.

## SUMMARY

This chapter provided a whirlwind tour of many topics related to building solid class libraries. All the topics pertain to internal development as well, but they are much more critical to building robust classes. Ultimately, the focus here was on forming more robust and programmable APIs. In the category of robustness, we can include namespaces and garbage collection. Both of these topics fit in the programmability category as well, along with overriding `object`’s virtual members, operator overloading, and XML comments for documentation.

Exception handling uses inheritance heavily by defining an exception hierarchy and enforcing custom exceptions to fit within this hierarchy. Furthermore, the `C#` compiler uses inheritance to verify catch block order. In the next chapter, you will see why inheritance is such a core part of exception handling.
