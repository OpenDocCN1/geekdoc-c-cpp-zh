

# 垃圾回收器是如何工作的？

垃圾回收器在自己的线程中运行，并且只能在特定时间执行——通常当你的应用程序到达方法的末尾时。当它运行时，应用程序中运行的其他线程将临时停止，因为垃圾回收器可能需要移动对象并更新对象引用，而它在对象在使用期间是无法执行这些操作的

> 注意
线程是应用程序中独立的执行路径。Windows 使用线程使应用程序能够并发执行多个操作。

垃圾回收器是一个复杂的软件，它具有自调优功能并实现了一些优化，以尝试在保持内存可用性与维持应用程序性能的需求之间取得平衡。垃圾回收器使用的内部算法和结构的细节超出了本书的范畴（而且微软在不断完善垃圾回收器执行工作的方式），但从高层次来说，垃圾回收器采取的步骤如下：

- 1. 它构建一个所有可达对象的映射。它通过反复跟踪对象内部的引用字段来实现这一点。垃圾回收器非常小心地构建此映射，并确保循环引用不会导致无限递归。不在此映射中的任何对象都被视为不可达的。
- 2. 它检查任何不可达对象是否具有需要运行的终结器（此过程称为终结化）。任何需要终结化的不可达对象都被放在一个名为可达队列（reachable queue，读作 F-reachable）的特殊队列中。
- 3. 它通过将可达对象向下移动来释放剩余的不可达对象（那些不需要终结化的对象），从而消除堆碎片并释放顶部的内存。当垃圾回收器移动可达对象时，它也会更新对该对象的任何引用。
- 4. 它允许所有其他线程恢复，然后在它自己的线程上运行 Finalize 方法，对需要终结化的不可达对象（现在位于 freachable 队列中）进行终结。

# 建议

编写终结器的类会增加代码和垃圾回收过程的复杂度，这会让你的程序运行变慢。如果你的程序不包含任何终结器，垃圾回收器就不需要将不可达对象放入 freachable 队列并对其进行终结化。显然，什么都不做比做某些事更快。因此，除非确实需要回收未托管资源，否则请避免使用终结器。（你可以考虑使用 `using` 语句，将在本章稍后部分描述。）

在编写终结器时要小心。特别要注意，如果你的终结器调用了其他对象，那些其他对象可能已经被垃圾回收器调用过终结器。记住，终结化的顺序是不保证的。因此，确保终结器之间不要相互依赖或重叠。例如，不要让两个终结器尝试释放同一个资源。

# 资源管理

有时，在终结器中释放资源是不可接受的。某些资源价值太高，不能就在那里等待任意长时间直到垃圾回收器释放它们。

稀缺资源（如内存、数据库连接和文件句柄）需要被释放，而且需要尽快释放。在这些情况下，你唯一的选择是自己释放资源。你可以通过创建一个释放方法（disposal method）来实现这一点——该方法显式地释放资源。如果一个类具有释放方法，你就可以调用它并控制资源释放的时机。

> 注意
“释放方法”一词指的是方法的目的，而不是它的名称。释放方法可以使用任何有效的 C# 标识符命名。

# 释放方法

实现释放方法的类示例是 `System.IO` 命名空间下的 `TextReader` 类。该类提供了一种从顺序输入流中读取字符的机机制。

`TextReader` 类包含一个名为 `Close` 的虚方法，用于关闭流。`StreamReader` 类（从流如打开的文件中读取字符）和 `StringReader` 类（从字符串中读取字符）都派自 `TextReader`，并且都重写了 `Close` 方法。

这是一个使用 `StreamReader` 类从文件读取文本行并显示在屏幕上的示例：

点击此处查看代码图像

```
TextReader reader = new StreamReader(filename);
string line;
while ((line = reader.ReadLine()) is not null)
{
    Console.WriteLine(line);
}
reader.Close();
```

`ReadLine` 方法从流中读取下一行文本并转换为字符串。如果流中没有剩余，`ReadLine` 方法返回 `null`。在完成对 `reader` 操作后调用 `Close` 以释放文件是非常重要的。

# 异常安全的释放

确保方法（如 `Close`）无论是否发生异常总是被调用的一种方法是使用 `finally` 块。以下是使用此技术的示例：

```
TextReader reader = new StreamReader(filename);
try
{
    string line;
    while ((line = reader.ReadLine()) is not null)
    {
        Console.WriteLine(line);
    }
}
finally
{
    if (reader is not null)
    {
        reader.Close();
    }
}
```

像这样的 `finally` 块虽然有效，但它有几个缺点，使其不那么理想：

- 如果你需要释放多个一个资源，它会迅速变得难以处理。你最终会得到嵌套的 `try` 和 `finally` 块。
 它的扩展性不好——如果你需要释放多个资源。
- 它扭曲了程序代码的逻辑。
- 它没有抽象问题并避免重复。
- 你可能会在 `finally` 语句结束后意外地引用在 `try/finally` 块内声明的变量（在本例中为 `reader`），因为它仍在……

# using 语句和 IDisposable 接口

`using` 语句提供了一种整洁的机制来控制资源的生命周期。在 `using` 语句中声明的变量必须是实现了 `IDisposable` 接口的类型。

`using` 语句的语法如下：

```
using ( type = initialization )
{
    StatementBlock
}
```

以下是确保你的代码对 `TextReader` 调用 `Close` 的最佳方式：

```
using (TextReader reader = new StreamReader(filename))
{
    string line;
    while ((line = reader.ReadLine()) is not null)
    {
        Console.WriteLine(line);
    }
}
```

此 `using` 语句等于以下转换：

```
{
    TextReader reader = new StreamReader(filename);
    try
    {
        string line;
        while ((line = reader.ReadLine()) is not null)
        {
            Console.WriteLine(line);
        }
    }
    finally
    {
        if (reader is not null)
        {
            ((IDisposable)reader).Dispose();
        }
    }
}
```

# 注意
`using` 语句引入了自己的作用域。这意味着在 `using` 语句中声明的变量在语句结束时自动离开作用域，你无法意外访问已释放的资源。

在 `using` 语句中声明的变量必须是实现了 `IDisposable` 接口的类型。`IDisposable` 接口位于 `System` 命名空间，并仅包含一个方法 `Dispose`：

```
namespace System
{
    interface IDisposable
    {
        void Dispose();
    }
}
```

`Dispose` 方法的目的是释放对象使用的资源。恰好 `StreamReader` 类实现了 `IDisposable` 接口，其 `Dispose` 方法调用 `Close` 来关闭流。你可以采用 `using` 语句作为一种整洁、异常安全且健壮的方法来确保资源始终被释放。这种方法解决了手动 `try/finally` 解决方案的所有问题。你现在拥有一个具有以下解决方案：

- 如果你需要释放多个资源，它的扩展性良好。
- 不扭曲程序代码的逻辑。
- 抽象了问题并避免了重复。
- 实现了健壮性。你无法在 `using` 语句结束后意外引用在其内部声明的变量（在本例中为 `reader`），因为它不再在作用域内；你会得到编译时错误。

**重要** 不要将本节所示的 `using` 语句与引入命名空间作用域的 `using` 指令混淆。

# 从终结器中调用 Dispose 方法

在编写类时，我们应该编写终结器？还是我们应该实现 `IDisposable` 接口，以便类的实例可以由 `using` 语句管理

