```
```csharp
public virtual void DoThis()
{
}

public virtual void DoThat()
{
}
}
```
```

Bear in mind that when you use the SynchronizedDemo class, only methods are synchronized. There is no synchronization for invoking other members of this class.

Now, change the SharedState class that was not synchronized at first to use the SyncRoot pattern. If you try to make the SharedState class thread-safe by locking access to the properties with the SyncRoot pattern, you still get the race condition shown earlier in the “Race Conditions” section:

```
```csharp
public class SharedState
{
    private int _state = 0;
    private object _syncRoot = new object();

    public int State // there's still a race condition,
    // don't do this!
    {
        get { lock (_syncRoot) { return _state; } }
        set { lock (_syncRoot) { _state = value; } }
    }
}
```
```

The thread invoking the DoTheJob method is accessing the get accessor of the SharedState class to get the current value of the state, and then the get accessor sets the new value for the state. In between calling the get and set accessors, the object is not locked, and another thread can read the interim value (code file SynchronizationSamples/Job.cs):

```
```csharp
public void DoTheJob()
{
    for (int i = 0; i < 50000; i++)
    {
        _sharedState.State += 1;
    }
}
```
```

Therefore, it is better to leave the SharedState class as it was earlier, without thread safety (code file SynchronizationSamples/SharedState.cs):

```
```csharp
public class SharedState
{
    public int State { get; set; }
}
```
```

In addition, add the lock statement where it belongs, inside the method DoTheJob (code file SynchronizationSamples/Job.cs):

```
```csharp
public void DoTheJob()
{
    for (int i = 0; i < 50000; i++)
    {
        _sharedState.State += 1;
    }
}
```
```