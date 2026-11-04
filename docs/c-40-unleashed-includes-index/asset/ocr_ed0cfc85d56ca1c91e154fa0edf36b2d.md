and the finalizer doesn't have any work left to do anymore. By doing so, you avoid the extra object death ceremony involving the finalizer queue:

```
public void Dispose()
{
    Dispose(true);
    GC.SuppressFinalize(this);
}
```

With all of this in place, we should never leak the job object handle anymore. To verify this claim, you can use Task Manager and observe the Handles column decrementing by 1 after the call to Dispose. Figure 12.7 shows this experiment. If the Dispose method isn't called, it will take some garbage collector cycles before the object disappears.

![](bbox=[0.08, 0.53, 0.78, 0.78])

FIGURE 12.7 Proper handle release triggered by a call to Dispose.

# SAFEHANDLE

Dealing with handles and providing a manual implementation of IDisposable and a finalizer is tricky business. To simplify this task, .NET 2.0 introduced the concept of SafeHandle objects, which are recommended to be used when dealing with some typical types of handles (see MSDN). The Microsoft.Win32.SafeHandles namespace contains base classes for a series of handle types.

# Summary

Initialization logic for newly created object instances or even types themselves is what constructors are about. In this chapter, you learned how to declare constructors that deal with such initialization of state. You saw how to chain constructor calls and learned about implications of having type initialization logic in static constructors.