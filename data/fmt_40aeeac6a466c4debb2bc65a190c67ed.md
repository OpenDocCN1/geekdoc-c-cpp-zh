
线程 3 运行一段时间；它抛出一个未处理异常，事件处理程序被调用，并进入睡眠。此后不久，操作系统意识到线程 1 可以被调度，但其代码立即让它进入睡眠。线程 1 首先醒来并运行`finally`块，然后 2 秒后线程 3 醒来，未处理异常最终导致进程崩溃。

这一系列事件——事件处理程序执行，以及在其完成后进程崩溃——是典型的，但不是必然的。程序中一旦出现未处理异常，一切都无法预料；程序现在处于未知且可能非常不稳定的状态，因此其行为可能是不可预测的。在这种情况下，如你所见，CLR 允许主线程继续运行并执行其`finally`块，即使它知道当控制权到达`finally`块时，另一个线程正处于`AppDomain`的未处理异常事件处理程序中。

为了强调这一事实，试着更改延迟，使主线程的睡眠时间长于事件处理程序。在那种情况下，`finally`块将永远不会执行！进程会在线程 1 醒来之前被未处理异常销毁。根据抛出异常的线程是否由线程池创建，你还会得到不同的结果。因此，最佳实践是避免所有可能的未处理异常，无论它们发生在工作线程还是主线程中。

这与任务有什么关系？如果你想要关闭系统时，系统中还有未完成的任务挂在那里怎么办？我们将在下一节中讨论任务取消。

## 指南

- **避免**编写在任何线程上产生未处理异常的程序。
- **考虑**注册未处理异常事件处理程序，用于调试、日志记录和紧急关闭。
- **务必**取消未完成的任务，而不是让它们在应用程序关闭期间继续运行。

## 取消任务

在本章前面，我们解释了为什么为了取消线程正在执行的任务而粗鲁地中止该线程是一个坏主意。TPL 使用协作式取消，这是一种更礼貌、更健壮、更可靠的技术，用于安全地取消不再需要的任务。支持取消的任务通过定期轮询`CancellationToken`对象（位于`System.Threading`命名空间中）来监视是否已发出取消请求。清单 18.10 演示了取消请求和对此请求的响应。输出 18.6 显示了结果。

### 清单 18.10：使用`CancellationToken`取消任务

```
using System;

using System.Threading;

using System.Threading.Tasks;

using AddisonWesley.Michaelis.EssentialCSharp.Shared;

public class Program

{

    public static void Main()

    {

        string stars =

            "*".PadRight(Console.WindowWidth-1, '*');

        Console.WriteLine("Push ENTER to exit.");

        CancellationTokenSource cancellationTokenSource=

            new CancellationTokenSource();

        // Use Task.Factory.StartNew<string>() for

        // TPL prior to .NET 4.5

        Task task = Task.Run(

            () =>

                WritePi(cancellationTokenSource.Token),

                cancellationTokenSource.Token);

        // Wait for the user's input

        Console.ReadLine();

        cancellationTokenSource.Cancel();

        Console.WriteLine(stars);

        task.Wait();

        Console.WriteLine();

    }

    private static void WritePi(

        CancellationToken cancellationToken)

    {

        const int batchSize = 1;

        string piSection = string.Empty;

        int i = 0;

        while(!cancellationToken.IsCancellationRequested

            || i == int.MaxValue)

{

    piSection = PiCalculator.Calculate(

        batchSize, (i++) * batchSize);

    Console.Write(piSection);

}

}
```

### 输出 18.6

```
Push ENTER to exit.

3.141592653589793238462643383279502884197169399375105820974944592307816

40628620899862803482534211706798214808651328230664709384460955058223172

5359408128481117450

**************************************************************

2

```

任务启动后，`Console.Read()` 会阻塞主线程。与此同时，任务继续执行，计算 pi 的下一位数字并打印出来。一旦用户按下 Enter，执行过程会遇到对 `CancellationTokenSource.Cancel()` 的调用。在清单 18.10 中，我们将 `task.Cancel()` 的调用与 `task.Wait()` 的调用分开，并在两者之间打印一行星号。这一步的目的是表明在取消令牌被观察到之前很可能还会再执行一次迭代——因此输出 18.6 中星号之后多了一个 2。出现这个 2 是因为 `CancellationTokenSource.Cancel()` 并不会粗鲁地停止任务执行。任务会一直运行，直到检查令牌；当它看到令牌的所有者正在请求取消任务时，它会礼貌地关闭。

`Cancel()` 调用会有效地设置从 `CancellationTokenSource.Token` 复制的所有取消令牌上的 `IsCancellationRequested` 属性。不过，有几点需要注意：

- 传递给异步任务的是 `CancellationToken`，而不是 `CancellationTokenSource`。`CancellationToken` 支持轮询取消请求；`CancellationTokenSource` 提供令牌，并在取消时发出信号（参见图 18.2）。通过传递 `CancellationToken` 而不是 `CancellationTokenSource`，我们不必担心 `CancellationTokenSource` 上的线程同步问题，因为后者仅对原始线程保持可访问。
- `CancellationToken` 是一个结构体，因此按值复制。`CancellationTokenSource.Token` 返回的值产生令牌的副本。因此，`CancellationToken` 是线程安全的——它只能从 `WritePi()` 方法内部使用。

![](img/25683ccec0773ba5b8794b11f2b12877_809_0.png)

![](img/25683ccec0773ba5b8794b11f2b12877_809_1.png)

图 18.2：`CancellationTokenSource` 和 `CancellationToken` 类图

为了监视 `IsCancellationRequested` 属性，会将 `CancellationToken` 的副本（从 `CancellationTokenSource.Token` 获取）传递给任务。在清单 18.9 中，我们会偶尔检查 `CancellationToken` 参数上的 `IsCancellationRequested` 属性；在本例中，我们在每次数字计算后进行检查。如果 `IsCancellationRequested` 返回 `true`，则 `while` 循环退出。与线程中止（会在随机点抛出异常）不同，我们使用正常的控制流退出循环。我们通过频繁轮询来确保代码对取消请求保持响应。

关于 `CancellationToken` 还需要注意的一点是重载的 `Register()` 方法。通过此方法，你可以注册一个操作，该操作会在令牌被取消时被调用。换句话说，调用 `Register()` 方法相当于在对应的 `CancellationTokenSource` 的 `Cancel()` 上订阅一个监听器委托。

考虑到在完成之前取消是此程序中的预期行为，清单 18.9 中的代码不会抛出 `System.Threading.TaskCanceledException`。因此，`task.Status` 将返回 `TaskStatus.RanToCompletion`——没有表明任务的工作实际上已被取消的迹象。在本例中，并不需要这种指示；然而，TPL 确实包含了实现此功能的能力。如果取消调用在某种程度上具有破坏性——例如阻止有效结果返回——则抛出 `TaskCanceledException`（它派生自 `System.OperationCanceledException`）将是 TPL 用于报告它的模式。除了显式抛出异常外，`CancellationToken` 还包含 `ThrowIfCancellationRequested()` 方法，以便在有 `CancellationToken` 实例可用时更轻松地报告异常。

如果尝试对抛出 `TaskCanceledException` 的任务调用 `Wait()`（或获取其 `Result`），其行为与任务中抛出任何其他异常时相同：该调用将抛出 `AggregateException`。异常是传达任务执行后状态可能不完整的手段。与所有预期工作均成功执行且成功完成的任务不同，已取消的任务可能具有部分完成的工作——工作的状态不可信。

此示例演示了如何让长时间运行的处理器绑定操作（几乎无限期地计算 pi）监控取消请求并在发生时做出响应。然而，在某些情况下，取消可以在目标任务中未显式编码的情况下发生。例如，本章后面讨论的 `Parallel` 类默认提供此类行为。

## `Task.Run()`：`Task.Factory.StartNew()` 的快捷方式和简化

在 .NET 4.0 中，获取任务的通用做法是调用 `Task.Factory.StartNew()`。在 .NET 4.5 中，`Task.Run()` 提供了更简单的调用结构。与 `Task.Run()` 一样，`Task.Factory.StartNew()` 可在 C# 4.0 场景中用于调用需要创建额外线程的 CPU 密集型方法。

鉴于 .NET 4.5，除非证明不足，否则应默认使用 `Task.Run()`。例如，如果你需要使用 `TaskCreationOptions` 控制任务，如果你需要指定替代调度程序，或者出于性能原因，你想传入对象状态，你应考虑使用 `Task.Factory.StartNew()`。只有在极少数情况下，你

## 基于任务的异步模式

正如我们迄今所见，任务为异步工作的操作提供了比线程更好的抽象。任务会自动调度到正确数量的线程，并且可以通过链接小任务来组合大型任务，就像可以通过多个小方法组合大型程序一样。

然而，任务也有一些缺点。任务的主要困难在于它将你的程序逻辑“倒转”过来。为了说明这一点，我们首先考虑一个阻塞于 I/O 绑定、高延迟操作——Web 请求的同步方法。接下来，我们将其与 C# 5.0 之前的异步版本和基于任务的异步模式（TAP）进行比较。最后，我们使用 C# 5.0（及以上）以及 `async/await` 上下文关键字修改相同的示例。

## 同步调用高延迟操作

在列表 18.13 中，代码使用 `WebRequest` 下载网页并显示其大小。如果操作失败，则会抛出异常。

### LISTING 18.13: A Synchronous Web Request

```
using System;

using System.IO;

using System.Net;

using System.Linq;

public class Program

{

    public static void Main(string[] args)

    {

        string url = "http://www.IntelliTect.com";

        if(args.Length > 0)

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

            Console.Write("....");
            using(StreamReader reader =

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

            // ...

        }

        catch(IOException )

        {

            // ...

        }

        catch(NotSupportedException )

        {

            // ...

        }

        static public string FormatBytes(long bytes)

        {

            string[] magnitudes =

                new string[] { "GB", "MB", "KB", "Bytes" };

            long max =

                (long)Math.Pow(1024, magnitudes.Length);

            return string.Format("{1:##.##} {0}",

                magnitudes.FirstOrDefault(

                    magnitude =>

                        bytes > (max /= 1024)) ?? "0 Bytes",

                (decimal)bytes / (decimal)max);

        }

}
```

列表 18.13 中的逻辑相对简单——使用常见的 C# 习惯用法，如 `try`/`catch` 块和 `return` 语句来描述控制流。给定一个 `WebRequest`，此代码调用 `GetResponse()` 来下载页面。为了获得对页面的流访问，它调用 `GetResponseStream()` 并将结果分配给 `StreamReader`。最后，它使用 `ReadToEnd()` 读取流末尾以确定页面的大小，然后将其打印到屏幕上。

这种方法的问题当然是，调用线程在 I/O 操作完成之前被阻塞；这浪费了一个线程

```
return true;

});

}

catch(WebException)

{

    // ...

}

catch(IOException )

{

    // ...

}

catch(NotSupportedException )

{

    // ...

}

}

private static Task WriteWebRequestSizeAsync(

    string url)

{

    StreamReader reader = null;

    WebRequest webRequest =

        WebRequest.Create(url);

    Task task =

        webRequest.GetResponseAsync()

        .ContinueWith( antecedent =>

        {

            WebResponse response =

                antecedent.Result;

            reader =

                new StreamReader(

                    response.GetResponseStream());

            return reader.ReadToEndAsync();

        })

        .Unwrap()

        .ContinueWith(antecedent =>

        {

            if(reader != null) reader.Dispose();

            string text = antecedent.Result;

            Console.WriteLine(

                FormatBytes(text.Length));

        });

    return task;

}

// ...

}
```

