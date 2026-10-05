+   The protected Dispose method supports disposal of managed resources (such as a large array) and unmanaged resources (such as a file handle). If the disposing parameter is true, this method must have been called from the public Dispose method. In this case, the managed and unmanaged resources are all released. If the disposing parameter is false, this method must have been called from the finalizer, and the garbage collector is finalizing the object. In this case, it's not necessary (or exception-safe) to release the managed resources because they will be, or might already have been, handled by the garbage collector, so only the unmanaged resources are released.

+   The public Dispose method calls the static GC.SuppressFinalize method. This method stops the garbage collector from calling the finalizer on this object because the object has already been finalized.

+   All the regular methods of the class (such as SomeBehavior) check to see whether the object has already been discarded. If it has, they throw an exception.

# # Implementing exception-safe disposal

In the following exercises, you'll examine the using statement to ensure that resources used by objects in your applications can be released promptly, even if an exception occurs in your application code. First, you'll implement a simple class that implements a finalizer and examine when this finalizer is invoked by the garbage collector.

> > Note
The Calculator class created in these exercises is intended only to illustrate the essential principles of garbage collection. The class does not actually consume any significant or unmanaged resources. You would not normally create a finalizer or implement the IDisposable interface for such a simple class as this.

# To create a simple class that uses a finalizer

+   1. Start Microsoft Visual Studio 2022, if it is not already running.