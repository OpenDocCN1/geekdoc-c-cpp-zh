
如果我没提到，`System.Runtime.Interop` 命名空间也定义了一个 `CriticalHandle` 类。该类在所有方面与 `SafeHandle` 类完全相同，但它不提供引用计数功能。`CriticalHandle` 类及其派生类在使用时提供了更好的性能（因为计数器不需要管理）。像 `SafeHandle` 一，`CriticalHandle` 类有两个派生类型：`CriticalHandleMinusOneIsInvalid` 和 `CriticalHandleZeroMinusOneInvalid`。微软构建了一个更安全的系统而非更快的系统，类库不包含派生自这两个任何一个类型。对于你的工作，我建议只有在性能有问题时才使用 `CriticalHandle` 派生类型。如果你证明降低安全性，可以切换到 `CriticalHandle` 派生类型。

# 使用封装原生资源的类型

现在你已经知道如何定义一个封装原生资源的 `SafeHandle` 派类，让我们来看看开发者是如何使用它的。让我们从常见的 `System.IO.FileStream` 类开始说起。`FileStream` 类提供了打开文件从从读取字节、向文件写入字节以及关闭文件的能力。当构造 `FileStream` 对象时，会调用 Win32 `CreateFile` 函数，返回的句柄被保存在 `SafeHandle` 对象中，并通过 `FileStream` 对象中的私有字段维护对该对象的引用。`FileStream` 类还提供了额外的属性（如 `Length`、`Position`、`CanRead`）和方法（如 `Read`、`Write`、`Flush`）。

假设你想编写代码创建一个临时文件，向文件中写入一些字节，然后将其删除。你可能会这样写代码：

```csharp
using System;
using System.IO;
public static class Program {
public static void Main() {// 创建要写入临时文件的字节。
  Byte[] bytesToWrite = new Byte[] { 1, 2, 3, 4, 5 };

  // 创建临时文件。
  FileStream fs = new FileStream("Temp.dat", FileMode.Create);

  // 将字节写入临时文件。
  fs.Write(bytesToWrite, 0, bytesToWrite.Length);

  // 删除临时文件。
  File.Delete("Temp.dat"); // 抛出 IOException
}
```

遗憾的是，如果你构建并运行这段代码，它可能会成功，但极可能不会成功。问题在于，调用 `File` 的静态 `Delete` 方法要求 Windows 在文件仍打开时删除它。因此，`Delete` 会抛出一个 `System.IO.IOException`，带有以下字符串消息：无法访问文件 "Temp.dat"，因为它正被另一个进程使用。

请注意，在某些情况下，文件实际上可能会被删除！如果另一个线程在调用 `Write` 之后调用 `Delete` 之前触发了垃圾回收，`FileStream` 的 `SafeFileHandle` 将调用其 `Finalize` 方法，这将关闭文件并允许 `Delete` 工作。然而，这种情况发生的概率极罕见，因此之前的代码在 99% 以上的情况下都会失败。

允许消费者控制原生资源生命周期的类实现了 `IDisposable` 接口，如下所示。

```csharp
public interface IDisposable {
    void Dispose();
}
```

> **重要** 如果一个类定义了一个字段，该字段的类型实现了释放模式，那么该类本身也应该实现释放模式。`Dispose` 方法应该释放由字段所引的对象。这允许使用该类的人对它调用 `Dispose`，从而释放该类本身使用的资源。

幸运的是，`FileStream` 类实现了 `IDisposable` 接口，其实现调用了 `FileStream` 对象私有 `SafeFileHandle` 句柄的 `Dispose` 方法。现在我们可以修改代码，以便当我们想要避免等待未来发生垃圾回收时显式地关闭文件。以下是修正后的源代码。

```csharp
using System;
using System.IO;

public static class Program {
    public static void Main() {
        // 创建要写入临时文件的字节。
        Byte[] bytesToWrite = new byte[] { 1, 2, 3, 4, 5 };

        // 创建临时文件。
        FileStream fs = new FileStream("Temp.dat", FileMode.Create);

        // 将字节写入临时文件。
        fs.Write(bytesToWrite, 0, bytesToWrite.Length);

        // 在写入文件时显式关闭文件。
        fs.Dispose();

        // 删除临时文件。
        File.Delete("Temp.dat"); // 现在这始终有效。
    }
}
```

现在，当调用 `File` 的 `Delete` 方法时，Windows 看到文件未打开并成功删除了它。

请记住，`Dispose` 并不是保证原生资源清理的。原生资源的清理最终都会发生；调用 `Dispose` 让你控制清理何时发生。此外，调用 `Dispose` 不会从托管堆中删除托管对象。回收托管堆中内存的唯一方法是触发垃圾回收。这意味着在释放了该对象可能使用的任何原生资源后，你仍然可以对托管对象调用方法。

以下代码显示了文件关闭后调用 `Write` 方法，尝试向关闭的文件写入更多字节。显然，这些字节无法写入，当代码执行时，第二次调用 `Write` 方法会抛出一个带有以下字符串消息的 `System.ObjectDisposedException`：无法访问已关闭的文件。

请注意，这里没有发生内存损坏，因为用于 `FileStream` 对象的内存仍然存在于托管堆中；只是对象在被显式释放后无法成功执行其方法。

> 在定义实现 `IDisposable` 接口的自定义类型时，确保在所有方法和属性中编写代码，如果对象已被显式清理，则抛出 `System.ObjectDisposedException`。`Dispose` 方法永远不应该抛出异常；如果被调用多次，它应该直接返回。

重要：通常，我强烈建议不要在代码中显式调用 `Dispose`。原因是 CLR 的垃圾回收器编写得很好，你应该让它尽职责。垃圾回收器知道对象何时不再被应用程序代码访问，只有那时它才会收集该对象。当代码调用 `Dispose` 时，实际上是在说应用程序不再需要该对象了。对于许多应用程序来说，要确定一个对象何时不再被需要是不可能的。

例如，如果你的代码构造了一个新对象，然后将该对象的引用传递给另一个，该方法可以将对象的引用保存在某些内部字段变量（根）中。该方法没有办法知道这种情况发生了。当然，该方法可以调用 `Dispose`，但稍后其他代码可能会尝试访问该对象，导致抛出 `ObjectDisposedException`。我建议只在在你确定必须清理资源的地方调用 `Dispose`（例如尝试删除打开的文件时）。

类似地，可能存在多个线程同时对单个对象调用 `Dispose`。然而，设计指南指出 `Dispose` 不必是线程安全的。原因是因为代码只有在确定没有其他线程正在使用该对象时，才应该调用 `Dispose`。

之前的代码示例显示了如何显式调用类型的 `Dispose` 方法。如果你决定调用 `Dispose`，我强烈建议将该调用放在异常处理块中。这样可以保证清理代码能够执行。因此，将代码写成如下更好。

```csharp
using System;
using System.IO;

public static class Program {
  public static void Main() {
    // 创建要写入临时文件的字节。
    Byte[] bytesToWrite = new Byte[] { 1, 2, 3, 4, 5 };

    // 创建临时文件。
    FileStream fs = new FileStream("Temp.dat", FileMode.Create);
    try {
      // 将字节写入临时文件。
      fs.Write(bytesToWrite, 0, bytesToWrite.Length);
    }
    finally {
      // 完成后显式关闭文件。
      if (fs != null) fs.Dispose();
    }

    // 删除临时文件。
    File.Delete("Temp.dat");
  }
}
```

添加异常处理代码是正确的做法，你必须具备这种勤勉去这样做。坦率地说，C 语言提供了 `using` 语句，它提供了一种简化的语法，产生的代码与上述代码完全相同。以下是使用 C# 语句对前面的代码重写。

```csharp
using System;
using System.IO;

public static class Program {
  public static void Main() {
    // 创建要写入临时文件的字节。
    Byte[] bytesToWrite = new byte[] { 1, 2, 3, 4, 5 };

    // 创建临时文件。
    using (FileStream fs = new FileStream("Temp.dat", FileMode.Create)) {
      // 将字节写入临时文件。
      fs.Write(bytesToWrite, 0, bytesToWrite.Length);
    }

    // 删除临时文件。
    File.Delete("Temp.dat");
  }
}
```

在 `using` 语句中，你初始化一个对象并将其引用保存在变量中。然后通过大括号内的代码更改变量。当你编译时，编译器会自动产生 `try` 和 `finally` 块。在 `finally` 块中，编译器生成的代码将对象强制转换为 `IDisposable` 并调用 `Dispose` 方法。显然，编译器允许 `using` 语句仅用于实现 `IDisposable` 接口的类型。

> 注意 C# 的 using 语句支持初始化多个变量，只要这些变量具有相同类型。它还支持使用已初始化的变量。有关此主题的更多信息，请参阅 C# 程序员参考中的“Using Statements”主题。

![](img/0ce3b788d061e3d3095fa554b1a34adf_561_0.png)

# 一种有趣的 IO.FileStream 类型

`System.FileStream` 类型允许用户打开文件进行读取和写入。为了提高性能，该类型的实现使用了一个内存缓冲区。只有当缓冲区满时，它才会将缓冲区中的内容刷新到文件中。`FileStream` 仅支持字节（bytes）的写入。如果你想写入字符和字符串，可以使用 `System.IO.StreamWriter`，如下代码所示。

```csharp
FileStream fs = new FileStream("Data.dat", FileMode.Create);
StreamWriter sw = new StreamWriter(fs);
sw.Write("Hi there");
```

```csharp
// 下面对 Dispose 的调用是你应该的操作。
sw.Dispose();
// 注意：StreamWriter.Dispose 会关闭 FileStream；
// FileStream 不需要显式关闭。
```

注意，`StreamWriter` 的构造函数接受一个 `Stream` 对象的引用作为参数，这允许将 `FileStream` 对象的引用作为参数传递。在内部，`StreamWriter` 对象保存了 `Stream` 的引用。当你向 `StreamWriter` 对象写入数据时，它会将数据缓冲在自己的内存缓冲区中。当缓冲区满时，`StreamWriter` 将数据写入 `Stream`。

当你通过 `StreamWriter` 完成数据写入后，应该调用 `Dispose`。（由于 `StreamWriter` 类型实现了 `IDisposable` 接口，你也可以在 C# 中配合 `using` 语句使用。）这会导致 `StreamWriter` 对象将其数据刷新到 `Stream` 对象并关闭 `Stream` 对象。

> 注意：你不需要显式对 `FileStream` 对象调用 `Dispose`，因为 `StreamWriter` 会为你调用它。但是，如果你显式调用了 `Dispose`，`FileStream` 将发现该对象已经被清理——该方法将什么都不做并返回。

如果没有代码显式调用 `Dispose` 会发生什么？嗯，在某个时刻，垃圾回收器会正确检测到对象是垃圾并对它们进行终化。垃圾回收器不保证对象终化的顺序。如果 `FileStream` 对象先终化，它会关闭文件。那么当 `StreamWriter` 对象终化时，它将尝试向已关闭的文件写入数据，从而抛出异常。相反，如果 `StreamWriter` 对象先终化，数据将安全地写入文件。

7 你可以通过调用接受 `Boolean leaveOpen` 参数的 `StreamWriter` 构造函数来覆盖此行为。

第 21 章 托管堆与垃圾回收 537

微软如何解决这个问题呢？让垃圾回收器按特定顺序终化对象是不可能的，因为对象之间可以相互引用，垃圾回收器没有办法正确猜出终化这些对象的顺序。微软的解决方案是：`StreamWriter` 类型不支持底层的 `FileStream` 对象。这意味着，如果你忘记对 `StreamWriter` 对象调用 `Dispose`，数据将保证会丢失。微软期望开发者能看到这种一致的数据丢失，并通过通过插入显式的 `Dispose` 调用来修复代码。

> 注意：.NET Framework 提供了一项名为“托管调试助手（MDAs）”的功能。当启用 MDA 时，.NET Framework 会寻找常见的程序员错误和相应的 MDA。在调试器中，它看起来就像抛出了一个异常。有一个可用的 MDA 用来检测 `StreamWriter` 对象在未先进行显式 `Dispose` 的情况下被回收的情况。要在 Microsoft Visual Studio 中启用此 MDA，请打开你的项目并启动 `Debug.Exceptions` 菜单节点并滚动到最后。你会看到 `StreamWriterBufferedDataList` MDA。勾选复选框，以便在 `StreamWriter` 对象的数据丢失时让 Visual Studio 调试器捕获。

# 用于原生句的其他 GC 特性

有时，原生资源会消耗所有内存，而封装它的托管对象只占用极少的内存。这最典型的例子是位图（bitmap）。位图可以占用几兆字节的原生内存，而托管对象很小，因为它只包含一个 `HBITMAP`（一个 4 字节或 8 字节的值）。从 CLR 的角度来看，进程在执行收集之前可以分配数百个位图（使用很少的托管内存）。如果进程正在处理许多位图，进程的内存消耗将以惊人的速度增长。为了解决这种情况，`GC` 类提供了以下两个方法。

```csharp
public static void AddMemoryPressure(Int64 bytesAllocated);
public static void RemoveMemoryPressure(Int64 bytesAllocated);
```

封装可能大型原生资源的类应该使用这些方法来向垃圾回收器提供提示，说明到底消耗了多少内存。垃圾回收器会监控这种压力，当压力变高时，就会强制进行垃圾回收。

某些原生资源的数量是固定的。例如，Windows 曾经有一个限制只能创建五个设备上下文。对应用程序可以打开的文件数量也有限制。同样，从 CLR 的角度来看，进程在执行收集之前可以分配数百个对象（使用很少的内存）。如果原生资源的数量有限，尝试使用比可用数量更多的资源通常会导致抛出异常。
