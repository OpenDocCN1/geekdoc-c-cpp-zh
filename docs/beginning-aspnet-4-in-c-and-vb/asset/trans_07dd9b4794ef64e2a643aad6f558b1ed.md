
在线程的主方法 `ThreadMain()` 中，线程会调用 `WaitOne()` 来锁定信号量。请记住，信号量的计数为 4，因此可以有四个线程获取锁。线程 5 必须等待，在这里，600 毫秒的超时时间被定义为最长等待时间。如果等待时间结束后仍无法获取锁，线程会向控制台写入一条消息，并在循环中重复等待。一旦获取到锁，线程就会向控制台写入一条消息，休眠一段时间，然后释放锁。同样，在释放锁时，确保资源在所有情况下都能被释放非常重要。因此，`Semaphore` 类的 `Release()` 方法会在 `finally` 处理程序中调用。

```
static void ThreadMain(object o)
{
    SemaphoreSlim semaphore = o as SemaphoreSlim;
    Trace.Assert(semaphore != null, "o must be a Semaphore type");
    bool isCompleted = false;
    while (!isCompleted)
    {
        if (semaphore.Wait(600))
        {
            try
            {
                Console.WriteLine("Thread {0} locks the semaphore",
                    Thread.CurrentThread.ManagedThreadId);
                Thread.Sleep(2000);
            }
            finally
            {
                semaphore.Release();
                Console.WriteLine("Thread {0} releases the semaphore",
                    Thread.CurrentThread.ManagedThreadId);
                isCompleted = true;
            }
        }
        else
        {
            Console.WriteLine("Timeout for thread {0}; wait again",
                Thread.CurrentThread.ManagedThreadId);
        }
    }
}
```

运行应用程序时，可以看到，使用四个线程时，锁会立即被获取。ID 为 7 和 8 的线程必须等待。等待会在循环中持续进行，直到其他线程之一释放信号量。

```
Thread 3 locks the semaphore
Thread 4 locks the semaphore
Thread 5 locks the semaphore
Thread 6 locks the semaphore
Timeout for thread 8; wait again
Timeout for thread 7; wait again
Timeout for thread 8; wait again
Timeout for thread 7; wait again
Timeout for thread 7; wait again
Timeout for thread 8; wait again
Thread 3 releases the semaphore
Thread 8 locks the semaphore
Thread 4 releases the semaphore
Thread 7 locks the semaphore
Thread 5 releases the semaphore
Thread 6 releases the semaphore
Thread 8 releases the semaphore
Thread 3 releases the semaphore
Thread 7 releases the semaphore
Thread 4 releases the semaphore
Thread 5 releases the semaphore
Thread 6 releases the semaphore
All threads finished
```

## 事件

事件是下一组系统范围的同步资源。要在托管代码中使用系统事件，.NET Framework 在 `System.Threading` 命名空间中提供了 `ManualResetEvent`、`AutoResetEvent`、`ManualResetEventSlim` 和 `CountdownEvent` 类。`ManualResetEventSlim` 和 `CountdownEvent` 是 .NET 4 中新增的。

![](img/d7d2ffa0a76feaab821930e95daace93_587_0.png)

可以使用事件通知其他任务某些数据已经存在、某项操作已经完成，等等。事件可以处于有信号状态，也可以处于无信号状态。借助前面已经讨论过的 `WaitHandle` 类，任务可以等待事件进入有信号状态。

调用 `Set()` 方法可以使 `ManualResetEvent` 进入有信号状态，调用 `Reset()` 方法则可以将其重新设置为无信号状态。如果有多个线程正在等待事件进入有信号状态，并且调用了 `Set()` 方法，那么所有正在等待的线程都会被释放。此外，如果某个线程刚刚调用了 `WaitOne()` 方法，但事件已经处于有信号状态，那么等待线程可以立即继续执行。

调用 `Set()` 方法同样可以使 `AutoResetEvent` 进入有信号状态。也可以使用 `Reset()` 方法将其重新设置为无信号状态。但是，如果某个线程正在等待自动重置事件进入有信号状态，那么当第一个线程结束等待状态时，事件会自动变为无信号状态。这样，如果有多个线程正在等待事件被设置，只有一个线程会从等待状态中释放出来。被释放的并不是等待事件进入有信号状态时间最长的线程，而是等待线程中优先级最高的线程。

为了使用 `ManualResetEventSlim` 类演示事件，`Calculator` 类定义了 `Calculation()` 方法，该方法是任务的入口点。通过此方法，任务接收用于计算的输入数据，并将结果写入变量 `result`，该变量可以通过 `Result` 属性访问。结果完成后（经过一段随机时间），通过调用 `ManualResetEventSlim` 的 `Set()` 方法使事件进入有信号状态。

```csharp
public class Calculator
{
    private ManualResetEventSlim mEvent;
    public int Result { get; private set; }
    public Calculator(ManualResetEventSlim ev)
    {
        this.mEvent = ev;
    }
    public void Calculation(object obj)
    {
        Tuple<int, int> data = (Tuple<int, int>)obj;
        Console.WriteLine("Task {0} starts calculation", Task.Current.Id);
        Thread.Sleep(new Random().Next(3000));
        Result = data.Item1 + data.Item2;
        // signal the event-completed!
        Console.WriteLine("Task {0} is ready", Task.Current.Id);
        mEvent.Set();
    }
}
```

### 2.3 洛伦兹变换

现在推导以恒定相对速度运动的惯性参考系之间的坐标变换。根据爱因斯坦的假设，该变换必须是线性的，并且保持光速不变。

考虑两个惯性参考系 S 和 S'，其中 S' 以速度 v 沿 x 轴运动。所需的变换就是洛伦兹变换：

```
$$\begin{aligned} x' &= \gamma (x - vt) \\ t' &= \gamma \left( t - \frac{vx}{c^2} \right) \end{aligned}$$
```

其中，$\gamma = \frac{1}{\sqrt{1 - v^2/c^2}}$ 是洛伦兹因子。这些表达式在高速情况下取代了伽利略变换。

- S' 的原点对应于世界线 $x = vt$。
- 当 $v = 0$ 时，该变换退化为恒等变换。
- 时空间隔 $s^2 = c^2 t^2 - x^2$ 保持不变。

将 v 替换为 -v 即可得到逆变换，这与相对运动的对称性相一致。

```
$$\begin{aligned} x &= \gamma (x' + vt') \\ t &= \gamma \left( t' + \frac{vx'}{c^2} \right) \end{aligned}$$
```

> 人们常说洛伦兹变换混合了空间和时间；然而，其精确关系仍然保持了普适的速度 c。

在非相对论极限下，即 $v \ll c$ 时，因子 $\gamma$ 趋近于 1，洛伦兹变换也就退化为人们熟悉的伽利略变换。

```
finished task for 0, result: 4
Task 4 starts calculation
Task 3 is ready
finished task for 2, result: 8
Task 1 is ready
finished task for 1, result: 6
Thread 4 is ready
finished task for 3, result: 10
```

在类似这样的场景中，如果要将一些工作拆分到多个任务中，然后再汇总结果，那么新增的 `CountdownEvent` 类会非常有用。不必为每个任务分别创建一个事件对象，只需创建一个即可。`CountdownEvent` 为所有会设置信号的任务定义一个初始数量，计数达到该数量后，`CountdownEvent` 就会进入有信号状态。

`Calculator` 类经过修改后，使用 `CountdownEvent` 替代了 `ManualResetEvent`。`CountdownEvent` 使用 `Signal()` 方法，而不是使用 `Set()` 方法来设置信号。

```csharp
public class Calculator
{
    private CountdownEvent cEvent;

    public int Result { get; private set; }

    public Calculator(CountdownEvent ev)
    {
        this.cEvent = ev;
    }

    public void Calculation(object obj)
    {
        Tuple<int, int> data = (Tuple<int, int>)obj;
        Console.WriteLine("Task {0} starts calculation", Task.Current.Id);
        Thread.Sleep(new Random().Next(3000));
        Result = data.Item1 + data.Item2;

        // signal the event-completed!
        Console.WriteLine("Task {0} is ready", Task.Current.Id);
        cEvent.Signal();
    }
}
```

代码片段 EventSample/Calculator.cs

现在可以简化 `Main()` 方法，使其只需等待一个事件即可。如果不需要像之前那样分别处理结果，那么这个新版本可能就已经足够了。

```csharp
const int taskCount = 4;
var cEvent = new CountdownEvent(taskCount);
var calcs = new Calculator[taskCount];
var taskFactory = new TaskFactory();
for (int i = 0; i < taskCount; i++)
{
    calcs[i] = new Calculator(cEvent);
    taskFactory.StartNew(calcs[i].Calculation,
        Tuple.Create(i + 1, i + 3));
}
cEvent.Wait();
Console.WriteLine("all finished");
```

