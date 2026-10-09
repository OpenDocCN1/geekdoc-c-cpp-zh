

Thread thread = new Thread(() =>
{
    Message("Throwing exception.");
    throw new Exception();
});
thread.Start();

    Delay(2000);
}
finally
{
    Message("Finally block running.");
}

static void Delay(int i)
{
    Message($"Sleeping for {i} ms");
    Thread.Sleep(i);
    Message("Awake");
}

static void Message(string text)
{
    Console.WriteLine("{0}:{1:0000}:{2}",
        Thread.CurrentThread.ManagedThreadId,
        clock.ElapsedMilliseconds, text);
}

### **输出 19.5**

3:0047:Throwing exception.
3:0052:Unhandled exception handler starting.
3:0055:Sleeping for 4000 ms
1:0058:Sleeping for 2000 ms
1:2059:Awake
1:2060:Finally block running.
3:4059:Awake
Unhandled Exception: System.Exception: Exception of type 'System.Exception' was thrown.

如**输出 19.5**所示，新线程被分配了线程 ID 3，而主线程被分配了线程 ID 1。操作系统调度线程 3 运行一段时间；它抛出一个未处理的异常，事件处理程序被调用，然后它进入睡眠。紧随其后，操作系统意识到可以调度线程 1，但其代码立即使其进入睡眠。线程 1 先醒来并运行 finally 块，然后在 2 秒后线程 3 醒来，未处理的异常最终导致进程崩溃。

这种事件顺序——事件处理程序执行，进程在其完成后崩溃——是典型的，但并不保证总是发生。一旦你的程序中出现了未处理的异常，所有既定的行为都不可预测了；程序现在处于一个未知且可能极不稳定的状态，因此其行为可能是不可预测的。在这种情况下，如你所见，CLR（公共语言运行时）允许主线程继续运行并执行其 finally 块，尽管它知道在控制权到达 finally 块时，另一个线程正位于 AppDomain 的未处理异常事件处理程序中。

为了强调这一点，请尝试更改延迟时间，使主线程的睡眠时间比事件处理程序更长。在那种场景中，finally 块将永远不会执行！在线程 1 醒来之前，进程就会被未处理的异常销毁。此外，根据抛出异常的线程是否由线程池创建，你也可能得到不同的结果。因此，最佳实践是避免所有可能的未处理异常，无论是发生在工作线程还是主线程中。

这与任务有何关系？如果你希望关闭系统时，系统中还有未完成的任务挂起怎么办？我们在下一节中讨论任务取消。

> **准则**

避免编写会在任何线程上产生未处理异常的程序。

考虑注册一个未处理异常事件处理程序，用于调试、日志记录和紧急关闭目的。

在应用程序关闭期间，取消未完成的任务，而不是允许它们运行。

### 取消任务

在本章前面，我们描述了为什么粗暴地中止一个线程以取消该线程正在执行的任务是一个坏主意。TPL（任务并行库）使用协作式取消，这是一种更礼貌、健壮且可靠的技術，用于安全地取消不再需要的任务。支持取消的任务会通过定期轮询 `CancellationToken` 对象（位于 System.Threading 命名空间中）来监视是否发出了取消请求。**清单 19.10** 演示了取消请求以及对请求的响应。**输出 19.6** 显示了结果。

#### **清单 19.10：使用 CancellationToken 取消任务**

```csharp
using System;
using System.Threading;
using System.Threading.Tasks;
using AddisonWesley.Michaelis.EssentialCSharp.Shared;

public class Program
{
	public static void Main()
	{
		string stars =
			"=".PadRight(Console.WindowWidth-1, '*');
		Console.WriteLine("Push ENTER to exit.");

		CancellationTokenSource cancellation_tokenSource=
			new CancellationTokenSource();
		// Use Task.Factory.StartNew<string>() for
		// TPL prior to .NET 4.5
		Task task = Task.Run(
			() =>
			{
				WritePi(cancellation_tokenSource.Token),
				cancellation_tokenSource.Token);
		}

		// Wait for the user's input
		Console.ReadLine();

		cancellation_tokenSource.Cancel();
		Console.WriteLine(stars);
		task.Wait();
		Console.WriteLine();
	}

	private static void WritePi(
		CancellationToken cancellation_token)
	{
		const int batchSize = 1;
		string piSection = string.Empty;
		int i = 0;

		while (!cancellation_token.IsCancellationRequested || i == int.MaxValue)
		{
			piSection = PiCalculator.Calculate(
				batchSize, (i++) * batchSize);
			Console.Write(piSection);
		}
	}
}
```

![](img/ef6a8a417630b222bfb3f3b949facff0_847_0.png)

#### **输出 19.6**

Push ENTER to exit.
3.141592653589793238462643383279502884197169399375105820974944592307816
40628620899862803482534211706798214808651328230664709384460955058223172
5359408128481117450\n***********************************************
2

在启动任务后，`Console.Read()` 阻塞了主线程。与此同时，任务继续执行，计算圆周率的下一位数字并将其打印出来。一旦用户按下回车键，执行流会遇到对 `CancellationTokenSource.Cancel()` 的调用。在清单 19.10 中，我们将对 `task.Cancel()` 的调用与对 `task.Wait()` 的调用分开，并在中间打印一行星号。这一步的目的是表明，在观察到取消令牌之前，很可能还会发生一次额外的迭代——因此，**输出 19.6** 中星号后面多了一个 2。出现 2 的原因在于，`CancellationTokenSource.Cancel()` 不会粗暴地阻止任务执行。任务会继续运行，直到它检查该令牌，当它看到令牌的所有者正在请求取消该任务时，它会礼貌地关闭。

`Cancel()` 调用实际上设置了从 `CancellationTokenSource.Token` 复制的所有取消令牌上的 `IsCancellationRequested` 属性。不过，有几点需要注意：

- 传递给异步任务的是 `CancellationToken`，而不是 `CancellationTokenSource`。`CancellationToken` 允许轮询取消请求；`CancellationTokenSource` 提供令牌并在取消时发出信号（参见图 19.3）。通过传递 `CancellationToken` 而不是 `CancellationTokenSource`，我们不必担心 `CancellationTokenSource` 上的线程同步问题，因为后者仅对原始线程可访问。
- `CancellationToken` 是一个结构体，因此它是按值复制的。`CancellationTokenSource.Token` 返回的值会产生令牌的一个副本。由于 `CancellationToken` 是值类型且创建了一个副本，因此对 `CancellationTokenSource.Token` 的访问是线程安全的——它仅在 `WritePi()` 方法内部可用。

![](img/ef6a8a417630b222bfb3f3b949facff0_849_0.png)

#### **图 19.3：CancellationTokenSource 和 CancellationToken 类图**

为了监视 `IsCancellationRequested` 属性，一个 `CancellationToken` 的副本（从 `CancellationTokenSource.Token` 获取）被传递给任务。在清单 19.9 中，我们随后会不时检查 `CancellationToken` 参数上的 `IsCancellationRequested` 属性；在这种情况下，我们在每次数字计算后进行检查。如果 `IsCancellationRequested` 返回 true，while 循环将退出。与线程中止不同，后者基本上会在随机点抛出异常，我们通过正常的控制流退出循环。我们通过频繁轮询来保证代码对取消请求的响应性。

关于 `CancellationToken` 的另一点需要注意的是重载的 `Register()` 方法。通过此方法，你可以注册一个操作，该操作将在令牌被取消时调用。换句话说，调用 `Register()` 方法相当于订阅了对应 `CancellationTokenSource` 的 `Cancel()` 上的监听委托。

鉴于在此程序中，完成前取消是预期行为，清单 19.9 中的代码不会抛出 `System.Threading.Tasks.TaskCanceledException`。因此，`task.Status` 将返回 `TaskStatus.RanToCompletion`——这表明任务的工作实际上已被取消这一事实没有指示。在此示例中，无需这样的指示；然而，TPL

