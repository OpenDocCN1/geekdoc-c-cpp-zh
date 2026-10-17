
因此，在这种情况下，两个任务分别分配到了不同的线程。两个任务的状态均为 Running，它们通过自动生成的 lambda 名称和编号 `<lambda12>()` 和 `<lambda13>()` 来标识。发生这种情况是因为代码使用 lambda 表达式生成与每个任务关联的委托。

如果双击某个任务名称，IDE 将显示所选任务接下来要执行的语句。请记住，分配给这些任务的线程和主线程正在并发运行，并且根据可用的硬件资源和调度程序所做的决策，它们可能并行运行。

> CLR 任务调度程序会尝试从最合适的底层线程中窃取工作，具体方式是占用空闲线程的时间。它还可以决定创建新线程来支持任务的执行。然而，此过程并不能保证底层线程会并行运行，即使所需数量的逻辑核心可用。操作系统调度程序会在数十个或数百个计划从可用核心接收处理器时间的线程之间分配核心。这就是为什么相同的并发代码在同一硬件配置上会以不同的并行级别和不同的并发执行时间运行。

你可以检查每个不同的并发或并行任务的情况。你拥有与早期 Visual Basic 版本为线程提供的类似选项，但信息更完善，因为你可以检查任务是处于已调度状态还是等待死锁状态。你还可以像使用任何其他 Visual Basic IDE 功能一样，对窗口中显示的信息进行排序和分组。

“并行任务”网格包含一个名为“线程分配”的列。该数字是“线程”窗口中显示的 ID。因此，你可以知道哪个托管线程正在支持某个任务的执行。你还可以检查每个不同线程的下一条语句和其他详细信息。为此，请选择“调试”⇨“窗口”⇨“线程”（`Ctrl + Alt + H`）。IDE 将显示如图 33-12 所示的“线程”对话框，其中包含所有线程的列表、它们的类别和位置。

![](img/d99870e80390742f93963da7be0b2e61_1082_1.png)

## 图 33-12

> 虽然在黑白截图中不可见，但 Threads 对话框使用不同的颜色和名称来区分主线程——通常运行 UI 代码或支持 Main 子程序的线程（主线程，绿色方块），以及其他线程（工作线程，黄色方块）。运行中的任务从工作线程窃取工作，而不是从主线程。因此，任务必须使用委托来更新 UI，以便在此目的下在主线程中运行代码。

可视化任务与线程之间关系的一种更简单的方法。你可以选中 Debug ▸ Windows ▸ Parallel Stacks（`Ctrl + Shift + D, S`）。IDE 将显示图 33-13 所示的 Parallel Stacks 窗口，其中包含所有任务或线程的图表、其状态以及它们的关系。默认视图为 Threads。

![](img/d99870e80390742f93963da7be0b2e61_1083_0.png)

图 33-13

图表右侧的两个线程正在运行由两个任务调度的代码。每个线程都显示其调用堆栈。支持 `Module1.<lambda12>` 的线程正在运行 `GenerateAESKeys` 子程序——具体来说，是 `ConvertToHexString` 子程序调用中的代码。支持 `Module1.<lambda13>` 的线程正在运行 `GenerateMD5Hashes` 子程序，并且显示了许多原生到托管代码的转换以及反之亦然。该图表以极高的细节程度指示每个线程正在做什么。

你可以将左上角组合框的值从 Threads 改为 Tasks，IDE 将显示一个包含所有任务的图表，包括其状态、关系和调用堆栈，如图 33-14 所示。

![](img/d99870e80390742f93963da7be0b2e61_1083_1.png)

图 33-14

### 等待任务完成

在某个时刻，你需要等待由异步执行启动的某些任务完成。以下行调用 `Task.WaitAll` 方法，该方法将等待作为 ParamArray 接收的 Task 实例，以逗号分隔。此方法具有同步执行，这意味着主线程不会继续执行下一条语句，直到作为参数接收的 Task 实例完成其执行。

```
Task.WaitAll(t1, t2)
```

### LISTING 33-14 (continued)

```
If t2.IsCanceled Then
    Console.WriteLine("The task running GenerateMD5HashesCancel was cancelled.")
End If
' Display the results and wait for the user to press a key
Console.ReadLine()
End Sub
```

`GenerateAESKeysCancel` 的第一行将在其取消已被请求时抛出上述异常。这样，如果此时不必要，它就不会开始循环。

```
ct.ThrowIfCancellationRequested()
```

此外，在循环的每次迭代之后，新的代码检查令牌的 `IsCancellationRequested`。如果为 True，它将调用 `ThrowIfCancellationRequested` 方法。在调用此方法之前，当 `IsCancellationRequested` 为 True 时，可以根据需要添加清理代码：

```
If ct.IsCancellationRequested Then
' It is important to add clean up code here when necessary
ct.ThrowIfCancellationRequested()
End If
```

这段额外代码为循环的每次迭代增加了少量开销。然而，它增加了观察 `OperationCanceledException` 并将其令牌与与 Task 实例关联的令牌进行比较的能力。如果它们相同并且其 `IsCanceledProperty` 为 True，Task 实例将理解存在取消请求并过渡到 Canceled 状态，中断其执行。当有代码等待已取消的 Task 实例时，这也会生成自动的 `TaskCanceledException`，该异常被包装在 `AggregateException` 中。

在这种情况下，主子程序创建一个 `CancellationTokenSource`，`cts`，和一个 `Cancellation Token`，`ct`：

```
Dim cts As New System.Threading.CancellationTokenSource()
Dim ct As System.Threading.CancellationToken = cts.Token
```

`CancellationTokenSource` 能够发起取消请求，而 `CancellationToken` 将其传达给异步操作。

需要将 `CancellationToken` 作为参数发送给每个任务委托；因此，代码使用 `TaskFactory.StartNew` 方法的定义之一。以下行使用相同的 `CancellationToken` 实例（`ct`）作为参数创建并启动两个 Task 实例及其关联的操作：

```
Dim t1 = Task.Factory.StartNew(Sub() GenerateAESKeysCancel(ct), ct)
Dim t2 = Task.Factory.StartNew(Sub() GenerateMD5HashesCancel(ct), ct)
```

前面的行使用 `Task` 类的 `Factory` 属性检索 `TaskFactory` 实例，该实例可用于创建比直接实例化 `Task` 类所提供的选项更多的任务。在这种情况下，它使用 `StartNew` 方法，该方法在功能上等同于使用其构造函数之一创建 Task 然后调用 `Start` 以安排其执行。

然后，代码调用 `Sleep` 方法使主线程休眠一秒。此方法将当前线程挂起指定的时间——在本例中指定为毫秒的 Integer：

```
Threading.Thread.Sleep(1000)
```

> 主线程保持挂起一秒，但支持任务执行的线程不会被挂起。因此，任务将被安排开始执行。

一秒后，主线程通过 `CancellationTokenSource` 实例的 `Cancel` 方法向两个任务发出取消请求：

```
cts.Cancel()
```

取消令牌在由 Task 实例启动的两个委托中被评估，如前所述。

添加几行代码，很容易取消异步操作。然而，添加必要的清理代码非常重要。

一个 `Try...Catch...End Try` 块包围了对 `Task.WaitAll` 的调用。因为对两个任务都发出了取消请求，所以会出现两个良性的 `OperationCanceledException` 异常。

两个任务的 `IsCanceled` 属性都将为 True。检查此属性，你可以在任务被取消时添加代码。

### 处理任务抛出的异常

由于许多任务并行运行，因此可能并行发生许多异常。Task 实例也使用之前解释的 `System.AggregateException` 类处理一组异常。

Listing 33-15 显示了在 `GenerateAESKeysCancel` 子程序中添加未处理异常的高亮行。

注释掉请求对两个任务取消的代码：

```
' cts.Cancel()
```

**LISTING 33-15: An unhandled exception in the subroutine called by an asynchronous delegate**

```vb
Sub GenerateAESKeysCancel(ByVal ct As System.Threading.CancellationToken)
    ct.ThrowIfCancellationRequested()
    Dim sw = Stopwatch.StartNew()
    Dim aesM As New AesManaged()
    Dim result() As Byte
    Dim hexString As String
    For i As Integer = 1 To NUM_AES_KEYS
        aesM.GenerateKey()
        result = aesM.Key
        hexString = ConvertToHexString(result)
        ' Console.WriteLine("AES: " + hexString)
        If (sw.Elapsed.Seconds > 0.5) Then
            Throw New TimeoutException("GenerateAESKeysCancel is taking more than 0.5 seconds to complete.")
        End If
        If ct.IsCancellationRequested Then
            ct.ThrowIfCancellationRequested()
        End If
    Next
    Debug.WriteLine("AES: " + sw.Elapsed.ToString())
End Sub
```

向 Main 子程序添加以下行：

```
If t1.IsFaulted Then
    For Each innerEx As Exception In t1.Exception.InnerExceptions
        Debug.WriteLine(innerEx.ToString())
        ' Do something else considering the innerEx Exception
    Next
End If
```

由于 `t1` 中存在未处理的异常，其 `IsFaulted` 属性为 True。因此，`t1.Exception`，即 `AggregateException`，包含在其关联委托执行期间发生的

一个或多个异常。检查 `IsFaulted` 属性后，可以遍历 `Exception` 的 `InnerExceptions` 只读集合中包含的每个单独异常。你可以根据导致任务无法完成的问题做出决策。Listing 33-16 显示了未处理异常的信息转换为字符串并发送到 Debug 输出。

### LISTING 33-16: Debug output with the exceptions found in the InnerExceptions collection

```
System.TimeoutException: GenerateAESKeysCancel is taking more than 0.5 seconds to complete.
    at ConsoleApplication3.Module1.GenerateAESKeysCancel(CancellationToken ct) in C:\Wrox\Professional_VB_2010\ConsoleApplication3\ConsoleApplication3\Module1.vb:line 427
    at ConsoleApplication3.Module1._Closure$__3._Lambda$__12() in C:\Wrox\Professional_VB_2010\ConsoleApplication3\ConsoleApplication3\Module1.vb:line 337
    at System.Threading.Tasks.Task.InnerInvoke()
    at System.Threading.Tasks.Task.Execute()
```

> 异步操作中的未处理异常通常是复杂的问题，因为有时需要执行重要的清理操作。例如，当发生异常时，你可能有部分结果，如果由于异常作业未完成，你可能必须删除这些值。因此，在使用任务时必须考虑清理操作。

### 从任务返回值

到目前为止，任务实例没有返回值；它们是运行子程序的委托。然而，也可以通过调用函数并使用 `Task(Of TResult)` 实例从任务返回价值，其中 `TResult` 必须替换为返回的类型。

Listing 33-17 显示了生成众所周知的 AES 密钥然后返回以作为参数之一接收的字符前缀（`prefix`）开头的密钥列表的新函数的代码。`GenerateAESKeysWithCharPrefix` 返回一个 `List` of `String`。

Main 子程序使用 `TaskFactory.StartNew` 方法的定义，但这次它从 `Task(Of TResult)` 实例而不是 Task 实例调用它。具体来说，它创建一个 `Task(Of List(Of String))` 实例，向任务委托发送 `CancellationToken` 作为参数：

```
Dim t1 = Task(Of List(Of String)).Factory.StartNew(Function()
    GenerateAESKeysWithCharPrefix(ct, "A"), ct)
```

委托是一个返回 `List(Of String)` 的函数，该值将在 `Task(Of Result)` 实例（`t1`）中通过其 `Result` 属性可用，在关联委托完成其执行并函数返回一个值之后。

主线程等待 `t1` 完成，然后检查它是否完成了其执行，检查之前解释的 Task 实例属性。

然后，它遍历由前一个任务中调用的函数返回的列表中的每个字符串，并在控制台上显示结果。它通过运行新的异步任务 `t2` 来完成这项工作。

### LISTING 33-17: Returning a list of String instances from a task

```
Function GenerateAESKeysWithCharPrefix(ByVal ct As System.Threading.CancellationToken, ByVal prefix As Char) As List(Of String)
    ct.ThrowIfCancellationRequested()
    Dim sw = Stopwatch.StartNew()
```
