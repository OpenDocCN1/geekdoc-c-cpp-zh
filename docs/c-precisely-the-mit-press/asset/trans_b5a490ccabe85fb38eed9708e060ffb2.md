

# 线程、并发执行与同步 135

## 示例 166 通过监视器（Monitor）通信的生产者与消费者

缓冲区有一个存储整数的空间，并有一个 `Put` 方法用于存入缓冲区（如果为空）以及一个 `Get` 方法用于从缓冲区读取（如果非空）；它是一个监视器（第 21.2 节）。调用 `Get` 的线程必须获取缓冲区锁。如果它发现缓冲区为空，它会调用 `Wait` 释放锁并等待直到有内容放入缓冲区。如果另一个线程调用 `Put` 和 `Pulse`，那么获取数据的线程将重新竞争缓冲区锁，如果它获得了锁，将将继续执行。

```csharp
class Buffer {
    private int contents;
    private bool empty = true;
    public int get() {
        lock (this);
        while (empty) Monitor.Wait(this);
        empty = true;
        Monitor.Pulse(this);
        return contents;
    }
    public void Put(int v) {
        lock (this);
        while (!empty) Monitor.Wait(this);
        empty = false; contents = v;
        Monitor.Pulse(this);
    }
}
```

## 示例 167 死锁

由于粗心地锁定多个对象会导致死锁。假设有一只左鞋和一只右鞋（两个对象），以及两个人（两个线程）想要使用它们。首先由一个人拿这双鞋。但如果通过 `new Person("groucho", left, right)` 和 `new Person("harpo", right, left)` 创建了两只鞋，那么第一个人可能会锁定左鞋，而第二个人可能会锁定右鞋，然后他们都会永远地等待另一只鞋。这可以通过始终以相同的固定的顺序（实例在前，右侧在后）锁定对象来避免。

```csharp
class Person {
    String name, fst, snd;
    public Person(String name, String fst, String snd) {
        this.name = name; this.fst = fst; this.snd = snd;
        new Thread(new ThreadStart(Run)).Start();
    }
    public void Run() {
        lock (this);
        Console.WriteLine(name + " got " + fst);
        Thread.Sleep(0); // 让出给其他线程
        lock (snd) { Console.WriteLine(name + " got " + snd);
            Console.WriteLine(name + " released " + snd);
        }
        Console.WriteLine(name + " released " + fst);
    }
}
```

任务并行库 (C# 4.0)

## 22 任务并行库 (C# 4.0)

任务并行库通过 `System.Threading.Tasks` 命名空间中的几种类型实现。

### 22.1 类并行

`System.Threading.Tasks` 命名空间下的静态类 `Parallel`：

- * staticParallelLoopResult For(int m, int n, Action<int> body) 执行 `body(m)`、`body(m+1)`……`(n-1)`，可能并发且无序执行。阻塞直到所有调用完成；如果 `m>=n` 则什么都不做。
- * staticParallelLoopResult For(int m, int n, Action<int, LoopState> body) 执行 `body(m, loopState)`、`body(m+1, loopState)`……`(n-1, loopState)`，可能并发且无序执行。使用委托 `i(loopState).Break(i)` 信号第 `i` 次迭代之后不再需要，或调用 `loopState.Stop()` 信号不再进行任何后续迭代。在某些情况下，可能会执行后续迭代。注意 `ParallelLoopState` 类的 `loopState` 对象是由 `For` 方法创建的。

存在其他重载，用于接收范围而非边界、接收并行选项以及创建线程本地状态。详情请参见 .NET 库文档。

- * staticParallelLoopResult ForEach<T>(IEnumerable<T> xs, Action<T> body) 为 `xs` 的所有元素 `x1`, `x2`……执行 `body(x1)`、`body(x2)`……，可能并发且无序执行。

存在 `ForEach` 重载，用于接受并行循环参数的 `Action` 委托、接收并行选项以及创建线程本地状态的情况。详情请参见 .NET 库文档。

- * static void Invoke(params Action[] acts) 调用数组 `acts` 中的委托，可能并发且无序执行。还重载了以接收并行选项参数。

- * 只读属性 `bool IsCompleted` 如果所有迭代已执行则为 `true`；否则为 `false`。
- * 只读属性 `length LowestBreakIteration` 返回调用 `Break(i)` 的最低迭代索引，如果为空则返回。

当并行循环的多次迭代需要更新全局资源时，它们必须锁定该资源（第 21.2 节）。例如，对于示例 170 中的 `Parallel.For` 如果将结果存储在列表 `results` 中，而不是独立的数组中，那么循环在添加元素时必须锁定数组（但在执行计算时不需要）：

```csharp
i => { String res = NcbProtein(ids[i]);
lock (results) results.Add(res); };
```

这种方法可以安全地防止过度锁定，因为某些或所有迭代可能在同一个线程上执行。`For` 和 `ForEach` 的进一步重载提供了引入线程本地资源的方法，从而节省某些锁定。参见 .Net 库文档。

## 示例 168 并行矩阵乘法
矩阵乘法 $R = AB$ 可以通过三层嵌套循环实现。通过调用方法 `Parallel.For` 并配合表示内部循环的 Lambda 表达式，可以将普通的顺序外层循环替换为并行外层循环。不需要同步。

```csharp
Parallel.For(0, rows, r => {
    for (int c = 0; c < cols; c++) {
        for (int k = 0; k < inner; k++) {
            R[r, c] += A[r, k] * B[k, c];
        }
    }
});
```

示例 169 计算的并行执行
使用任务并行库可以使用 `Task.Run` 方法。

```csharp
Task task = Task.Run(() => {
    // 在处执行计算
});
```

示例 170 数据检索
任务并行库可以从多个源并行检索数据。

```csharp
string[] results = new string[ids.Length];
Parallel.For(0, ids.Length, i => {
    string res = NcbProtein(ids[i]);
    results[i] = res;
});
```

## 22.2 Task 类
`Task` 类及其子类 `Task<T>` 用于创建任务并实现异步方法（第 23 ）。`Task` 表示不产生结果的异步活动（void 委托），而 `Task<T>` 表示类型 `T`。

### 22.2.1 Task 类
`System.Threading.Tasks` 命名空间下的 `Task` 类包含以下成员等：

- Constructor(Action act) 创建一个任务，启动时将执行 `act`。
- ContinueWith(Action<Task> cont) 创建并启动一个延续任务；当任务完成后将调用 `cont(task)`。
- Task<U> ContinueWith(Func<Task, U> cont) 类似，但延续产生结果。
- static Delay(int ms) 创建并启动一个阻塞 `ms` 毫秒的任务。
- static Run(Action act) 创建并启动一个执行 `act` 的并发任务。
- static Task<T> Run(Func<T> func) 创建并启动一个执行 `func` 的并发任务。
- RunSynchronously() 在当前任务调度器上同步启动任务；阻塞当前线程直到任务完成。
- Start() 在当前任务调度器上异步启动给任务。如果任务已启动或取消，则抛出 `InvalidOperationException`。
- 只读属性 `TaskStatus` 返回任务状态（见第 141 页）。
- Wait() 阻塞直到任务完成。如果任务取消或抛出异常，则抛出 `AggregateException`。
- static Task WhenAll(params Task[] tasks) 创建并启动一个任务，当所有给定的任务完成后，返回结果数组。
- static Task<T[]> WhenAll(params Task<T>[] tasks) 创建并启动一个任务，当所有给定的任务完成后，返回结果数组。
- static Task<T> WhenAny(params Task<T>[] tasks) 创建并启动一个任务，当任何一个任务完成后，返回完成的任务之一。

构造函数和方法 `ContinueWith`、`Delay` 和 `Run` 具有进一步重载，可以接收额外的 `CancellationToken` 参数（第 22.2.3 节和 174 节），用于取消生成的任务。`ContinueWith` 方法具有接收任务延续选项参数或任务调度器参数的重载。请参见 .NET 类库文档。

