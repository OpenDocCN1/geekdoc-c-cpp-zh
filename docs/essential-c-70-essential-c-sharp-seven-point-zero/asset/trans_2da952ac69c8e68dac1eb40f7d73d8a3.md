
确实包含了执行此操作的能力。如果取消调用以某种方式具有破坏性——例如，阻止有效结果返回——那么抛出 `TaskCanceledException`（它继承自 `System.OperationCanceledException`）将是 TPL 报告此问题的标准模式。CancellationToken 包含一个 `ThrowIfCancellationRequested()` 方法，在存在 CancellationToken 实例的情况下，可以更轻松地报告异常，而无需显式抛出异常。

如果您尝试对已抛出 `TaskCanceledException` 的任务调用 `Wait()`（或获取 `Result`），其行为与在任务中抛出任何其他异常时相同：该调用将抛出 `AggregateException`。异常是一种通信机制，表明任务之后的执行状态可能不完整。与成功完成的任务（其中所有预期工作均成功执行）不同，已取消的任务可能具有部分完成的工作——工作状态不可信。

本示例展示了长时间运行的处理器密集型操作（几乎无限地计算圆周率）如何监控取消请求并在发生取消请求时作出响应。然而，在某些情况下，即使目标任务内部没有显式地编码处理，取消也可能发生。例如，本章后面讨论的 Parallel 类默认提供了这种行为。

## Task.Run()：Task.Factory.StartNew() 的快捷方式和简化

在 .NET 4.0 中，获取任务的一般做法是调用 `Task.Factory.StartNew()`。在 .NET 4.5 中，提供了更简单的调用结构 `Task.Run()`。与 `Task.Run()` 类似，`Task.Factory.StartNew()` 可以在 C# 4.0 场景中用于调用需要创建额外线程的 CPU 密集型方法。

在 .NET 4.5 中，除非证明 `Task.Run()` 不够用，否则应默认使用它。例如，如果您需要使用 `TaskCreationOptions` 控制任务、需要指定备用调度器，或者出于性能原因想要传入对象状态，那么应考虑使用 `Task.Factory.StartNew()`。只有在极少数需要分离创建和调度的情况下，才应考虑先通过构造函数实例化然后调用 `Start()`。

代码清单 19.11 提供了使用 `Task.Factory.StartNew()` 的示例。

### 代码清单 19.11：使用 Task.Factory.StartNew()

```csharp
public Task<string> CalculatePiAsync(int digits)
{
    return Task.Factory.StartNew<string>(
           () => CalculatePi(digits));
}

private string CalculatePi(int digits)
{
    // ...
}
```

## 长时间运行的任务

正如我们在代码清单 19.2 的注释中之前讨论的那样，线程池假设工作项将是处理器密集型且生命周期相对较短；它做出这些假设以有效限制创建的线程数。这既防止了昂贵线程资源的过度分配，也防止了处理器的过度订阅，后者会导致过多的上下文切换和时间切片。

但如果开发者知道任务将长时间运行，因此会占用底层线程资源很长时间怎么办？在这种情况下，开发者可以通知调度器该任务不太可能很快完成其工作。这有两个影响。首先，它提示调度器可能应该专门为此任务创建一个专用线程，而不是尝试使用线程池中的线程。其次，它提示调度器这也许是允许调度比处理器数量更多的任务的好时机。这将导致更多的时间切片，这是好事。我们不希望一个长时间运行的任务独占整个处理器并阻止较短任务使用它。短任务将能够利用其时间切片完成大部分工作，而长时间运行的任务不太可能注意到与其他任务共享处理器导致的相对轻微的延迟。为了实现这一点，在调用 `StartNew()` 时使用 `TaskCreationOptions.LongRunning` 选项，如代码清单 19.12 所示。（`Task.Run()` 不支持 `TaskCreationOptions` 参数。）

### 代码清单 19.12：协作执行长时间运行的任务

```csharp
using System.Threading.Tasks;

// ...

    Task task = Task.Factory.StartNew(
        () =>
            WritePi(cancellationTokenSource.Token),
        TaskCreationOptions.LongRunning);
// ...
```

> **准则**
- 告知任务工厂新创建的任务可能是长时间运行的，以便其可以适当地管理它。
- 谨慎使用 `TaskCreationOptions.LongRunning`。

## 任务是可释放的

注意，`Task` 还支持 `IDisposable`。这是必要的，因为 `Task` 在等待其完成时可能会分配一个 `WaitHandle`；由于 `WaitHandle` 支持 `IDisposable`，因此根据最佳实践，`Task` 也支持 `IDisposable`。然而，请注意，前面的代码示例不包含 `Dispose()` 调用，也不依赖于通过 `using` 语句隐式进行此类调用。这些清单实际上依赖于程序退出时 `WaitHandle` 终结器的自动调用。

这种方法导致两个显著结果。首先，句柄存活时间更长，因此消耗的资源比应有的多。其次，由于终结对象存活到下一代，垃圾回收器的效率略有降低。然而，除非正在终结极其大量的任务，否则在 `Task` 的情况下，这两个问题都不重要。因此，虽然从技术上讲所有代码都应该释放任务，但除非性能指标要求且操作简便——即您确定 `Task` 已完成且没有其他代码正在使用它们——否则您不必费心去做。

## 基于任务的异步模式

到目前为止，我们看到任务为异步操作的操控提供了比线程更好的抽象。任务会自动调度到正确数量的线程，并且可以通过将小任务链接在一起组成大任务，就像大型程序可以由多个小方法组成一样。

然而，任务也有一些缺点。使用任务的主要困难在于它们将你的程序逻辑“翻转”。为了说明这一点，我们首先考虑一个被阻塞在基于 I/O 的高延迟操作（网络请求）上的同步方法。接下来，我们将其与 C# 5.0 和 TAP 之前的异步版本进行比较。最后，我们使用 C# 5.0（及更高版本）和 async/await 上下文关键字来修订同一个示例。

### 同步调用高延迟操作

在代码清单 19.13 中，代码使用 WebRequest 下载网页并显示其大小。如果操作失败，将抛出异常。

### 代码清单 19.13：同步网络请求

```csharp
using System;
using System.IO;
using System.Net;
using System.Linq;

public class Program
{
    public static void Main(string[] args)
    {
        string url = "http://www.IntelliTect.com";
        if (args.Length > 0)
        {
            url = args[0];
        }

        try
        {
            Console.Write(url);
            WebRequest webRequest =
                WebRequest.Create(url);

            WebResponse response =
                webRequest.GetResponse();

            Console.Write("……");

            using (StreamReader reader =
                new StreamReader(
                    response.GetResponseStream()))
            {
                string text =
                reader.ReadToEnd();
                Console.WriteLine(
                    FormatBytes(text.Length));
            }
        }
        catch(WebException)
        {
            // ... }
        catch(IOException)
        {
            // ... }
        catch(NotSupportedException)
        {
            // ... }
    }

    static public string FormatBytes(long bytes)
    {
        string[] magnitudes =
            new string[] { "GB", "MB", "KB", "Bytes" };
        long max =
            (long)Math.Pow(1024, magnitudes.Length);

        return string.Format("{1:#,##} {0}",
                magnitudes.FirstOrDefault(
                    magnitude =>
                        bytes > (max /= 1024)) ? "0 Bytes",
                        (decimal)bytes / (decimal)max);
    }
}
```

代码清单 19.13 中的逻辑相对直接——使用常见的 C# 惯用法（如 try/catch 块和 return 语句）来描述控制流。给定一个 WebRequest，此代码调用 `GetResponse()` 来下载页面。为了获取页面的流访问，它调用 `GetResponseStream()` 并将结果分配给 `StreamReader`。最后，它通过 `ReadToEnd()` 读取到流的末尾以确定页面大小，然后将其打印到屏幕上。

这种方法的问题当然是，调用线程会阻塞直到 I/O 操作完成；这浪费了本可以在异步操作执行期间执行有用工作的线程。因此，例如，我们无法执行任何其他代码，如指示进度的代码。

