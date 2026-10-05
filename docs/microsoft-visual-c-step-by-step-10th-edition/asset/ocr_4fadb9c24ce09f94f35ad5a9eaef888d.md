```
{
  this.disposed = true;
}

public void SomeBehavior() // example method
{
  checkIfDisposed();
  ...
}
...
private void checkIfDisposed()
{
  if (this.disposed)
  {	hrow new ObjectDisposedException("Example: object has been disposed");
  }
}
```

Notice the following features of the Example class:

+   - The class implements the IDisposable interface.
- The public Dispose method can be called at any time by your application code.
- The public Dispose method calls a protected and overloaded version of the Dispose method that takes a Boolean parameter (described in an upcoming bullet point), passing the value true as the argument. The method actually performs the resource disposal.
- The finalizer calls the protected and overloaded version of the Dispose method that takes a Boolean parameter, passing the value false as the argument. The finalizer is called only by the garbage collector when your object is being finalized.
- You can safely call the Dispose method multiple times. The Dispose variable indicates whether the method has already been run and is a safety feature to prevent the method from attempting to dispose of the resources multiple times if it's called. (Your application might call Dispose, but before the method completes, your object might be subject to garbage collection and the Dispose method run again by the .NET runtime from the finalizer.) The resources are released only the first time the method runs.