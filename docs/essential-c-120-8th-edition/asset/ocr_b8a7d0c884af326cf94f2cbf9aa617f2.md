# 590 Chapter 10: Well-Formed Types

DO call System.GC.SuppressFinalize() from Dispose() to avoid repeating resource cleanup and delaying garbage collection an object.

DO ensure that Dispose() is idempotent (it should be possible to call Dispose() multiple times).

DO keep Dispose() simple, focusing on the resource cleanup required by finalization.

AV calling Dispose() on objects that have a finalizer. Instead, rely on the finalization queue to clean up the instance.

AV referencing other objects that are not being finalized during finalization.

DO invoke a base class's Dispose() method when overriding Dispose().

CONSIDER ensuring that an object becomes unusable after Dispose() is called. After an object has been disposed, methods other than Dispose() (which could potentially be called multiple times) should throw an ObjectDisposedException.

DO implement IDisposable on types that have own disposable fields (or properties) and dispose of those instances.

DO invoke a base class's Dispose() method from the Dispose(bool disposing) method if one exists.

# Language Contrast: C++—Deterministic Destruction

Although finalizers are similar to destructors in C++, the fact that their execution cannot be determined at compile time makes them distinctly different. The garbage collector collects C# finalizers after they were used but before the program shuts down; C++ destructors are automatically called when the object (not a pointer) goes out of scope.

Although running the garbage collector can be a relatively expensive process, the fact that garbage collection is intelligent enough to delay running until process utilization is somewhat reduced offers an advantage over deterministic destructors, which will run at compile-time-defined locations, even when a processor is in high demand.