
## 2. 在资源管理器中，打开 `GraphDemo` 应用程序，展开 `MainPage.xaml`。在文件顶部添加以下 `using System.Threading.Tasks;`：

``` 
using System.Threading.Tasks;
```

## 3. 定位到 `generateGraphData` 方法。它如下：

``` 
private void generateGraphData(byte[] data)
{
    double a = pixelWidth / 2;
    double b = a * a;
    double c = pixelHeight / 2;
    for (double x = 0; x < a; x++)
    {
        double s = x * x;
        double p = Math.Sqrt(b - s);
        for (double i = -p; i < p; i += 3)
        {
            double q = (r - 1) * Math.Sin(24 * r);
            double y = i / 3 + (q * c);
            plotXY(data, (int)(x + pixelWidth / 2), (int)(y + pixelHeight / 2));
        }
    }
}
```

## 4. 将局部变量定义和循环体中的代码剪切，并创建一个名为 `calculateData` 的新 void 方法，代码如下。`calculateData` 方法应接受一个名为 `x` 的整数参数和一个名为 `data` 的字节数组。此外，将 `generateGraphData` 方法中声明局部变量 `a`、`b` 和 `c` 的语句移动到 `calculateData` 方法的开头。以下代码显示了 `generateGraphData` 方法删除了这些代码并添加了 `calculateData` 方法（现在不要尝试编译此代码）：

点击此处查看图片

``` 
private void generateGraphData(byte[] data)
{
}
```

``` 
private void calculateData(int x, byte[] data)
{
    double a = pixelWidth / 2;
    double b = a * a;
    double c = pixelHeight / 2;
}
```

```cs
for (double i = -p; i < p; i += 3)
{
    double r = Math.Sqrt(s * i * i) / a;
    double q = (r - 1) * Math.Sin(24 * r);
    double y = i / 3 + (q * c);
    plotXY(data, (int)(-x + (pixelWidth / 2)), (int)(y + (pixelHeight / 2)));
    plotXY(data, (int)(x + (pixelWidth / 2)), (int)(y + (pixelHeight / 2)));
}
```

## 6. 在 `generateGraphData` 方法中，将 `for` 循环替换为下面加粗显示的语句，该语句调用了静态 `Parallel.For` 方法：

点击此处查看代码图片

```cs
private void generateGraphData(byte[] data)
{
    Parallel.For(0, pixelWidth / 2, x => calculateData(x, data));
}
```

这是原始循环的并行等实现。它遍历从 0 到 `pixelWidth / 2 - 1` 的值。每次调用都由一个任务运行，并且每个任务可能会运行多次迭代。

`Parallel.For` 方法在它创建的所有任务完成工作后结束。请记住：`Parallel.For` 方法期望最后一个参数是一个接收单个整数参数的方法。它在调用该方法时会将当前循环索引作为参数传递。在此示例中，`calculateData` 方法并不符合所需的签名（它需要两个参数：一个整数和一个字节数组）。因此，代码使用了 Lambda 表达式，它作为一个适配器使用适当的参数调用 `calculateData` 方法。

## 7. 在 **Debug**（调试）菜单中，选择 **Start Debugging**（开始调试）以构建生成并运行应用程序。

## 8. 在 **Graph Demo** 窗口中，选择 **Plot Graph**（绘制图表）。当图表出现在 Graph Demo 窗口时，记录生成图表所需的时间。重复此操作几次以获得平均值。

你会注意到应用程序的运行速度至少与使用 `Task` 对象的之前的版本一样，可能更快，取决于你可用的 CPU 数量。

关闭 `GraphDemo` 应用程序并返回 Visual Studio。

## 9. 在 **Debug**（调试）菜单中，选择 **Relaunch Performance Profiler**（重新启动性能分析器）。应用程序再次启动，使用性能分析器跟踪 CPU 使用情况。

## 10. 多次选择 **Plot Graph**，并在选择之间等待几秒。

## 11. 关闭应用程序并返回 Visual Studio。

## 12. 在 CPU 使用率图中，检查 CPU 使用情况。在每次选择 **Plot Graph** 时，它都应该会达到 100% 的峰值。这是因为 `Parallel.For` 结构会自动利用所有可用处理器。因此，在双核机器上，它将使用两个处理器核心；依此类推。你不需要以任何方式修改代码来适应处理器架构的扩展。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_859_0.png)

# 何时不使用 Parallel 类

尽管事实如此，并且微软 .NET 开发团队付出了巨大努力，`Parallel` 类并不是魔法。你不能在没有经过适当考虑的情况下就使用它，并期望应用程序运行得显著更快且产生相同的结果。`Parallel` 类的目的是将代码中 CPU 密集型的独立区域并行化。

如果你没有运行 CPU 密集型代码，并行化它可能不会提高性能。在这种情况下，创建任务、在单独线程上运行任务以及等待任务完成的开销可能大于直接运行它的成本。额外的开销在每次调用方法时可能只占几毫秒，但你应该记住方法运行的次数。如果方法调用位于嵌套循环中并执行了数千次，那么所有这些微小的开销成本就会累积起来。通用规则是只有在值得这样做时才使用 `Parallel.Invoke`。你应该将计算密集型操作预留给 `Parallel.Invoke` 操作；否则，创建和管理任务的开销实际上会减慢应用程序的速度。

使用 `Parallel` 类的另一个关键考虑因素是并行操作应该是独立的。例如，如果你尝试使用 `Parallel.For` 来并行化一个迭代之间存在相互依赖关系的循环，结果将是不可预测的。要理解我的意思，请看以下代码。（你可以在 `ParallelLoop` 解决方案中找到该示例，它位于你文档文件夹中的 `Microsoft Press\VCSBS\Chapter23\ParallelLoop` 文件夹中。）

点击此处查看代码图片

```cs
using System;
using System.Threading;
using System.Threading.Tasks;
namespace ParallelLoop
{
    class Program
    {
        private static int accumulator = 0;
        static void Main(string[] args)
        {
            for (int i = 0; i < 100; i++)
            {
                AddToAccumulator(i);
            }
            Console.WriteLine($"Accumulator is {accumulator}");
        }

        private static void AddToAccumulator(int data)
        {
            if ((accumulator % 2) == 0)
            {
                accumulator += data;
            }
            else
            {
                accumulator -= data;
            }
        }
    }
}
```

此程序遍历从 0 到 99 的值，并带入每个值调用 `AddToAccumulator` 方法。`AddToAccumulator` 方法检查 `accumulator` 变量的当前值。如果是偶数，则将参数的值加到 `accumulator` 变量上；否则减去该值。在程序结束时，结果应该为 100。为了增加这个简单应用程序的并行程度，你可能会尝试用 `Parallel.For` 替换 `Main` 方法中的 `for` 循环，如下：

```cs
static void Main(string[] args)
{
    Parallel.For(0, 100, AddToAccumulator);
    Console.WriteLine("Accumulator is {accumulator}");
}
```

然而，无法保证创建的任务会按特定顺序执行。代码不是线程安全的，因为运行任务的多个线程可能会修改 `accumulator`。如果你对 `AddToAccumulator` 方法进行如下加粗修改，将得到不同的结果：

点击此处查看代码图片

```cs
private static void AddToAccumulator(int data)
{
    if ((accumulator % 2) == 0)
    {
        accumulator += data;
        Thread.Sleep(10); // 等待 10 毫秒
    }
    else
    {
        accumulator -= data;
    }
}
```

`Thread.Sleep` 方法只是让当前线程等待指定。这种修改模拟了线程上的额外处理。它还影响了 `Parallel` 类调度任务的方式，任务现在在不同的线程上运行，导致产生不同的值。如果你运行多次应用程序，将得到不同的结果。

通用规则是，只有当你能保证循环的每次迭代都是独立的并且经过彻底测试时，才使用 `Parallel.For` 和 `Parallel.ForEach`。类似的考虑也适用于 `Parallel.Invoke`；只有当方法调用是独立的且应用程序不依赖它们按特定顺序运行时才使用此结构。

# 取消任务和处理异常

执行长时间运行的应用程序的一个常见需求是在时停止这些操作。然而，你不应该直接中止任务，因为这会导致应用程序中的数据处于不确定状态。相反，`Task` 类实现了协作取消策略。

协作取消允许任务选择一个合适的停止处理点，并在必要时撤销在此之前已执行的任何工作。

## 协作取消的机制

协作取消基于取消令牌的概念。取消令牌是一个代表取消一个或多个任务请求的结构。任务的方法应该包含一个 `System.Threading.CancellationToken` 参数。想要取消任务的应用程序将该参数的 `IsRequested` 属性设置为 `true`。运行任务的方法可以在处理过程的各个点查询此属性。如果该属性在任何时候为 `true`，它就知道应用程序已请求取消任务。此外，方法知道它在此之前做了什么，因此在必要时可以撤销任何更改然后结束。或者，方法也可以简单地忽略请求并继续运行。

> 提示
> 你应该频繁地检查任务的取消令牌，但频率不要高到对任务性能产生不利影响。如果可能，你的目标应该是每 10 毫秒检查一次取消，但频率不能高于每毫秒一次。

应用程序通过创建 `System.Threading.CancellationSource` 对象并查询其 `Token` 属性来获取 `CancellationToken`。应用程序可以将此 `CancellationToken` 对象作为参数传递给由创建并运行的任务启动的任何方法。如果应用程序需要取消任务，它调用 `CancellationSource` 对象的 `Cancel` 方法。此方法会设置传递给所有任务的 `CancellationToken` 的 `IsCancellationRequested` 属性。

代码示例了如何创建取消令牌并使用它取消任务。`initiateTasks` 方法实例化 `cancellationSource` 变量，并返回通过该变量可用的 `CancellationToken` 对象的引用。代码创建并运行了一个执行 `doWork` 方法的任务。稍后，代码调用 `cancel source` 对象的 `Cancel` 方法，这会设置取消令牌。`doWork` 方法查询取消令牌的 `IsCancellationRequested` 属性。如果该属性被设置，方法将终止；否则，它将继续运行。

点击此处查看代码图像

```
public class MyApplication
{
    // 创建并管理任务的方法
    private void initiateTasks()
    {
        // 创建取消令牌源并获取取消令牌
        CancellationSource cancellationSource = new CancellationSource();
        CancellationToken cancellationToken = cancellationSource.Token;
        // 创建任务并启动其运行 doWork 方法
        Task myTask = Task.Run(() => doWork(cancellationToken));
    }
}
```

```
...
if (...)
{
    // 取消任务
    cancellationTokenSource.Cancel();
}
...
```

```
// 任务运行的方法
private void doWork(CancellationToken token)
{
    // 如果应用程序已设置取消令牌，则完成处理
    if (token.IsCancellationRequested)
    {
        // 清理并完成
        return;
    }
    // 如果任务未被取消，则正常继续运行
}
```

除了对取消处理提供高程度的控制外，这种方法还可以扩展到任意数量的任务。你可以启动多个任务并将相同的 `CancellationToken` 对象传递给其中的每一个任务。如果你调用 `CancellationSource` 对象的 `Cancel` 方法，每个任务都会检查 `IsCancellationRequested` 属性是否已设置并相应地进行。

你还可以使用 `Register` 方法向取消令牌注册一个回调方法（以 `Action` 委托的形式存在）。当应用程序调用相应的 `CancellationSource` 对象的 `Cancel` 方法时，该回调将会运行。然而，你无法保证此方法的执行时机。它必须在任务执行自己的取消处理之前或之后执行，甚至在该处理过程中执行。

点击此处查看代码图像

```
...
cancellationToken, Register(doAdditionalWork);
...
private void doAdditionalWork()
{
```

```
// 执行额外的取消处理
)
```

在下一个练习中，你将为 `GraphDemo` 应用程序添加取消功能。

# 为 GraphDemo 应用程序添加取消功能

- 1. 使用 Visual Studio 2022 打开 `GraphDemo` 解决方案，它位于你文档文件夹中的 `\Microsoft Press\VCSB\Chapter 23\GraphDemo With Cancellation` 文件夹。这是之前练习中 `GraphDemo` 应用程序的完成副本，它使用任务来提高处理吞吐量。用户界面还包含一个用户可以选择的按钮，用于停止计算图表数据的任务。此按钮运行 `cancelButton_Click` 方法。此外，增加了 `pixelWidth` 和 `imageHeight` 变量的大小，以便以更高的分辨率绘制图表并并了生成图表数据所需的时间。（如果你计算机上的可用内存小于 8 GB，则可能需要减小这些变量的值）。

> 重要
> 由于内存要求的增加，在尝试运行此应用程序之前，请确保你已在 Visual Studio 工具栏中选择了 x64 平台。

- 2. 在解决方案管理器中，在 `GraphDemo` 项目中，双击 `MainPage.xaml` 以在设计视图窗口中显示表单。注意表单左侧窗格中出现的 Cancel 按钮。

- 3. 在代码和编辑器窗口中打开 `MainPage.xaml.cs` 文件并找到 `cancelButton_Click` 方法。此方法在用户选择 Cancel 时运行。目前它是空的。

- 4. 在文件顶列表中添加以下 `using` 指令：

`using System.Threading;`

协作取消所使用的类型位于此命名空间。

- 5. 在 `MainPage` 类中添加一个名为 `tokenSource` 的 `CancellationTokenSource` 字段并将其初始化为 `null`，如下加粗代码所示：
