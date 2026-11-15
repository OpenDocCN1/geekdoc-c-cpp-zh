
线程的分配与释放。其结果是，Tasks 使用的底层线程是共享资源，预期任务会协作并及时归还线程，以便其他请求可以使用同一共享资源。

但是，如果开发者知道某个 Task 将长时间运行并长期占用底层线程资源，开发者需要通知线程池，该共享线程短期内不太可能被归还。这样，线程池就可以增加为任务创建专用线程的可能性，而不是从共享线程中获取一个。要实现这一点，在调用 StartNew() 时使用 TaskCreationOptions.LongRunning 选项，如清单 18.7 所示。

## 清单 18.7：协作式执行长时间运行的任务

```
using System.Threading.Tasks;

// ...

Task task = Task.Factory.StartNew(
    () =>
    WritePI(cancellationTokenSource.Token),
    TaskCreationOptions.LongRunning);

// ...
```

从技术角度看，TaskCreationOptions.LongRunning 实际上是调度器需要考虑的内容。但是，由于默认调度器是 ThreadPoolTaskScheduler，因此是线程池考虑了长时间运行参数。

## 释放 Task

在迄今为止依赖 Task 的清单中，我们通常调用任务的 Wait() 方法，以确保程序在任务完成执行之前不会退出。这符合 TPL 内置的协作式取消方法，因为我们不会在任务完成执行之前关闭程序。但是，如果程序在任务完成之前退出，会发生什么情况？

如果在应用程序开始退出时 Task 仍在运行，Task 依赖的底层线程将由 CLR 中止。因此，中止可能导致的任何不良影响都可能在应用程序退出时发生。更可取的方法是协作式取消，即 Task 支持取消，应用程序调用取消并等待任务完成。

请注意，Task 也支持 IDisposable。这是支持 Wait() 函数所必需的。Wait() 依赖于 WaitHandle，由于 WaitHandle 支持 IDisposable，因此 Task 也遵循最佳实践支持 IDisposable。但是，读者会注意到，前面的代码示例既不包含 Dispose() 调用，也不通过 using 语句隐式依赖此类调用。从技术上讲，调用 Dispose() 会是更好的代码，因此通常应尽合理努力这样做。

虽然任务实例化通常应包含相应的 Dispose() 调用，如果没有它，对 Wait() 的任何调用都可能导致未调用 Dispose() 的 WaitHandle 实例，但遗漏此调用并非关键。例如，本章中的清单不包含 Task.Dispose() 调用，而是依赖于程序退出时自动调用 WaitHandle 终结器。在这些示例中，任何 Dispose() 调用都无关紧要，因此为了阐述清晰而省略了它。但是，从技术上讲，它应该存在，开发者通常应包含它，除非代码变得难看，以至于依赖终结化队列是一种可接受的权衡。虽然调用 Dispose() 确实可以减轻后续对终结化队列的压力，除非存在大量的 Task 和相应的 WaitHandle，否则不尽快调用 Dispose() 也不会消耗显著资源。因此，让终结化负责资源清理并非不合理——例如，在希望使用“发射即忘”调用模式的情况下。

## 并行执行迭代

考虑 for 循环语句及使用此类循环的以下代码（参见清单 18.8 和相应的输出 18.6）。该清单调用一个方法来计算 pi 的一部分，其中第一个参数是位数（BatchSize），第二个参数是起始位数（i * BatchSize）。实际计算与讨论无关，因此完整清单出现在附录中。然而，使其非常适合多线程的一个特点是，计算可以拆分成多个部分。

## 清单 18.8：使用 for 循环同步分段计算 pi

```
using System;

const int TotalDigits = 100;
const int BatchSize = 10;

class Program
{
    void Main()
    {
        string pi = null;
        int iterations = TotalDigits / BatchSize;
        for (int i = 0; i < iterations; i++)
        {
            pi += PiCalculator.Calculate(
                BatchSize, i * BatchSize);
        }

        Console.WriteLine(pi);
    }
}
```

```
using System;

class PiCalculator
{
    public static string Calculate(int digits, int startingAt)
    {
        // ...
    }

    // ...
}
```

## 输出 18.6:

```
> 3.141592653589793238462643383279502884197169399375105820974944592307816
40628620899862803482534211706798214808651328230664709384460955058223172
5359408128481117450284102701938521105559644622948954930381964428810975
6659334461284756482337867831652712019091456485669234603486104543266482
1393607260249141273724587006606315588174881520920962829254091715364367
892590360011330530548820466521384146951941511609433057270365759591953
092186117381932611793105118548074462379962749567351885752724891227938
18301194912...
```

for 循环同步且按顺序执行每次迭代。但是，由于 pi 计算算法将 pi 计算拆分为独立的部分，只要所有部分仍按顺序追加，就不需要按顺序完成各个部分。因此，想象一下，如果可以让迭代同时运行并相互重叠，因为每个处理器可以获取一个迭代，并与其他处理器执行其他迭代并行执行它。鉴于迭代的同时执行，我们可以根据处理器数量越来越多地减少执行时间。

```
Parallel.For()
```

.NET 4 通过 System.Threading.Tasks.Parallel 上的 API 包含了此类并行 for 功能，如清单 18.9 所示。

## 清单 18.9：并行分段计算 pi 的 for 循环

```
using System;
using System.Threading;
// ...
class Program
{
    void Main()
    {
        string pi = null;
        int iterations = TotalDigits / BatchSize;
        string[] sections = new string[iterations];
        Parallel.For(0, iterations, (i) =>
        {
            sections[i] += PiCalculator.Calculate(
                BatchSize, i * BatchSize);
        });
        pi = string.Join("", sections);
        Console.WriteLine(pi);
    }
}
```

清单 18.9 的输出与输出 18.6 相同；但是，执行时间要快得多（假设有多个 CPU）。Parallel.For() API 的设计旨在与标准 for 循环相似。第一个参数是 fromInclusive 值，第二个是 toExclusive 值，最后一个是要执行的 Action<int>。当为操作使用表达式语句（带花括号）时，代码看起来类似于 for 循环语句，只不过现在每次迭代都可能并行执行。

与 for 循环一样，对 Parallel.For() 的调用在所有迭代完成之前不会完成。换句话说，当执行到达 string.Join() 语句时，所有 pi 部分都已计算完毕。

重要的是要注意，合并各个 pi 部分的代码不再发生在迭代（操作）内部。由于 pi 计算的各个部分很可能不会按顺序完成，因此每次迭代完成时追加一个部分可能会导致它们按顺序不当地追加。即使顺序不是问题，仍然存在潜在的竞态条件，因为 += 运算符不是原子的。为了解决这两个问题，每个 pi 部分都存储在数组中，且不会有两个或更多迭代同时访问数组中的同一个元素。只有在所有 pi 部分都计算完毕后，string.Join() 才会合并它们。换句话说，我们将部分的连接推迟到 Parallel.For() 循环完成之后。这避免了由尚未计算的部分或部分按顺序不当连接引起的任何竞态条件。

```
Parallel.ForEach()
```

循环的并行执行不仅限于 for 构造。Parallel.ForEach() 为 foreach 循环提供了类似的功能，如清单 18.10 所示。

## 清单 18.10：foreach 循环的并行执行

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
        IEnumerable<string> files = Directory.GetFiles(
            directoryPath, searchPattern,
            SearchOption.AllDirectories);

        Parallel.ForEach(files, (fileName) =>
        {
            Encrypt(fileName);
        });
    }
}
