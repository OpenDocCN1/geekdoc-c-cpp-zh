```
```text
-Contact()
{
    Dispose(false);
}

public void Dispose()
{
    Dispose(true);
    GC.SuppressFinalize(this);
}

protected virtual void Dispose(bool disposing)
{
    if (!this.disposed)
    {
        if (disposing)
        {
            // Release only managed resources here.
        }

        // Release only unmanaged resource here.
        this.disposed = true;
    }
}
```
```

There are several important rules about declaring and using finalizers:

+   - The exact time and order of when a finalizer executes is undefined.
- The finalizer method runs on the GC thread, not the application's main thread.
- Finalizers apply only to reference types.
- You cannot specify an access modifier for a finalizer method.
- You cannot provide parameters to a finalizer method.
- You cannot overload or override a finalizer method.
- You cannot call a finalizer method directly in your own code; only the garbage collector can call a finalizer method.

Although finalizers are typically used when you want to provide some assurance that resources will be released even if the calling code does not call Dispose, it is not necessary to provide a finalizer just because you implement the dispose pattern. However, if you do implement a finalizer, be sure to also implement the dispose pattern.