```
```csharp
}
[AttributeUsage(AttributeTargets.Parameter, Inherited = false)]
public sealed class CallerFilePathAttribute : Attribute
{
    public CallerFilePathAttribute() { }
}

[AttributeUsage(AttributeTargets.Parameter, Inherited = false)]
public sealed class CallerLineNumberAttribute : Attribute
{
    public CallerLineNumberAttribute() { }
}

[AttributeUsage(AttributeTargets.Parameter, Inherited = false)]
public sealed class CallerMemberNameAttribute : Attribute
{
    public CallerMemberNameAttribute() { }
}

public static class FormattableStringFactory
{
    public static FormattableString Create(string format,
        params object[] arguments);
}

public interface ICriticalNotifyCompletion : INotifyCompletion
{
    void UnsafeOnCompleted(Action continuation);
}

public interface INotifyCompletion
{
    void OnCompleted(Action continuation);
}

public readonly struct TaskAwaiter : ICriticalNotifyCompletion,
    INotifyCompletion
{
    public bool IsCompleted { get; }
    public void GetResult();
}

public readonly struct TaskAwaiter<TResult> : ICriticalNotifyCompletion,
    INotifyCompletion
{
    public bool IsCompleted { get; }
    public TResult GetResult();
}

public readonly struct ValueTaskAwaiter : ICriticalNotifyCompletion,
    INotifyCompletion
{
    public bool IsCompleted { get; }
    public void GetResult();
}
```
```