

## Note

一个 *thread* 是应用程序中的一个单独的执行路径。Windows 使用线程使应用程序能够并发执行多个操作。

垃圾收集器是一段复杂的软件，它是自调优的，并实现了一系列优化，试图在保持内存可用性和维持应用程序性能的需求之间取得平衡。本书超出范围的是垃圾收集器使用的内部算法和结构的细节（而且 Microsoft 不断改进垃圾收集器执行工作的方式），但在高层面上，垃圾收集器采取的步骤如下：

- 1. 它构建所有可达对象的映射。它通过反复跟随对象内部的引用字段来完成此操作。垃圾收集器非常仔细地构建此映射，并确保循环引用不会导致无限递归。任何 *not* 在此映射中的对象都被视为不可达。
- 2. 它检查是否有任何不可达对象具有需要运行的析构函数（称为 *finalization* 的过程）。任何需要终结的不可达对象都会被放置在名为 *freachable queue*（读作“F-reachable”）的特殊队列中。
- 3. 它通过将 *reachable* 对象向下移动堆来释放剩余的不可达对象（那些不需要终结的对象），从而对堆进行碎片整理并释放其顶部的内存。当垃圾收集器移动一个可达对象时，它也会更新对该对象的任何引用。
- 4. 在这一点上，它允许其他线程恢复。
- 5. 它通过在自己的线程上运行 *Finalize* 方法来终结需要终结的不可达对象（现在在 *freachable* 队列中）。

## Recommendations

编写包含析构函数的类会增加代码和垃圾收集过程的复杂性，并使程序运行变慢。如果你的程序不包含任何析构函数，垃圾收集器就不必将不可达对象放置在 *freachable* 队列中并对其进行终结。显然，不做某事比做某事更快。因此，尽量避免使用析构函数，除非你真的需要它们——仅在需要回收非托管资源时使用它们。（你可以考虑使用 *using* 语句，如本章后面将描述的那样。）

编写析构函数时需要非常小心。特别是，要注意如果你的析构函数调用其他对象，那么这些其他对象可能 *already* 已被垃圾收集器调用过其析构函数。记住，终结的顺序是不确定的。因此，确保析构函数彼此不依赖也不重叠——例如，不要有两个析构函数尝试释放同一资源。

## Resource management

有时在析构函数中释放资源是不明智的；有些资源太宝贵了，不能随意等待不确定的时间直到垃圾收集器实际释放它们。稀缺资源如内存、数据库连接或文件句柄需要被释放，并且需要尽快释放。在这些情况下，你唯一的办法就是自己释放资源。你可以通过创建 *disposal method*——一个显式释放资源的 方法来实现这一点。如果一个类具有处置方法，你可以调用它并控制资源释放的时间。

## Note

术语 *disposal method* 指的是方法的目的而不是其名称。处置方法可以使用任何有效的 C# 标识符命名。

## Disposal methods

实现处置方法的类的一个例子是来自 *System.IO* 命名空间的 *TextReader* 类。此类提供从顺序输入流读取字符的机制。*TextReader* 类包含一个名为 *Close* 的虚方法，用于关闭流。*StreamReader* 类（从流（如打开的文件）读取字符）和 *StringReader* 类（从字符串读取字符）都派生自 *TextReader*，并且都重写了 *Close* 方法。以下是一个使用 *StreamReader* 类从文件读取文本行然后在屏幕上显示它们的示例：

Click here to view code image

```
TextReader reader = new StreamReader(filename);
string line;
while ((line = reader.ReadLine()) != null)
{
    Console.WriteLine(line);
}
reader.Close();
```

*ReadLine* 方法将流中的下一行文本读取到字符串中。

*ReadLine* 方法在流中没有剩余内容时返回 *null*。在你完成对 *reader* 的使用后调用 *Close* 以释放文件句柄和相关资源非常重要。然而，这个示例存在一个问题：它对异常不安全。如果对 *ReadLine* 或 *WriteLine* 的调用抛出异常，对 *Close* 的调用将不会发生；它将被绕过。如果这种情况经常发生，你将耗尽文件句柄，无法再打开任何文件。

## Exception-safe disposal

确保处置方法（例如 *Close*）无论是否有异常总是被调用的一种方法是，在 *finally* 块中调用处置方法。下面是使用此技术编写的上述示例：

Click here to view code image

```
TextReader reader = new StreamReader(filename);
try
{
    string line;
    while ((line = reader.ReadLine()) != null)
    {
        Console.WriteLine(line);
    }
}
finally
{
    reader.Close();
}
```

使用这样的 *finally* 块是可行的，但它有几个缺点，使其成为不太理想的解决方案：

- 如果你需要释放多个资源，它很快就会变得难以处理。（你最终会得到嵌套的 *try* 和 *finally* 块。）
- 在某些情况下，你可能需要修改代码以使其符合此习惯用法。（例如，你可能需要重新排列资源引用的声明，记住将引用初始化为 *null*，并在 *finally* 块中记住检查引用是否不是 *null*。）
- 它未能创建解决方案的抽象。这意味着解决方案难以理解，并且你必须在需要此功能的地方重复代码。
- 资源引用在 *finally* 块之后仍然在作用域内。这意味着你可能会意外地尝试在资源已释放后使用资源。

*using* 语句旨在解决所有这些问题。

## The *using* statement and the *IDisposable* interface

*using* 语句为控制资源生命周期提供了一种简洁的机制。你可以创建一个对象，并且该对象将在 *using* 语句块结束时被销毁。

## Important

不要将本节中显示的 *using* 语句与将命名空间引入作用域的 *using* 指令混淆。遗憾的是，同一个关键字有两个不同的含义。

*using* 语句的语法如下：

Click here to view code image

```
using ( type variable = initialization )
{
    StatementBlock
}
```

确保你的代码始终对 *TextReader* 调用 *Close* 的最佳方法是：

Click here to view code image

```
using (TextReader reader = new StreamReader(filename))
{
    string line;
    while ((line = reader.ReadLine()) != null)
    {
        Console.WriteLine(line);
    }
}
```

这个 *using* 语句与以下转换完全等价：

Click here to view code image

```
{
    TextReader reader = new StreamReader(filename);
    try
    {
        string line;
        while ((line = reader.ReadLine()) != null)
        {
            Console.WriteLine(line);
        }
    }
    finally
    {
        if (reader != null)
        {
            ((IDisposable)reader).Dispose();
        }
    }
}
```

## Note

using 语句为作用域目的引入了自己的块。这种安排意味着你在 using 语句中声明的变量会在嵌入语句结束时自动超出作用域，你无法意外尝试访问已释放的资源。

你在 using 语句中声明的变量必须是实现 IDisposable 接口的类型。IDisposable 接口位于 System 命名空间中，只包含一个名为 Dispose 的方法：

```
namespace System
{
    interface IDisposable
    {
        void Dispose();
    }
}
```

Dispose 方法的目的是释放对象使用的任何资源。碰巧的是，StreamReader 类实现了 IDisposable 接口，并且其 Dispose 方法调用 Close 来关闭流。你可以使用 using 语句作为一种简洁、异常安全且健壮的方式来确保资源始终被释放。这种方法解决了手动 try/finally 解决方案中存在的所有问题。你现在拥有一个执行以下操作的解决方案：

- 如果需要释放多个资源，扩展性良好。
- 不扭曲程序代码的逻辑。
- 抽象问题并避免重复。
- 健壮。你不能在 using 语句结束后再意外引用在 using 语句中声明的变量（在本例中为 reader），因为它不再在作用域中——你会得到编译时错误。

## Calling the Dispose method from a destructor

在编写自己的类时，你应该编写析构函数还是实现 IDisposable 接口以便类的实例可以通过 using 语句管理？对析构函数的调用会发生，但你只是不知道何时发生。另一方面，你确切知道对 Dispose 方法的调用何时发生，但你无法确定它是否真的会发生，因为它依赖于使用你的类的程序员记住编写 using 语句。然而，通过从析构函数中调用它，可以确保 Dispose 方法始终运行。这作为一个有用的备份。你可能会忘记调用

