> **CHRISTIAN NAGEL**  “The destruction is called at some unspecified later time . . .”
> 
> When a destructor is created, it’s usually a good idea to implement the interface IDisposable as well. With the IDisposable interface, the caller has a chance to invoke the cleanup code early, when the object is no longer needed.

> **CHRISTIAN NAGEL**  To invoke the destructor more than once, `GC.ReRegisterForFinalize` keeps the object alive and allows for the destructor to be called once more. Instead of taking this tack, it could be worthwhile to change the application architecture.

+   4. Once the destructor for an object is run, if that object, or any part of it, cannot be accessed by any possible continuation of execution, including the running of destructors, the object is considered inaccessible and the object becomes eligible for collection.
+   
+   5. Finally, at some time after the object becomes eligible for collection, the garbage collector frees the memory associated with that object.

The garbage collector maintains information about object usage, and uses this information to make memory management decisions, such as where in memory to locate a newly created object, when to relocate an object, and when an object is no longer in use or accessible.

Like other languages that assume the existence of a garbage collector, C# is designed so that the garbage collector may implement a wide range of memory management policies. For instance, C# does not require that destructors be run or that objects be collected as soon as they are eligible, or that destructors be run in any particular order, or on any particular thread.

The behavior of the garbage collector can be controlled, to some degree, via static methods on the class `System.GC`. This class can be used to request a collection to occur, destructors to be run (or not run), and so forth.

> **ERIC LIPPERT**  Using these static methods to control the behavior of the garbage collector is almost never a good idea. In production code, odds are good that the garbage collector knows more about when would be a good time to do a collection than your program does.
> 
> Explicit tweaking of the garbage collector behavior at runtime should typically be limited to purposes such as forcing a collection for testing purposes.

# 3. Basic Concepts