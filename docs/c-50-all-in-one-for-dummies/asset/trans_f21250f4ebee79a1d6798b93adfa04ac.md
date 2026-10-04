

## 446 给老沃尔特的流式写入

`catch` 块就像足球守门员：它的作用是捕获程序中可能发生的任何文件错误。`catch` 输出一条错误消息，包括 `err` 文件的名称。它不会输出简单的文件名——而是为了你的方便，输出整个文件名，包括路径。它这是通过使用 `Path.Combine()` 方法，将通过 `Directory` 类获取的当前目录名称追踪到你输入的文件上实现的。（`Path` 是一个设计用于处理路径信息的类。`Directory` 提供了处理目录的属性和方法。）该块为你提供了关于异常的各种信息，包括异常的异常、那些异常的异常——我放弃了。

![](img/6df7bb88e9302e98442acc219cfbd7fc_471_0.png)

路径是文件文件夹的全名。例如，在文件 `c:\user\directory.txt` 中，路径是 `c:\user`。

`Combine()` 方法足够简单，它能意识到对于像 `c:\test.txt` 这样的文件，路径并不在当前目录中。`Path.Combine()` 也是确保两个路径段正确组合的最安全方法，包括它们之间的路径分隔符。（在 Windows 中，路径分隔符是 `\`。.NET Framework 库包含了许多专门针对运行在多个操作系统上的 C# 程序的特性，例如用于 Unix 的 Mono，我将在书中讨论它。）

遇到 `while` 循环的结束时（无论是成功完成 `try` 块还是结束了 `catch` 块），程序都会返回 `while` 循环的顶部，允许用户写入另一个文件。程序的几个示例所示。我的输入是**粗体**的：

```
Enter filename (Enter blank to quit): Test1.txt
Enter text: some stuff
This is some
```

```
Enter filename (Enter blank to quit): Test1.txt
Error on file: C:\Programs\FileWrite\bin\Debug\Test1.txt
The file 'C:\Programs\FileWrite\bin\Debug\Test1.txt' already exists.
```

```
Enter filename (Enter blank to quit): Test2.txt
Enter text:
I messed up there. I should have called it Test2.txt.
```

当我向 `Test1.txt` 输入一些随机文本时，一切进展都很顺利。然而，当我尝试再次打开 `Test1.txt` 时，程序会吐出一个消息，其核心意思是“文件已存在”，并附带文件名。文件的路径被“折磨”了，因为“当前目录”是 Visual Studio 放置可执行文件的所在目录。纠正我的错误，我输入了一个接受的文件名——如 `Test2.txt`——它没有抱怨。

### 使用更好的方法：using 语句

现在你已经运行了 `FileStream` 和 `StreamWriter`，我应该指出在 C# 中处理流的主要方法——在 `using` 语句内部：

```csharp
using (resource)
{
  }
```

`using` 是一种自动化的清理流过程的结构。当遇到 `using` 块的大括号时，C# 会为你管理“刷新”（flushing）流并关闭它。（“刷新”是在流被关闭之前，将流缓冲区中任何剩余的字节推送到关联文件。可以想象为将最后剩下的数据挤出流。）`using` 消除了在写入文件后忘记刷新和关闭文件的常见错误，导致周围留下许多打开的文件。使用 `using`，你需要这样写：

```csharp
Stream file fileStream = null;
TextWriter writer = null;
try {
  // 创建并使用流，然后...
}
finally {
  stream.Flush();
  stream.Close();
  stream = null;
}
```

我在 `try` 块上方声明了流和写入（这样它们在方法中是可见的）。我还使用了抽象类而不是具体的 `FileStream` 和 `StreamWriter` 类型来声明 `FileStream` 和写入变量。这是一个良好的做法。我将它们设置为 `null`，这样编译器就不会对未初始化的变量抱怨。在 `FileWrite` 示例中编写 I/O 代码的首选方法如下：

```sharp
// 准备文件流。
FileStream fs = File.Open(fileName, FileMode.Create, FileAccess.Write);
```

| 第三卷 |
| 第 3 章 |

![](img/6df7bb88e9302e98442acc219cfbd7fc_472_0.png)

```csharp
// 将 fs 变量传递给 using 语句中的 StreamWriter。
using (StreamWriter sw = new StreamWriter(fs))
{
    // sw 仅存在于块内，这是一个局部作用域。

    // 从控制台一次读取一个字符串，将其输出到
    // FileStream 以写入。
    Console.WriteLine("Enter text; enter blank line to stop");
    while (true)
    {
        // 从控制台读取下一行；如果行为空则退出。
        string input = Console.ReadLine();
        if (input == null)
        {
            break;
        }
        // 通过流将刚刚读取的行写入输出文件。
        sw.WriteLine(input);
    }
    // 回到循环获取另一行，fs 现在已关闭。
    fs = null; // 确保你不再访问 fs。
```

`using` 关键字之后的项是你的“资源获取”部分，你可以在那里分配一个或多个资源作为流、读取器/写入器、字体等。（如果分配了多个资源，它们必须是相同的类型。）该部分之后是包含块，由外部大括号界定。

> 语句块不是循环。该块定义了一个作用域，就像 `try` 块或方法一样。（在块内定义的变量在块外部不存在。因此， StreamWriter sw 在块外部是不可见的。）我将在 I 中讨论作用域。

在示例的顶部，在资源获取部分，你设置了一个资源——在本例中，封装在现有 `FileStream` 之上的新 `StreamWriter`。在块内部，你执行文件的 I/O 代码。

在 `using` 块结束时，C# 会自动刷新 `StreamWriter` 并关闭它，然后释放 `FileStream`，这处理了在被关闭之前流中的任何剩余字节。具体来说，它是针对实现 `IDisposable` 接口对象的。`using` 语句确保对象的 `Dispose()` 方法被调用。`IDisposable` 主要关于释放资源，即操作系统之外的资源，如文件句柄和图形资源。`File` 打开了必须释放的文件句柄，这就是为什么我在这里提到 `IDisposable`。（许多类和结构都实现了 `IDisposable`；你的类如果有需要也可以。）

我没有在书中介绍 `IDisposable`，但你应该计划在使用 C# 能力时熟悉它。正确实现它与我在第二卷中简要提到的不确定垃圾回收有关，并且可能复杂。所以 `using` 适用于实现了 `IDisposable` 的类和结构，你可以在帮助中检查。它不适用于任何类型的对象。注意：C# 内置类型 `int`、`double`、`char` 没有实现 `Disposable`。`StreamWriter` 的基类 `TextWriter` 实现了该接口。在帮助中，它看起来如下：

```csharp
public abstract class StreamWriter : MarshalByRefObject, IDisposable
```

块之后， StreamWriter 不再存在，但 `fs` 变量仍然存在（假设你在 `using` 语句外部创建了它）。如果你尝试对流执行操作，将得到一个异常，提示你无法访问已关闭的对象。当你不确定时，检查帮助你计划实现的类或结构是否实现了 `IDisposable`。

