+   - The `IDisposable` interface provides a mechanism that enables users of a class to control when resources are freed but requires discipline to ensure that `Dispose` is called.

If you are creating a finalizer, you should also implement the `IDisposable` interface. You implement `IDisposable` on the assumption that most programmers will call `Dispose` correctly, but implement a destructor as a safety mechanism in case `Dispose` is not called. Here is an example of a dual implementation:

```
using System;

public class ResourceHolder: IDisposable
{
    private bool _isDisposed = false;

    public void Dispose()
    {
        Dispose(true);
        GC.SuppressFinalize(this);
    }

    protected virtual void Dispose(bool disposing)
    {
        if (! _isDisposed)
        {
            if (disposing)
            {
                // Cleanup managed objects by calling their
                // Dispose() methods.
            }
            // Cleanup unmanaged objects
        }
        _isDisposed = true;
    }

    ~ResourceHolder()
    {
        Dispose (false);
    }

    public void SomeMethod()
    {
        // Ensure object not already disposed before execution of any method
        if(_isDisposed)
        {
            throw new ObjectDisposedException("ResourceHolder");
        }

        // method implementation&hellip;
    }
}
```

You can see from this code that there is a second `protected` overload of `Dispose` that takes one `bool` parameter—and this is the method that does all the cleaning up. `Dispose(bool)` is called by both the destructor and by `IDisposable.Dispose`. The point of this approach is to ensure that all cleanup code is in one place.

The parameter passed to `Dispose(bool)` indicates whether