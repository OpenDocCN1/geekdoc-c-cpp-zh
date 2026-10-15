
清单18.25的输出与输出18.8相同；然而，如果你有多颗CPU，执行时间会显著加快（如果没有，可能会变慢）。`Parallel.For()` API的设计目标是与标准的`for`循环相似。第一个参数是`fromInclusive`值，第二个是`toExclusive`值，最后一个是在循环体中执行的`Action<int>`。当使用表达式lambda作为操作时，代码看起来与`for`循环语句相似，只是现在每次迭代可能并行执行。与`for`循环一样，对`Parallel.For()`的调用要等到所有迭代完成后才会返回。换句话说，当执行到达`string.Join()`语句时，圆周率的所有部分都已经计算完毕。

请注意，在清单18.25中，用于合并圆周率各部分（即每次迭代中的操作）的代码不再出现在循环内部。由于圆周率计算的各个部分很可能不会按顺序完成，所以在迭代完成时追加一个部分很可能会导致它们乱序追加。即使顺序不是问题，仍然存在潜在的竞争条件，因为`+=`运算符不是原子的。为了解决这两个问题，圆周率的每个部分都存储到一个数组中，并且任何两个或更多迭代不会同时访问数组中的单个元素。只有当圆周率的所有部分都计算完成后，`string.Join()`才会将它们合并。换句话说，我们将拼接各部分的操作推迟到`Parallel.For()`循环完成之后。这避免了由于部分尚未计算或部分乱序拼接而导致的任何竞争条件。

TPL使用与任务调度相同的线程池技术来确保并行循环的良好性能：它会尽力确保CPU不被过度调度，等等。

## 准则

当所执行的计算可以轻松拆分为许多相互独立且与处理器绑定的计算，并且可以在任何线程上以任意顺序执行时，请使用并行循环。

TPL还提供了`foreach`语句的类似并行版本，如清单18.26所示。

### 清单18.26：`foreach`循环的并行执行

```
using System;

using System.Collections.Generic;

using System.IO;

using System.Threading.Tasks;

class Program

{

    // ...

    static void EncryptFiles(

        string directoryPath, string searchPattern)

    {

        IEnumerable<string> files = Directory.EnumerateFiles(

            directoryPath, searchPattern,

            SearchOption.AllDirectories);

        Parallel.ForEach(files, (fileName) =>

        {

            Encrypt(fileName);

        });

    }

    // ...

}
```

在此示例中，我们调用一个方法，对`files`集合中的每个文件进行加密。它并行执行，执行的线程数由TPL根据效率来确定。

## 高级主题

### TPL如何调整其自身性能

TPL中的默认调度器面向线程池，采用多种启发式策略来确保在任一时刻执行适当数量的线程。其中使用的两种启发式策略是“爬山算法”和“工作窃取”。

爬山算法涉及创建线程来运行任务，然后监控这些任务的性能，以尝试通过实验确定增加线程开始使性能变差的临界点。一旦达到该点，线程数就可以减少到产生最佳性能的数量。

TPL将等待执行的“顶级”任务与特定线程关联。但是，如果运行在线程上的任务本身创建了另一个任务，则新创建的任务会自动与该线程关联。当新的“子”任务最终被调度运行时，它通常在与创建它的任务相同的线程上运行。工作窃取算法会识别出待处理工作量异常大或异常小的线程；关联任务过少的线程有时会从等待运行任务过多的线程那里“窃取”尚未执行的任务。

这些算法的关键特性在于，它们使TPL能够动态调整自身性能，以缓解处理器过度调度和调度不足，并在可用处理器之间平衡工作负载。

TPL通常能很好地调整自身性能，但你可以通过提供有关最佳行动方案的提示来帮助它做得更好。前面“长时间运行的任务”一节中描述的指定`TaskCreationOptions.LongRunning`选项就是这样一个提示。你还可以明确告诉任务调度器你认为多少个线程最适合服务一个并行循环；有关详细信息，请参阅题为“并行循环选项”的高级主题。

## 初学者主题

### 使用`AggregateException`处理并行循环异常

我们已经知道，TPL会捕获与任务关联的异常并将其保存在`AggregateException`中，因为给定任务可能会从它的子任务中获得多个异常。并行执行循环时也是如此：每次迭代都可能产生异常，因此需要将异常收集到一个聚合异常中。请考虑清单18.27中的示例及其输出（输出18.9）。

### 清单18.27：并行迭代的未处理异常

```
using System;

using System.Collections.Generic;

using System.IO;

using System.Threading;

using System.Threading.Tasks;

class Program

{

    // ...

    static void EncryptFiles(

        string directoryPath, string searchPattern)

    {
```

## 取消并行循环

与任务不同，任务需要显式调用才能阻塞直到完成，而并行循环并行执行迭代，但在整个并行循环完成之前，它本身不会返回。因此，取消并行循环通常涉及从执行并行循环的线程之外的线程调用取消请求。在清单18.28中，我们使用`Task.Run()`调用`Parallel.ForEach<T>()`。这样，循环不仅并行执行，而且异步执行，允许代码提示用户“按ENTER退出”。

### 清单18.28：取消并行循环

```
using System;

using System.Collections.Generic;

using System.IO;

using System.Threading;

using System.Threading.Tasks;

public class Program

{

    // ...

    static void EncryptFiles(

        string directoryPath, string searchPattern)

    {

        string stars =

            "*".PadRight(Console.WindowWidth - 1, '*');

        IEnumerable<string> files = Directory.GetFiles(

            directoryPath, searchPattern,

            SearchOption.AllDirectories);

        CancellationTokenSource cts =

            new CancellationTokenSource();

        ParallelOptions parallelOptions =

            new ParallelOptions

            { CancellationToken = cts.Token };

        cts.Token.Register(

            () => Console.WriteLine("Cancelling..."));

        Console.WriteLine("Push ENTER to exit.");

        // Use Task.Factory.StartNew<string>() for

        // TPL prior to .NET 4.5

        Task task = Task.Run(() =>

        {

            try

            {

                Parallel.ForEach(

                    files, parallelOptions,

                    (fileName, loopState) =>

                    {

                        Encrypt(fileName);

                    });

            }

            catch (OperationCanceledException) { }

        });

        // Wait for the user's input

        Console.Read();

        // Cancel the query

        cts.Cancel();

        Console.Write(stars);

        task.Wait();

    }

}
```
