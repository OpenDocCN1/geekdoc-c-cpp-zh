
```
static void Main()
{
    new Thread(() =>
    {
        while (true)
        {
            s_i++;
        }
    }).Start();

    while (true)
    {
        Thread.Sleep(1000);
        Console.WriteLine(s_i);
    }
}
```

当你想避免静态状态在线程之间共享时（例如，多个工作线程需要拥有该状态的自己的副本），ThreadStatic 特性就派上用场了。

有一点需要指出：对标记为线程静态的字段进行初始化并不是一个好主意，因为给该字段赋值的初始化代码位于（静态）类构造函数中，而该构造函数在每个应用程序域中只运行一次。下面的代码会输出 42 和 0，因为该类的静态构造函数是在主线程上执行的。同样的初始化代码并没有在另一个线程上运行。

```
class Program
{
    [ThreadStatic]
    static int s_i = 42;

    static void Main()
    {
        Console.WriteLine(s_i);                 // Prints 42 :-)
        new Thread(() => Console.WriteLine(s_i)).Start(); // Prints 0 :-( 
        Console.ReadLine();
    }
}
```

不要依赖这种表现不稳定的初始化代码（如这里所示），而应依赖静态字段被设置为默认值。代码可以对照该值进行检查，以执行一次性初始化。我最近使用线程静态字段的一个例子是分配线程专用的日志记录器。在这种情况下，进行诊断日志记录时不需要同步，因为每个线程都会获得自己专用的日志记录器实例：

```
class Program
{
    [ThreadStatic]
    static TextWriter s_logger;

    static void Main()
    {
        new Thread(() =>
        {
            EnsureLog();

            // Some thread that's responsible for some I/O operation.
            // At various times, it writes to the log, as shown here:
            s_logger.WriteLine("{0} - Performed some action", DateTime.Now);

            // Much more code is executed on this thread...
        }) { Name = "Lazy writer" }
        .Start();

        // Others threads could be created, each of which has to call
        // the EnsureLog method to have its s_logger field set up properly.
    }

    static void EnsureLog()
    {
        string name = Thread.CurrentThread.Name
            ?? Thread.CurrentThread.ManagedThreadId.ToString();

        // More complicated initialization logic could be dreamed up.
        // What matters is the fact this method will run multiple times
        // on different threads, initializing that thread's logger.
        s_logger = File.CreateText(name + ".log");
    }
}
```

注意使用当前线程的 Name 属性来初始化日志文件名。从 Main 中的代码来看，可能不容易看出这个值在线程看到它之前就已经被设置了。毕竟，我们使用对象初始值设定项来设置线程的 Name；由于调用了 Start，代码（这里在 lambda 表达式体中指定）会在 Name 设置之后才运行。这再次体现了委托的本质：它有助于在代码指定位置之外的地方延迟执行代码。

## ThreadLocal<T> 类

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1485_0.png)

与 Lazy<T> 类密切相关的 ThreadLocal<T> 类是在 .NET 4 中引入的。本质上，当每线程状态需要初始化代码时，该类型解决了 ThreadStatic 特性的缺点。ThreadLocal<T> 类充当每线程状态的工厂，它使用一个 Func<T> 委托，在调用 Value 属性时每个线程会调用该委托一次。这种模式应该很熟悉；毕竟，Lazy<T> 也使用了同样的模式。

例如，考虑上一节中的代码示例。使用 ThreadLocal<T> 类型重写这个示例（用 T 替换为 TextWriter）会得到以下代码：

```csharp
class Program
{
    static void Main()
    {
        new Thread(() =>
        {
            // Some thread that's responsible for some I/O operation.
            // At various times, it writes to the log, as shown here:
            s_log.Value.WriteLine("{0} - Performed some action", DateTime.Now);

            // Much more code is executed on this thread...
        }) { Name = "Lazy writer" }
            .Start();

        // Others threads could be created
        Console.ReadLine();
    }

    static ThreadLocal<TextWriter> s_log = new ThreadLocal<TextWriter>(() =>
    {
        string name = Thread.CurrentThread.Name
            ?? Thread.CurrentThread.ManagedThreadId.ToString();

        // More complicated initialization logic could be dreamed up.
        // What matters is the fact this method will run multiple times
        // on different threads, initializing that thread's logger.
        return File.CreateText(name + ".log");
    });
}
```

两个关键区别是：s_log 字段上缺少 ThreadStatic 特性，以及使用 Value 属性来获取线程本地状态。此外，还有一个 IsValueCreated 属性，用于检查初始化委托（或者随你怎么称呼的工厂）是否已经为当前线程运行过。这也遵循了之前 Lazy<T> 中看到的模式。

ThreadLocal<T> 类型的一个优势是，无需让字段带有 ThreadStatic 特性即可使用它。如果你自己无法控制这些字段（例如在使用闭包时），这一点尤其有用。正如我们在讨论委托时所学到的，对局部变量的闭包会导致在“显示类”上创建字段，而该类完全由编译器控制。例如，看看下面的代码。为了帮助你回顾闭包，图 29.11 展示了编译此示例的结果。

```
static void Main()
{
    int i = 0;
    new Thread(() =>
    {
        while (true)
            i++;
    }).Start();

    while (true)
    {
        Thread.Sleep(1000);
        Console.WriteLine(i);
    }
}
```

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1486_0.png)

图 29.11 对局部变量 i 的闭包会生成一个字段。

这几乎与我们之前展示的多线程读写计数器示例是相同的代码，唯一的区别是计数器使用了局部变量，而不是我们自己使用字段。由于 C# 中没有语法方式将特性应用于局部变量，因此这里不能使用 ThreadStatic。换句话说，用户无法影响因局部变量闭包而生成的字段。

然而，ThreadLocal<T> 可以毫无问题地使用。随着 lambda 表达式（以及因此闭包）的使用变得更加普遍，这是 .NET 4 带给我们的极好礼物。在第 30 章中，你会看到其他 .NET 4 构造的使用，例如 Parallel.For，在这些构造中使用 lambda 非常方便。这些构造的引入使对 ThreadLocal<T> 构造的需求更加迫切。下面的代码展示了如何使计数器变量成为线程本地变量，就像我们之前为使用 ThreadStatic 特性的类似示例所做的那样。回顾一下，这会改变代码的行为，使读取线程打印自己的 i 私有副本，而该副本始终设置为零：

```
static void Main()
{
    var i = new ThreadLocal<int>();
    new Thread(() =>
    {
        while (true)
            i.Value++;
    }).Start();

    while (true)
    {
        Thread.Sleep(1000);
        Console.WriteLine(i.Value);
    }
}
```

## 关于线程安全的说明

到目前为止，我们还没有提到线程安全（本章后面介绍同步原语时会更全面地讨论这一点）。特别是，我们通过只设置一个写入线程，避免了在两个计数器示例的上下文中讨论线程安全。然而，如果多个方试图写入一个共享的（即非线程本地的）计数器，我们就需要停下来思考如何确保线程安全。在使用 ThreadLocal<T> 的最后一个计数器示例中，如果存在多个写入线程，就会出现一个相当明显的多线程问题。看看下面这行代码：

```
i.Value++;
```

这行看似无辜的代码做了很多事情，这些事情导致递增操作不是原子的。首先，通过调用 getter 读取 Value 属性。然后，对检索到的值的本地副本进行递增。最后，通过使用 Value setter 分配递增后的值。如果多个写入线程正在更新计数器，这远非线程安全。稍后会详细讨论。

## 线程本地存储

我们把建立线程本地状态的“最原生”方式留到最后，因为 ThreadStatic 和 ThreadLocal<T> 是实现此效果的推荐方式。尽管如此，还有第三种进行线程本地存储的方式。

