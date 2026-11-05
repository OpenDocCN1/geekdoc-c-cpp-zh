
![](img/5da9b5c72747b887ec63f57c832400bf_639_0.png)

## 使用有限数量的池化对象处理请求

```
var throttle = new JoinBlock<ExpensiveObject, Request>();
for(int i=0; i<10; i++)
{
    requestProcessor.Target1.Post(new ExpensiveObject());
}

var processor = new Transform<Tuple<ExpensiveObject, Request>, ExpensiveObject>(pair =>
{
    var resource = pair.Item1;
    var request = pair.Item2;

    request.ProcessWith(resource);

    return resource;
});

throttle.LinkTo(processor);
processor.LinkTo(throttle.Target1);
```

Stephen Toub 的 TPL Dataflow 介绍

## 第 121.5 节：WriteOnceBlock<T>

(只读变量：记住其第一个数据项并将其副本作为输出传递。忽略所有其他数据项)

如果 BufferBlock 是 TPL Dataflow 中最基础的块，那么 WriteOnceBlock 就是最简单的。
它最多存储一个值，一旦该值被设置，就永远不会被替换或覆盖。

你可以将 WriteOnceBlock 视为类似于 C# 中的只读成员变量，只是与仅在构造函数中可设置然后不可变不同，它只能设置一次，然后就不可变了。

![](img/5da9b5c72747b887ec63f57c832400bf_639_1.png)

### 拆分任务的潜在输出

```
public static async void SplitIntoBlocks(this Task<T> task,
    out IPropagatorBlock<T> result,
    out IPropagatorBlock<Exception> exception)
{
    result = new WriteOnceBlock<T>(i => i);
    exception = new WriteOnceBlock<Exception>(i => i);
    try
    {
        result.Post(await task);
    }
    catch (Exception ex)
    {
        exception.Post(ex);
    }
}
```

Stephen Toub 的 TPL Dataflow 介绍

## 第 121.6 节：BatchedJoinBlock<T1, T2,...>

(从 2-3 个输入中收集一定数量的总项，并将它们分组为数据项集合的 Tuple)

BatchedJoinBlock<T1, T2,...> 在某种意义上是 BatchBlock 和 JoinBlock<T1, T2,...> 的组合。JoinBlock<T1, T2,...> 用于将每个目标的一个输入聚合为一个元组，而 BatchBlock 用于将 N 个输入聚合为一个集合，BatchedJoinBlock<T1, T2,...> 用于从所有目标中收集 N 个输入并形成集合的元组。

![](img/5da9b5c72747b887ec63f57c832400bf_640_0.png)

### 散布/收集

考虑一个散布/收集问题，其中启动了 N 个操作，其中一些可能成功并产生字符串输出，而另一些可能失败并产生 Exceptions。

```
var batchedJoin = new BatchedJoinBlock<string, Exception>(10);

for (int i=0; i<10; i++)
{
    Task.Factory.StartNew(() => {
        try { batchedJoin.Target1.Post(DoWork()); }
        catch(Exception ex) { batchedJoin.Target2.Post(ex); }
    });
}

var results = await batchedJoin.ReceiveAsync();

foreach(string s in results.Item1)
{
    Console.WriteLine(s);
}

foreach(Exception e in results.Item2)
{
    Console.WriteLine(e);
}
```

Stephen Toub 的 TPL Dataflow 介绍

## 第 121.7 节：TransformBlock<TInput, TOutput>

(Select，一对一)

与 ActionBlock 类似，TransformBlock<TInput, TOutput> 允许执行委托为每个输入数据执行某些操作；与 ActionBlock 不同，此处理有输出。该委托可以是 Func<TInput, TOutput>，在这种情况下，当委托返回时，该元素的处理被认为已完成；也可以是 Func<TInput,Task<>>，在这种情况下，该元素的处理被认为已完成的时间不是委托返回时，而是返回的 Task 完成时。对于熟悉 LINQ 的人来说，它有点类似于 Select()，即它接收输入，以某种方式转换该输入，然后产生输出。

默认情况下，TransformBlock<TInput, TOutput> 以 MaxDegreeOfParallelism 等于 1 的方式顺序处理其数据。除了接收缓冲输入并处理它之外，此块还会将所有已处理的输出进行缓冲（未处理的数据和已处理的数据）。

它有两个任务：一个用于处理数据，一个用于将数据推送到下一个块。

![](img/5da9b5c72747b887ec63f57c832400bf_641_0.png)

### 一个并发管道

```
var compressor = new TransformBlock<byte[], byte[]>(input => Compress(input));
var encryptor = new TransformBlock<byte[], byte[]>(input => Encrypt(input));

compressor.LinkTo(encryptor);
```

Stephen Toub 的 TPL Dataflow 介绍

## 第 121.8 节：TransformManyBlock<TInput, TOutput>

(SelectMany，1-m：此映射的结果会被“展平”，就像 LINQ 的 SelectMany 一样)

TransformManyBlock<TInput, TOutput> 与 TransformBlock<TInput, TOutput> 非常相似。关键区别在于，TransformBlock<TInput, TOutput> 为每个输入产生一个且仅一个输出，而 TransformManyBlock<TInput, TOutput> 为每个输入产生任意数量（零个或多个）输出。与 ActionBlock 和 TransformBlock<TInput, TOutput> 一样，此处理可以使用委托指定，既可用于同步处理，也可用于异步处理。

同步使用 Func<TInput, IEnumerable<>>，异步使用 Func<TInput, Task<IEnumerable<>>>。与 ActionBlock 和 TransformBlock<TInput, TOutput> 一样，TransformManyBlock<TInput, TOutput> 默认按顺序处理，但也可以另行配置。

映射委托返回一个项目集合，这些项目会单独插入到输出缓冲区中。

![](img/5da9b5c72747b887ec63f57c832400bf_642_0.png)

### 异步网络爬虫

```
var downloader = new TransformManyBlock<string, string>(async url =>
{
    Console.WriteLine("Downloading " + url);
    try
    {
        return ParseLinks(await DownloadContents(url));
    }
    catch()
    {
        return Enumerable.Empty<string>();
    }
});
downloader.LinkTo(downloader);
```

### 将可枚举对象扩展为其组成元素

```
var expanded = new TransformManyBlock<T[], T>(array => array);
```

### 通过从 1 到 0 或 1 个元素进行过滤

```
public IPropagatorBlock<T> CreateFilteredBuffer<T>(Predicate<T> filter)
{
    return new TransformManyBlock<T, T>(item =>
        filter(item) ? new [] { item } : Enumerable.Empty<T>());
}
```

Stephen Toub 的 TPL Dataflow 介绍

## 第 121.9 节：BatchBlock<T>

(将一定数量的顺序数据项分组为数据项集合)

BatchBlock 将 N 个单项组合成一个批项，以元素数组表示。实例使用特定的批大小创建，然后块在收到该数量的元素后立即创建一批，并异步将其输出到输出缓冲区。

BatchBlock 能够以贪婪和非贪婪两种模式执行。

- 在默认的贪婪模式下，从任意数量的源提供给块的所有消息都被接受并缓冲以转换为批。
- 在非贪婪模式下，所有消息都从源推迟，直到有足够多的源向块提供消息以创建一批。因此，BatchBlock 可用于从 N 个源各接收 1 个元素、从 1 个源接收 N 个元素，以及两者之间的多种选项。

![](img/5da9b5c72747b887ec63f57c832400bf_643_0.png)

### 将请求批量处理为 100 个一组以提交到数据库

```
var batchRequests = new BatchBlock<Request>(batchSize:100);
var sendToDb = new ActionBlock<Request[]>(reqs => SubmitToDatabase(reqs));

batchRequests.LinkTo(sendToDb);
```

### 每秒创建一次批

```
var batch = new BatchBlock<T>(batchSize:Int32.MaxValue);
new Timer(() => { batch.TriggerBatch(); }).Change(1000, 1000);
```

Stephen Toub 的 TPL Dataflow 介绍

## 第 122 章：函数式编程

### 第 122.1 节：Func 和 Action

**Func** 提供参数化匿名函数的持有者。领先的类型是输入，最后一个类型始终是返回值。

```
// square a number.
Func<double, double> square = (x) => { return x * x; };

// get the square root.
// note how the signature matches the built in method.
Func<double, double> squareroot = Math.Sqrt;

// provide your workings.
Func<double, double, string> workings = (x, y) =>
    string.Format("The square of {0} is {1}.", x, square(y))
```

**Action** 对象类似于 void 方法，因此它们只有输入类型。没有结果被放置在求值栈上。

```
// right-angled triangle.
class Triangle
{
    public double a;
    public double b;
    public double h;
}

// Pythagorean theorem.
Action<Triangle> pythagoras = (x) =>
    x.h = squareroot(square(x.a) + square(x.b));

Triangle t = new Triangle { a = 3, b = 4 };
pythagoras(t);
Console.WriteLine(t.h); // 5.
```

### 第 122.2 节：高阶函数

高阶函数是指接受另一个函数作为参数或返回一个函数（或两者兼有）的函数。

这通常使用 lambda 完成，例如在将谓词传递给 LINQ Where 子句时：

```
var results = data.Where(p => p.Items == 0);
```

Where() 子句可以接收许多不同的谓词，这使其具有相当大的灵活性。

在实现策略设计模式时，也会看到将方法传递给另一个方法。例如，可以根据运行时需求从各种排序方法中选择并将其传递给对象上的 Sort 方法。

### 第 122.3 节：避免空引用

C# 开发者要处理大量空引用异常。F# 开发者则不需要，因为他们有 Option 类型。Option<> 类型（有些人更喜欢 Maybe<> 作为名称）提供 Some 和 None 返回类型。它明确表示一个方法可能即将返回一个空记录。
