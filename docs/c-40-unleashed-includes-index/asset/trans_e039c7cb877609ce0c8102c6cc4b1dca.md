

在我们声明类型为 Destruct 的局部变量时，默认构造函数会被调用，导致打印出 Constructing。在方法退出时，为该方法编译的代码会确保栈上分配的对象通过对析构函数的调用而被析构。这是一种确定性的清理方式。

对于堆分配的示例，输出略有不同。这里删除对象的责任由用户通过使用 delete 运算符来承担。就在那个时间点，析构函数将被调用：

```
Heap - begin
Constructing
Destructing
Heap - end
```

再次，这也是一种确定性的清理方式。在这两种情况下，都是词法作用域或手动用户干预导致析构函数被调用。在任何情况下都不会有运行时服务介入来调用析构函数的代码。

## 在 C# 中定义终结器

在详细讨论其行为并与前面展示的 C++ 行为进行对比之前，我们首先展示如何在 C# 中声明终结器。由于它们与 C++ 语法相同，语言规范称它们为析构函数，但为了避免与你的 C++ 程序员朋友混淆，我们称它们为终结器。

下面是一个在 C# 中定义的终结器，使用类名前面加上 ~ 字符：

```
class A
{
    ~A()
    {
        Console.WriteLine("Destructing instance of A");
    }
}
```

终结器不能有访问修饰符，也不能有任何参数。它们不能由用户显式调用（因此传递参数没有意义），正如你将看到的那样。

## 终结器如何运行

现在让我们继续讨论其行为以及与终结器使用相关的最佳实践。与 C++ 不同，终结器是由运行时在对象实例不再可被用户代码访问时调用的。负责其调用的运行时服务是垃圾收集器，它负责在堆分配对象变得不可达之后释放它们占用的内存。前面我们讨论了垃圾收集器采用的标记-清除机制，用于扫描内存、标记仍存活的对象并收集不再可用的对象。

当对象被垃圾回收并且实现了终结器时，该方法将在对象占用的内存最终被回收之前由垃圾收集器安排运行。由于垃圾收集器的工作方式，终结器会给运行时带来额外的压力。原因如下。

在垃圾回收期间，运行时的托管代码执行会被挂起，因为内存正在被操作并且引用暂时不一致。如果此时允许代码运行，这将破坏类型安全，因为跟随托管引用可能会导致你进入无人区。因此，终结器中的代码不能在收集进行时运行。相反，已有资格进行终结的对象（由自定义终结器的实现确定）会被放入队列，以便在进行中的垃圾回收之后执行引擎重新启动时稍后处理。

由于这种行为，使用空终结器是对对象可能做到的最糟糕的事情，因为你只是无缘无故地推迟了它的死亡。你很快就会了解到终结器的使用如何以及应该在可能的情况下尽可能避免。但首先，让我们展示一个终结器被调用的情况：

```
static void Main()
{
    A a = new A();

    // Won't collect before the application quits.
    Console.ReadLine();
}

class A
{
    ~A()
    {
        Console.WriteLine("Destructing instance of A");
    }
}
```

除非发生完全意外的事件导致前一段代码触发垃圾收集器，否则 A 实例的终结器不会在应用程序退出时的最后时刻之前被调用。在前面的示例中，托管堆根本没有足够的压力来证明进行收集是合理的。为了真正说明终结的非确定性行为，让我们展示一个更人为的过度分配示例，导致收集发生：

```
while (true)
{
    A a = new A();
}
```

每次循环迭代都会在堆上分配一个新对象。这会导致堆增长直到第 0 代填满。此时，垃圾收集器将启动以收集不再可达的对象。事实上，先前迭代分配的所有对象都不可达，因为我们覆盖了保存其引用的局部变量。为了显示哪些对象被分配以及哪些对象被终结，我们将在 A 中添加一些计数机制：

```
class A
{
    private static int s_id;
    private int _id;

    public A()
    {
        _id = s_id++;
        Console.WriteLine("Allocated instance " + _id);
    }

    ~A()
    {
        Console.WriteLine("Finalized instance " + _id);
    }
}
```

执行此代码时，结果可能会因计算机而异，也可能因运行而异，因为垃圾收集器会考虑各种参数（例如系统的整体内存压力）。然而，你应该会看到对象被分配很长时间，直到第一次收集启动并移除孤立的实例：

```
Allocated instance 8338
Allocated instance 8339
Allocated instance 8340
Allocated instance 8341
Finalized instance 8331
Allocated instance 8342
Allocated instance 8343
Finalized instance 6
Finalized instance 7
```

这些对象被终结的顺序完全是非确定性的。你也可以监控收集计数以查看何时发生 gen0 收集：

```csharp
int gen0 = 0;
while (true)
{
    A a = new A();
    var new0 = GC.CollectionCount(0);
    if (gen0 != new0)
    {
        Console.WriteLine("Gen0 collection triggered");
        gen0 = new0;
    }
}
```

## 终结器如何实现

为了证明我们使用终结器而非析构函数的命名，请在 ILDASM 中查看生成的代码，如图 12.6 所示。如你所见，C# 析构函数被转换为重写 Finalize 方法的方法，该方法定义在 System.Object 上。用户的自定义逻辑和对基类终结器的调用都位于此方法内部。虽然我们仍需学习继承，但这个想法很简单。当一个类派生自另一个类以专门化其行为时，确保基类的清理逻辑作为终结的一部分运行至关重要。我们终结器中的代码将等同于以下内容：

```csharp
~A()
{
    try {
        Console.WriteLine("Finalized instance " + _id);
    }
    finally {
        base.Finalize();  // Calls System.Object's Finalize method.
    }
}
```

尽管析构函数会变成 Finalize 方法，但 C# 禁止直接使用此方法（例如使用 override 关键字）。另一方面，Visual Basic 不添加析构函数语法，并允许用户重写 Finalize 方法。

## 不适用于结构体

终结器只能在类上定义。确定结构体终结器何时运行的簿记工作会严重影响其轻量级特性。

![](img/a16f85e62ce9bdc527f4b09dbfe26092_624_0.png)

图 12.6 析构函数重写 Finalize 方法。

## 在收集之前释放：IDisposable

终结器通常用于确保超出垃圾收集器责任范围的资源得到正确清理。一个很好的例子是当你必须处理非托管资源时（例如，在 Win32 互操作场景中需要使用 CloseHandle 调用手动释放对象）。尽管许多 Win32 API 已在 .NET Framework 中被封装，但有时你可能需要手动 P/Invoke 其他 API。例如，考虑 CreateJobObject Win32 函数，它允许创建作业，即进程组。托管代码包装器可能如下所示：

```
public class Job
{
    [DllImport("kernel32.dll", CharSet = CharSet.Unicode, SetLastError = true)]
    static extern IntPtr CreateJobObject(SECURITY_ATTRIBUTES att, string name);

    [DllImport("kernel32.dll", SetLastError = true)]
    static extern bool AssignProcessToJobObject(IntPtr job, IntPtr process);

    [DllImport("kernel32.dll", SetLastError = true)]
    static extern bool TerminateJobObject(IntPtr job, uint exitCode);

    private IntPtr _handle;

    private Job(IntPtr handle)
    {
        _handle = handle;
    }

    public static Job CreateOrOpen(string name)
    {
        // Notice a "null" name is allowed by the Win32 function.
        var res = CreateJobObject(null, name);

