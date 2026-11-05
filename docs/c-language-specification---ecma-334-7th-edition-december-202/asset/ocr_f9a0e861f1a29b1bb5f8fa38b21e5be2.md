```
```csharp
public Awaiter<T> GetAwaiter() { ... }
}
class Awaiter<T> : INotifyCompletion
{
    public void OnCompleted(Action completion) { ... }
    public bool IsCompleted { get; }
    public T GetResult() { ... }
}
```
```

*end example*

A task builder type is a class or struct type that corresponds to a specific task type (§15.15.2).

An async function has the ability to suspend evaluation by means of await expressions (§12.9.8) in its body. Evaluation may later be resumed at the point of the suspending await expression by means of a resumption delegate. The resumption delegate is of type System.Action, and when it is invoked, evaluation of the async function invocation will resume from the await expression where it left off. The current caller of an async function invocation is the original caller if the function invocation has never been suspended or the most recent caller of the resumption delegate otherwise.

# 15.15.2 Task-type builder pattern

A task builder type can have at most one type parameter and cannot be nested in a generic type. A task builder type shall have the following accessible members (for non-generic task builder types, SetResult has no parameters):

```
```csharp
class «TaskBuilderType»<T>
{
    public static «TaskBuilderType»<T> Create();
    public void Start<TStateMachine>(ref TStateMachine stateMachine)
        where TStateMachine : IAsyncStateMachine;
    public void SetStateMachine(IAsyncStateMachine stateMachine);
    public void SetException(Exception exception);
    public void SetResult(T result);
    public void AwaitOnCompleted<TAwaiter, TStateMachine>(
        ref TAwaiter awaiter, ref TStateMachine stateMachine)
        where TAwaiter : INotifyCompletion
        where TStateMachine : IAsyncStateMachine;
    public void AwaitUnsafeOnCompleted<TAwaiter, TStateMachine>(
        ref TAwaiter awaiter, ref TStateMachine stateMachine)
        where TAwaiter : ICriticalNotifyCompletion
        where TStateMachine : IAsyncStateMachine;
    public «TaskType»<T> Task { get; }
}
```
```

The compiler generates code that uses the «TaskBuilderType» to implement the semantics of suspending and resuming the evaluation of the async function. The compiler uses the «TaskBuilderType» as follows:

+   - «TaskBuilderType».Create() is invoked to create an instance of the «TaskBuilderType», named builder in this list.
+   - builder.Start(ref stateMachine) is invoked to associate the builder with a compiler-generated state machine instance, stateMachine.
+     - The builder must call stateMachine.MoveNext() either in Start() or after Start() has returned to advance the state machine.