
解决此问题的更好方法是将 BranchName 作为类型为 `Collection<T>` 而不是 `List<T>` 的属性公开。这是因为泛型 `Collection<T>` 类型提供了四个可重写的方法 — ClearItems()、InsertItem()、RemoveItem() 和 SetItem() — 允许派生类在集合被修改时收到通知。

以下是使用泛型 `Collection<T>` 类型重写 Branch 类的方式：

```csharp
public class Branch
{
    public Branch()
    {
        _branchNames = new BranchNamesCollection(this);
    }

    private BranchNamesCollection _branchNames;
    public Collection<string> BranchNames
    {
        get
        {
            return _branchNames;
        }
    }

    //---event raised when an item is removed---
    public event EventHandler ItemRemoved;

    //---called from within the BranchNamesCollection class---
    protected virtual void RaiseItemRemovedEvent(EventArgs e)
    {
        if (ItemRemoved != null)
        {
            ItemRemoved(this, e);
        }
    }

    private class BranchNamesCollection : Collection<string>
    {
        private Branch _b;
        public BranchNamesCollection(Branch b)
        {
            _b = b;
        }

        //---fired when an item is removed---
        protected override void RemoveItem(int index)
        {
            base.RemoveItem(index);
            _b.RaiseItemRemovedEvent(EventArgs.Empty);
        }
    }
}
```

现在 Branch 类内部有一个名为 BranchNamesCollection 的类。BranchNamesCollection 类的类型为 `Collection<string>`。它重写了 `Collection<T>` 类中存在的 RemoveItem() 方法。当从集合中删除一项时，它会通过调用 base RemoveItem() 方法来删除该项，然后调用在 Branch 类中定义的一个函数：RaiseItemRemovedEvent()。RaiseItemRemovedEvent() 函数随后触发 ItemRemoved 事件以通知客户端已删除一项。

要在 Branch 类中处理 ItemRemoved 事件，请按如下方式修改代码：

```csharp
static void Main(string[] args)
{
    Branch b = new Branch();
    b.ItemRemoved += new EventHandler(b_ItemRemoved);

    b.BranchNames.Add("ABC");
    b.BranchNames.Add("XYZ");
    b.BranchNames.Remove("XYZ");

    foreach (string branchName in b.BranchNames)
    {
        Console.WriteLine(branchName);
    }
    Console.ReadLine();
}
```

```csharp
static void b_ItemRemoved(object sender, EventArgs e)
{
    Console.WriteLine("Item removed!");
}
```

以下是代码的输出：

```text
Item removed!
```

> 作为经验法则，使用泛型 `Collection<T>` 类（因为它更具可扩展性）作为公共方法的返回类型，并使用泛型 `List<T>` 类进行内部实现。

### Summary

泛型允许您在设计时不绑定到特定固定数据类型的情况下定义类型安全的数据结构。最终结果是您的代码变得更安全，而不会牺牲性能。除了展示如何定义自己的泛型类之外，本章还研究了 .NET Framework 类库中提供的一些泛型类，例如泛型 `LinkedList<T>` 和 `Collection<T>` 类。

## 10 Threading

今天的计算机运行速度超过 2GHz，与几年前相比速度提升惊人。几乎所有现代操作系统都是多任务的，这意味着您可以同时运行多个应用程序。然而，如果您的应用程序仍按顺序执行代码，您实际上并没有利用最新处理器的速度提升。您有多少次看到无响应的应用程序在完成诸如执行数学计算或网络传输之类的后台任务后重新恢复？为了充分利用计算机的强大处理能力并编写响应迅速的应用程序，了解和使用线程非常重要。

> **线程是程序内的顺序执行流。程序可以由多个执行线程组成，每个线程都能够独立执行。**

本章解释了如何使用 .NET Framework 中的 `Thread` 类编写多线程应用程序。它向您展示如何：

- 创建新的执行线程并停止它
- 使用各种可用的线程类同步不同的线程
- 编写线程安全的 Windows 应用程序
- 在 Windows Forms 中使用 `BackgroundWorker` 组件来编程后台任务。

### The Need for Multithreading

多线程是编程中最强大的概念之一。使用多线程，您可以将单个应用程序中的复杂任务分解为多个相互独立执行的线程。多线程的一个特别好的用途是在同步性质的任务中，例如 Web 服务调用。默认情况下，Web 服务调用是阻塞调用 — 即调用方代码不会继续，直到 Web 服务返回结果。由于 Web 服务调用通常很慢，这可能导致客户端性能迟缓，除非您采取特殊措施使调用变为异步。

### Part I: C# Fundamentals

为了了解多线程的工作原理，首先来看以下示例：

```csharp
class Program
{
    static void Main(string[] args)
    {
        DoSomething();
        Console.WriteLine("Continuing with the execution...");
        Console.ReadLine();
    }

    static void DoSomething()
    {
        while (true)
        {
            Console.WriteLine("Doing something...");
        }
    }
}
```

这是一个简单的应用程序，它调用 DoSomething() 函数来打印一系列字符串（事实上，它是一个无限循环，永远不会停止；参见图 10-1）。在调用 DoSomething() 函数后，您尝试向控制台窗口打印一个字符串（"Continuing with the execution..."）。然而，由于 DoSomething() 函数正忙于打印自己的输出，"Console.WriteLine("Continuing with the execution...");" 语句永远没有机会执行。

![](img/a977a875c7c627b45d939729705a252e_317_0.png)

图 10-1

此示例说明了应用程序的顺序性质 — 语句按顺序执行。DoSomething() 函数类似于使用 Web 服务，只要 Web 服务不向您返回值（例如由于网络延迟或 Web 服务器繁忙），您的应用程序其余部分就会被阻塞（即无法继续）。

### Starting a Thread

您可以使用线程将应用程序中的语句分解为更小的块，以便它们可以并行执行。例如，您可以使用单独的线程调用前例中的 DoSomething() 函数，让剩余的代码继续执行。

*每个应用程序都包含一个主执行线程。多线程应用程序包含两个或更多执行线程。*

在 C# 中，您可以使用 System.Threading 命名空间中的 Thread 类创建新的执行线程。Thread 类创建并控制线程。Thread 类的构造函数接收一个 ThreadStart 委托，该委托包装您想要作为单独线程运行的函数。以下代码展示了如何使用 Thread 类将 DoSomething() 函数作为单独线程运行：

> 使用 Thread 类时导入 System.Threading 命名空间。

```csharp
class Program
{
    static void Main(string[] args)
    {
        Thread t = new Thread(new ThreadStart(DoSomething));
        t.Start();

        Console.WriteLine("Continuing with the execution...");
        Console.ReadLine();
    }

    static void DoSomething()
    {
        while (true)
        {
            Console.WriteLine("Doing something...");
        }
    }
}
```

请注意，直到您显式调用 Start() 方法，线程才会被启动。当调用 Start() 方法时，DoSomething() 函数会被调用，并且控制立即返回到 Main() 函数。图 10-2 显示了示例应用程序的输出。
