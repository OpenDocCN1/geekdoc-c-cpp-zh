
清理工作是在 `Dispose()` 方法中完成的，而不是等待终结器执行。

如果不调用 `SuppressFinalize()`，对象的实例将包含在 f-reachable 队列中——这是一个所有已准备好进行垃圾回收的对象的列表，只是它们实现了析构器。在它们的终结化方法被调用之前，运行时无法垃圾回收带有终结器的对象。然而，垃圾回收本身并不调用终结化方法。相反，指向终结化对象的引用被添加到 f-reachable 队列中，并根据执行上下文在认为适当的时间内由额外的线程进行处理。讽刺的是，这种方法延迟了托管资源的垃圾回收——而恰恰是这些资源最应该被清理的时候。延迟的原因是 f-reachable 队列是一个“引用”列表；因此，在它们的终结化方法被调用且对象引用从 f-reachable 队列中移除之前，这些对象均不被视为垃圾。

> 注意
> 未显式调用 Dispose 的带有终结器的对象最终会导致对象生命周期延长。即使在所有显式引用都超出范围后，f-reachable 队列仍然持有引用，使对象保持存活，直到 f-reachable 队列处理完成。

出于这个原因，`Dispose()` 调用了 `SuppressFinalize`（即 `System.GC.SuppressFinalize`）。调用此方法通知运行时它不应将此对象添加到终结化队列，而应该在对象不再具有任何引用（包括任何 f-reachable 引用）时允许垃圾回收器释放该对象。

其次，`Dispose()` 调用参数为 `true` 的 `Dispose(bool disposing)`。结果是调用了 Stream  `Dispose()` 方法（清理其资源并抑制其终结化）。接下来，临时文件本身在调用 `Dispose()` 后立即被删除。这一重要调用消除了在等待终结化队列处理完成之前清理可能昂贵的资源的需要。

# 资源清理 589

第三，终结器并不是调用 `Close()`，而是调用参数为 `false` 的 `Dispose(bool disposing)`。结果是 Stream 没有被关闭（释放），尽管文件已被删除。关于调用 Stream 的条件确保了如果从终结器中调用 `Dispose(bool disposing)`，则 Stream 实例本身也将被加入终结化处理队列（或根据顺序可能已经运行）。因此，在执行终结器时，不应清理由托管资源拥有的对象，因为此操作将是终结化队列的职责。

第四，在同时创建 `Close()` 类型和 `Dispose()` 方法时，你应该保持谨慎。仅通过 API 无法看出 `Close()` 调用了 `Dispose()`，开发者将疑惑是否应该显式调用 `Close()` 和 `Dispose()`。

第五

### 指南原则

- 对于资源稀缺或昂贵的对象，**必须**实现 dispose 模式。
- 对于带有终结器的类**必须**实现 IDisposable 以支持可能的确定性终结化。
- 仅对没有终结器但仍需要清理的资源实现终结化方法。
- 重构终结化方法以调用与 IDisposable 相同的代码，可能只需调用 `Dispose()` 方法即可。
- **不要**从终结化方法中抛出异常。
- **考虑**通过 AppDomain.ProcessExit 注册终结化代码，以增加资源清理在进程退出前执行的概率。
- 在 dispose 期间注销任何 AppDomain.ProcessExit 事件。

# 590 第 10 章：良好的类型

- 从 `Dispose()` 调用 `System.GC.SuppressFinalize()` 以避免重复清理资源并延迟对象的垃圾回收。
- **必须**确保 `Dispose()` 是等等的（即可以多次调用 `Dispose()`）。
- **必须**保持 `Dispose()` 简单，重点关注终结化所需的资源清理。
- **避免**对带有终结器的对象调用 `Dispose()`。相反，请依赖终结化队列来清理实例。
- **避免**在终结化期间引用未正在终结化的对象。
- 在重写 `Dispose()` 时，**必须**调用基类的 `Dispose()` 方法。
- **考虑**确保对象在调用 `Dispose()` 后变得不可用。在对象被释放后，除 `Dispose()` 的其他方法（可能会被多次调用）应该抛出 `ObjectDisposedException`。
- 对于拥有自己的可释放字段（或属性）的类型，**必须**实现 IDisposable 并释放这些实例。
- 如果存在 `Dispose(bool disposing)` 方法，**必须**从其中调用基类的 `Dispose()` 方法。

# 语言对比：C++—确定性析构

尽管终结器与 C++ 中的析构函数相似，但其执行时间无法在编译时确定的事实使得它们有显著区别。垃圾回收器在 C# 终结器使用后但在程序关闭前收集它们；而 C++ 析构函数在对象（而非指针）超出范围时会被自动调用。

虽然运行垃圾回收可能是一个昂贵的过程，但垃圾回收足够智能，可以延迟到进程利用率某种程度上降低时运行，这比确定性析构函数具有优势，后者会在编译时定义的位置运行，即使在处理器处于高需求时也是如此。

# 资源清理

# 高级主题

### 在进程退出前强制执行资源清理

从 .NET Core 开始，进程在关闭时终结器可能不会执行。为了增加执行的概率，应该将终结化活动注册为进程¹¹⁰关闭时执行。出于这个原因，请注意列表 10.18 中 `SampleUnmanagedResource` 构造函数中涉及 `ProcessExit` 的语句，输出 0.3 显示了未向程序传递参数时的结果。（代码涉及 LINQ、事件注册和特殊属性，¹¹，这些将分别在第 12、14 和 18 章中介绍。）

¹¹⁰ 技术上是应用程序域，至少对于 .NET Framework 项目而言是。
¹¹ 参见随附的源代码。

列表 10.18：通过 Process Exit 注册

```csharp
using System.IO;
using System.Linq;
using System.Runtime.Compilers;
using static Console;

public static class Program
{
    public static void Main(string[] args)
    {
        WriteLine("Starting...");
        DoStuff();
        if (args.Any(arg => arg.ToLower() == "-gc")
        {
            GC.Collect();
            GC.WaitForPendingFinalizers();
        }
        WriteLine("Exiting...");
    }

    public static void DoStuff()
    {
        // ...

        WriteLine("Starting...");
    }
}
```

# 第 10 章：良好的类型

sampleUnmanagedResource? sampleUnmanagedResource = null;

```csharp
try {
    sampleUnmanagedResource =
        new SampleUnmanagedResource();
    // 使用非托管资源
    // ...
}
finally {
    if (Environment.GetCommandLineArgs().Any(arg => arg.ToLower() == "-dispose") {
        sampleUnmanagedResource?.Dispose();
    }
    WriteLine("Exiting...");
}
```

```csharp
class SampleUnmanagedResource : IDisposable {
    public SampleUnmanagedResource(string fileName) {
        WriteLine("Starting...",
            $"{nameof(SampleUnmanagedResource)}\.ctor");
        WriteLine("Creating托管 stuff...",
            $"{nameof(SampleUnmanagedResource)}\.ctor");
        WriteLine("Creating非托管 stuff...",
            $"{nameof(SampleUnmanagedResource)}\.ctor");
    }
}
```

```csharp
WeakReference<IDisposable> weakReferenceToSelf = new(this);
ProcessExitHandler = (_, _) => {
    WriteLine("Starting...", "ProcessExitHandler");
    if (weakReferenceToSelf.TryGetTarget(out IDisposable self)) {
        self.Dispose();
    }
    WriteLine("Exiting...", "ProcessExitHandler");
}
```

