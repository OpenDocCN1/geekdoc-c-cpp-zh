
不幸的是，异步委托调用模式使用的底层技术是一种用于分布式编程的已停止进一步开发的技术，即`remoting`。虽然`Microsoft`仍然支持异步委托调用的使用，并且在可预见的未来它将继续按今天的方式运行，但其性能特征在其他方法——即`Thread`、`ThreadPool`和`TPL`——面前是不理想的。鉴于这一现实，开发人员应优先考虑这些替代方案，而不是使用异步委托调用`API`实现新的开发。关于该模式的进一步讨论包含在下面的高级主题文本中，以便遇到它的开发人员能够理解其工作原理。

### ADVANCED TOPIC

### 异步委托调用详解

使用异步委托调用时，你不会使用对`Task`或`Thread`的显式引用进行编码。相反，你使用委托实例以及编译器生成的`BeginInvoke()`和`EndInvoke()`方法——其实现从`ThreadPool`请求线程。请考虑清单`C.7`中的代码。

**LISTING C.7: Asynchronous Delegate Invocation**

```
using System;

public class Program
{
    public static void Main(string[] args)
    {
        Console.WriteLine("Application started...");

        Console.WriteLine("Starting thread...");
        Func<int,string> workerMethod =
            PiCalculator.Calculate;
        IAsyncResult asyncResult =
            workerMethod.BeginInvoke(500, null, null);

        // Display periods as progress bar.
        while(!asyncResult.AsyncWaitHandle.WaitOne(
            100, false))
        {
            Console.Write('.');
        }
        Console.WriteLine();

        Console.WriteLine("Thread ending...");
        Console.WriteLine(
            workerMethod.EndInvoke(asyncResult));

        Console.WriteLine(
            "Application shutting down...");
    }
}
```

清单`C.7`的结果显示在输出`C.3`中。

**OUTPUT C.3**

```
Application started....
Starting thread....
....................
Thread ending....
3.14159265358979323846264338327950288419716939937510582097494459230781
64062862089986280348253421170679821480865132823066470938446095505623
7253594081284811174502841027019385211055596446229489549303819644288109
756659334461284756482337867831652712019091456485669234603486104543264
821339306026199461271237824646144913859102902214217521...
367892590360011330530548080466521384146951941511609433057270365759591
530921861173819326117931051185480744623799627495673518857272489122793
818301194912
Application shutting down....
```

`Main()`首先分配一个指向`PiCalculator.Calculate(int digits)`的`Func<int, string>`类型委托。

接下来，代码调用`BeginInvoke()`。此方法在线程池中的线程上启动`PiCalculator.Calculate()`方法，然后立即返回。这允许其他代码与`pi`计算并行运行。在此示例中，我们在等待`PiCalculator.Calculate()`方法完成时打印句点。

我们使用`IAsyncResult.AsyncWaitHandle.WaitOne()`在`asyncResult`上轮询委托的状态——与`APM`中可用的机制相同。因此，代码在`PiCalculator.Calculate()`方法执行期间每`100`毫秒向屏幕打印一个句点。

一旦等待句柄发出信号，代码就会调用`EndInvoke()`。与所有`APM`实现一样，将调用`BeginInvoke()`时返回的相同`IAsyncResult`引用传递给`EndInvoke()`很重要。在此示例中，`EndInvoke()`不会阻塞，因为我们在`while`循环中轮询线程状态，并在线程完成后才调用`EndInvoke()`。

清单`C.7`中的示例传递了一个整数并接收了一个字符串——这是`Func<int, string>`的签名。异步委托调用的关键特性是，将数据传入和传出目标调用是微不足道的；它与同步方法签名一致，就像在`APM`模式中一样。考虑一个包含`out`和`ref`参数的委托类型，如图`C.2`所示。（尽管常见，此示例故意不使用`Func`或`Action`，因为泛型不允许在类型参数上使用`ref`和`out`修饰符。）

```
System.IAsyncResult UpdateHandler.BeginInvoke(
    Object[] data, ref object value, out string text,
    AsyncCallback callback, object @object);

delegate bool UpdateHandlerFunc(
    object[] data, ref object value, out string text);

bool UpdateHandler.EndInvoke(
    ref object value, out string text);
```

**FIGURE C.2: Delegate Parameter Distribution to BeginInvoke() and EndInvoke()**

`BeginInvoke()`方法与委托签名匹配，除了额外的`AsyncCallback`和`object`参数。像`IAsyncResult`返回值一样，额外参数对应于指定回调和传递状态对象的标准`APM`参数。类似地，`EndInvoke()`方法与原始签名匹配，除了只有传出参数出现。由于`object[] data`仅为传入，因此它不会出现在`EndInvoke()`方法中。此外，由于`EndInvoke()`方法结束了异步调用，其返回与原始委托的返回匹配。

由于所有委托都包含`C#`编译器生成的`BeginInvoke()`和`EndInvoke()`方法，这些方法被异步委托调用模式使用，因此异步调用任何方法——尤其是使用`Func`和`Action`委托——变得相对容易。此外，对于调用方来说，无论`API`程序员是否显式实现了它，都很容易异步调用方法。

在`TPL`可用之前，异步委托调用模式的使用明显比替代方案更容易——这促使程序员在`API`未提供显式异步调用模式时使用它。然而，除了对`.NET 3.5`及更早框架的支持外，`TPL`的出现减少了使用异步委托调用方法的需求，如果有必要的话。

## 基于事件的异步模式¹

到目前为止，我们假设异步方法将返回一个任务；当任务的状态和结果被设置时，调用方会被通知异步工作已完成。这样做反过来也可能导致任务的完成异步执行。虽然这种模式很常见且功能强大，但它并不是处理异步性的唯一选择。值得注意的是，基于事件的异步模式（`EAP`）通常用于长时间运行的异步工作。

使用`EAP`的方法通常以`Async`结尾，返回`void`，并且没有`out`参数。`EAP`方法还通常接受一个对象或泛型参数，其中包含与异步工作关联的调用方确定的状态，有时它们接受取消令牌，如果异步工作可以取消的话。例如，如果我们有

```csharp
public void CalculateAsync<TState>(
    int digits,
    CancellationToken cancelToken
        = default(CancellationToken),
    TState userState
        = default(TState))
{
    SynchronizationContext.
        SetSynchronizationContext(
            AsyncOperationManager.
                SynchronizationContext);
    // Ensure the continuation runs on the current thread, so that
    // the event will be raised on the same thread that
    // called this method in the first place.
    TaskScheduler scheduler =
        TaskScheduler.
            FromCurrentSynchronizationContext();
    Task.Run(
        () =>
        {
            return PiCalculator.Calculate(digits);
        }, cancelToken)
        .ContinueWith(
            continueTask =>
            {
                Exception exception =
                    continueTask.Exception == null ?
                    continueTask.Exception :
                    continueTask.Exception.
                        InnerException;
                CalculateCompleted(
                    typeof(PiCalculator),
                    new CalculateCompletedEventArgs(
                        continueTask.Result,
                        exception,
                        cancelToken.IsCancellationRequested,
                        userState));
            }, scheduler);
}

public event
    EventHandler<CalculateCompletedEventArgs>
        CalculateCompleted = delegate { };

public class CalculateCompletedEventArgs
    : AsyncCompletedEventArgs
{
    public CalculateCompletedEventArgs(
        string value,
        Exception error,
        bool cancelled,
        object userState) : base(
            error, cancelled, userState)
    {
        Result = value;
    }

    public string Result { get; private set; }
}
```

在清单`C.8`中，与`async/await`方法一样，我们希望确保触发事件的延续任务始终在原始异步方法所在的同一线程上运行。为了实现这一目标，我们从`TaskScheduler`类获取同步上下文。由于这是一个控制台应用程序，当前线程没有同步（因此默认依赖线程池），所以清单`C.8`中首先创建了默认上下文。

如前所述，`EAP`（基于事件的异步模式，Event-based Asynchronous Pattern）方法通常用于长时间运行的异步操作。长时间运行的操作不仅在任务完成、失败或取消时提供通知，还经常会提供阶段性的进度更新。当用户界面以某种进度条或其他指示器显示长时间运行的异步操作的进度时，这类信息尤其有用。在`EAP`方法中，标准做法是将该方法与另一个名为`ProgressChanged`的事件（类型为`ProgressChangedEventHandler`）关联起来。

`EAP`方法及其关联事件（如果方法产生进度更新，也可以是多个事件）通常是实例成员，而不是静态成员。这使得支持多个并发操作变得更加容易，因为每个单独的操作都可以与不同的实例关联。

## 后台工作线程模式

另一种提供操作状态和取消可能性的模式是后台工作线程模式，它是`EAP`的一种具体实现。`.NET Framework 2.0`（或更高版本）包含一个用于编写此类模式的`BackgroundWorker`类。

清单`C.9`是该模式的一个示例——同样将`π`计算到指定的位数。

```csharp
}
}

private static void CalculatePi(
    object sender, DoWorkEventArgs eventArgs)
{
    int digits = (int)eventArgs.Argument;

    StringBuilder pi =
        new StringBuilder("3.", digits + 2);
    calculationWorker.ReportProgress(
        0, pi.ToString());

    // Calculate rest of pi, if required.
    if (digits > 0)
    {
        for (int i = 0; i < digits; i += 9)
        {
            // Calculate next i decimal places.
            int nextDigit =
                PiDigitCalculator.StartingAt(
                    i + 1);
            int digitCount =
                Math.Min(digits - i, 9);
            string ds =
                string.Format("{0:D9}", nextDigit);
            pi.Append(ds.Substring(0, digitCount));

            // Show current progress.
            calculationWorker.ReportProgress(
                0, ds.Substring(0, digitCount));

            // Check for cancellation.
            if (
                calculationWorker.CancellationPending)
            {
                // Need to set Cancel if you want to
                // distinguish how a worker thread completed--
                // i.e., by checking
                //RunWorkerCompletedEventArgs.Cancelled.
                eventArgs.Cancel = true;
                break;
            }
        }
    }

    eventArgs.Result = pi.ToString();
}

private static void UpdateDisplayWithMoreDigits(
    object sender,
    ProgressChangedEventArgs eventArgs)
{
    string digits = (string)eventArgs.UserState;
    Console.Write(digits);
}

static void Complete(
    object sender,
    RunWorkerCompletedEventArgs eventArgs)
{
    // ...
}

public class PiDigitCalculator
{
    // ...
}
```

### 建立模式

建立后台工作线程模式的步骤如下：
