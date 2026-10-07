

## 第 8 章：接口

现在考虑此场景的完全实现版本，并需要满足以下封装要求：

- 不允许重写 `Run()` 方法。
- 不允许调用 `Start()` 或 `Stop()`，因为它们的执行顺序完全由包含它们的类型（我们称之为 `IWorkflowActivity`）控制。
- 允许替换“Do something ...”代码块中执行的任何内容。
- 如果重写 `Start()` 和 `Stop()` 是合理的，那么实现这些方法的类并不一定能够直接调用它们——它们是基类实现的一部分。
- 允许派生类型提供 `Run()` 方法，但当在 `IWorkflowActivity` 上调用 `Run()` 方法时，不应调用（派生类重写的）`Run()` 方法。

为了满足所有这些要求及更多需求，C# 8.0 提供了对 `protected` 接口成员的支持，这与类中的 `protected` 成员有一些显著差异。列表 8.14 展示了这些差异，输出 8.3 显示了结果。

# 列表 8.14：强制执行理想的 Run() 封装

```csharp
public interface IWorkflowActivity
{
    // 私有的，因此不是虚的
    private static void Start() =>
        Console.WriteLine("IWorkflowActivity.Start()...");

    // 密封以防止重写。
    sealed void Run()
    {
        try
        {
            Start();
            InternalRun();
        }
        finally
        {
            Stop();
        }
    }

    protected void InternalRun();
}
```

```csharp
// 私有的，因此不是虚的
private static void Stop() =>
    Console.WriteLine("IWorkflowActivity.Stop()...");
```

```csharp
public interface IExecuteProcessActivity : IWorkflowActivity
{
    protected void RedirectStandardOut() =>
    Console.WriteLine("IExecuteProcessActivity.RedirectStandardOut()...");
}

// 重写时不允许使用 sealed。
/* 
void IWorkflowActivity.InternalRun()
{
    RedirectStandardOut();
    ExecuteProcess();
    RestoreStandardOut();
}
*/

protected void ExecuteProcessInOut();
protected void RestoreStandardOut() =>
    Console.WriteLine("IExecuteProcessActivity.RestoreStandardOut()...");
}
```

```csharp
public class ExecuteProcessActivity : IExecuteProcessActivity
{
    public ExecuteProcessActivity(string executablePath) =>
        ExecutableName = executablePath
        ?? throw new ArgumentNullException(nameof(executablePath));

    public string ExecutableName { get; }

    void IExecuteProcessActivity.RedirectStandardOut() =>
        Console.WriteLine("IExecuteProcessActivity.RedirectStandardOut()...");

    void IExecuteProcessActivity.ExecuteProcess() =>
        Console.WriteLine("$ExecuteProcessActivity.IExecuteProcessActivity.ExecuteProcess()...");

    public static void Run()
    {
        ExecuteProcessActivity activity = new("dotnet");
        // 保护成员无法被调用
        // 即使在类中实现
        // 实现类也无法调用。
        // ((IWorkflowActivity)this).InternalRun();
        // activity.RedirectStandardInOut();
        activity.ExecuteProcess();
        Console.WriteLine(
            $"Executing non-polymorphic Run() with process '{activity.ExecutableName}'.");
    }
}

public class Program
{
    static public void Main()
    {
        ExecuteProcessActivity activity = new("dotnet");
        Console.WriteLine(
            $"Invoking ((IExecuteProcessActivity)activity).Run()...");
        // 输出:
        // Invoking ((IExecuteProcessActivity)activity).Run()...
        // IWorkflowActivity.Start()...
        // ExecuteProcessActivity.RedirectStandardOut()...
        // ExecuteProcessActivity.IExecuteProcessActivity.ExecuteProcess()...
        // ExecuteProcessActivity.RestoreStandardOut()...
        // IWorkflowActivity.Stop()...
        ((IExecuteProcessActivity)activity).Run();

        // 输出:
        // Invoking activity.Run()...
        // Executing non-polymorphic Run() with process 'dotnet'.
        Console.WriteLine();
        Console.WriteLine(
            $"Invoking activity.Run()...");
        ExecuteProcessActivity.Run();
    }
}
```

让我们考虑列表 8.14 是如何满足前面概述的要求的。

# 输出 8.3

```
Invoking ((ExecuteProcessActivity)activity).Run()...
IWorkflowActivity.Start()...
ExecuteProcessActivity.RedirectStandardOut()...
ExecuteProcessActivity.IExecuteProcessActivity.ExecuteProcess()...
ExecuteProcessActivity.RestoreStandardOut()...
IWorkflowActivity.Stop().

activity.Run()...
Executing non-polymorphic Run() with process 'dotnet'.
```

注意 `IWorkflowActivity.Run()` 是 `sealed` 的，因此不是虚的。这防止了派生类型更改其实现。对于任何 `IWorkflowActivity` 类型，对 `Run()` 的任何调用将始终执行 `IWorkflowActivity` 的实现。

`IWorkflowActivity.Start()` 和 `Stop()` 方法是私有的，因此它们对所有其他类型都是不可见的。即使 `IExecuteProcessActivity` 似乎具有启动/停止类型的活动，`IWorkflowActivity` 也不允许替换其实现。

`IWorkflowActivity` 定义了一个 `protected` 的 `InternalRun()` 方法，允许 `IExecuteProcessActivity`（如果需要，还有 `ExecuteProcessActivity`）对其重载。但请注意，`ExecuteProcessActivity` 的任何成员都无法调用 `InternalRun()`。也许该方法不应该在 `Start()` 和 `Stop()` 之外之外运行，因此层次结构中的接口（`IWorkflowActivity` 或 `ExecuteProcessActivity`）被允许调用该保护成员。

所有受保护的成员如果显式地这样做，就可以重写任何默认接口成员。例如，`ExecuteProcessActivity` 上的 `RedirectStandardOut()` 和 `RestoreStandardOut()` 实现都带有 `IExecuteProcessActivity` 前缀。

尽管其中一个被显式声明为 `virtual`，但 `RedirectStandardOut()` 和 `RestoreStandardOut()` 都是虚的（除非成员被密封，否则默认是虚的）。因此，将调用最派生的实现。每当 `IExecuteProcessActivity.InternalRun()` 调用 `RedirectStandardOut()` 时，执行的是 `ExecuteProcessActivity` 的实现而不是 `IExecuteProcessActivity` 的。

派生类型的实现可能会提供与父类中密封签名匹配的方法。例如，如果 `ExecuteProcessActivity` 提供与 `IWorkflowActivity` 中的 `Run()` 匹配的方法，将执行与类型相关的实现，而不是派生实现。在其他情况下，`Program.Main()` 中的 `((IExecuteProcessActivity)activity).Run()` 调用了 `IExecuteProcessActivity.Run()`，而 `activity.Run()` 调用了 `ExecuteProcessActivity.Run()`。

总之，通过 `protected` 接口成员提供的封装，结合其他成员修饰符，提供了一种全面的封装机制——尽管这种机制无疑是复杂的。

# 扩展方法与默认接口成员

在扩展已发布的接口以增加功能时，什么情况下默认接口成员比创建扩展方法或创建一个派自第一个接口并添加成员的第二个接口更好？在做此决定时应考虑以下因素：

- 两者在概念上都支持通过在接口实例上实现相同签名的方法来重写。
- 扩展方法可以在包含接口定义的程序集之外添加。
- 虽然允许默认接口属性，但没有可用的实例存储位置（不允许使用字段）来存储属性值，这限制了其适用范围仅限于计算属性。

