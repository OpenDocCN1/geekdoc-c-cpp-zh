The thread invoking the `DoTheJob()` method is accessing the `get` accessor of the `SharedState` class to get the current value of the state, and then the `get` accessor sets the new value for the state. In between calling the `get` and the `set` accessor, the object is not locked, and another thread can be the interim value.

```
```csharp
public void DoTheJob()
{
    for (int i = 0; i < 50000; i++)
    {
        sharedState.State += 1;
    }
}
```
```

code snippet SynchronizationSamples/Job.cs

So, it is better to leave the `SharedState` class as it was earlier without thread safety:

```
```csharp
public class SharedState
{
    public int State { get; set; }
}
```
```

code snippet SynchronizationSamples/SharedState.cs

And to add the `lock` statement where it belongs, inside the method `DoTheJob()`:

```
```csharp
public void DoTheJob()
{
    for (int i = 0; i < 50000; i++)
    {
        lock (sharedState)
        {
            sharedState.State += 1;
        }
    }
}
```
```

code snippet SynchronizationSamples/Job.cs

This way, the results of the application are always as expected:

summarized 1000000

> > Using the `lock` statement in one place does not mean that all other threads accessing the object are waiting. You have to explicitly use synchronization with every thread accessing the shared state.

Of course, you can also change the design of the `SharedState` class and offer incrementing as an atomic operation. This is a design question — what should be an atomic functionality of the class?

```
```csharp
public class SharedState
{
    private int state = 0;
    private object syncRoot = new object();

    public int State
    {
        get { return state; }
    }

    public int IncrementState()
    {
```
```