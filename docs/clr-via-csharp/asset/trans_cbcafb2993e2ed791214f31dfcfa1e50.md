
现在，当你调用此方法并向其传入一个 `SafeWaitHandle` 对象的引用时，CLR 会在调用前递增计数器，并在调用后递减计数器。当然，计数器的操作是以线程安全的方式执行的。这如何提高安全性呢？好吧，如果另一个线程试图释放由 `SafeHandle` 对象包装的本机资源，CLR 知道它实际上不能释放该资源，因为该资源正被非托管函数使用。当非托管函数返回时，计数器递减为 0，资源将被释放。

如果你正在编写或调用将句柄作为 `IntPtr` 操作的代码，你可以从 `SafeHandle` 对象中获取它，但你应该显式地操作引用计数。你可以通过 `SafeHandle` 的 `DangerousAddRef` 和 `DangerousRelease` 方法来实现这一点。你可以通过 `DangerousGetHandle` 方法访问原始句柄。

如果我不提一下 `System.Runtime.InteropServices` 命名空间还定义了一个 `CriticalHandle` 类，那我就失职了。这个类在所有方面都与 `SafeHandle` 类完全相同，只是它不提供引用计数功能。`CriticalHandle` 类及其派生类在使用时会牺牲安全性来换取更好的性能（因为计数器不会被操作）。和 `SafeHandle` 一样，`CriticalHandle` 类也有两个派生类型：`CriticalHandleMinusOneIsInvalid` 和 `CriticalHandleZeroOrMinusOneIsInvalid`。由于 Microsoft 更倾向于安全的系统而非更快的系统，因此类库中不包含从这两个类派生的任何类型。对于你自己的工作，我建议只有在性能成为问题时才使用 `CriticalHandle` 派生类型。如果你能证明降低安全性是合理的，你就可以改用 `CriticalHandle` 派生类型。

### 对托管资源使用终结

> **重要提示** 有些人认为绝不应该对托管资源使用终结。在很大程度上，我同意这些人的看法。因此，你可能想完全跳过本节。对托管资源使用终结是一种超级高级的编码方式，只应在极少数情况下使用。你必须对在 `Finalize` 方法内部调用的代码有完全而深入的了解。此外，你必须知道你调用的代码的行为不会随着未来版本而改变。具体来说，你必须知道你在 `Finalize` 方法中调用的任何代码都不会使用任何可能已经被终结的其他对象。

虽然终结几乎专门用于释放本机资源，但偶尔对托管资源也可能有用。下面是一个类，它会在垃圾回收器每次执行回收时使计算机发出蜂鸣声：

```csharp
internal sealed class GCBeep {
    ~GCBeep() { // This is the Finalize method
        Console.Beep();

        // If the AppDomain isn't unloading and if the process isn't shutting down,
        // create a new object that will get finalized at the next collection.
        if (!AppDomain.CurrentDomain.IsFinalizingForUnload() && !Environment.HasShutdownStarted)
            new GCBeep();
    }
}
```

要使用这个类，你只需构造一个该类的实例。然后每当发生垃圾回收时，对象的 **Finalize** 方法就会被调用，该方法调用 **Beep** 并构造一个新的 **GCBeep** 对象。当下一次垃圾回收发生时，这个新的 **GCBeep** 对象的 **Finalize** 方法将被调用。下面是一个演示 **GCBeep** 类的示例程序：

```csharp
public static class Program {
    public static void Main() {
        // Constructing a single GCBeep object causes a beep to occur every time a GC starts.
        new GCBeep();

        // Construct a lot of 100-byte objects.
        for (Int32 x = 0; x < 10000; x++) {
            Console.WriteLine(x);
            Byte[] b = new Byte[100];
        }
    }
}
```

> **注意** 尽管 **GCBeep** 类很有用，但我会提供一个更有用的 **GCNotification** 类，它允许你检测应用程序，从而让你更深入地了解应用程序的内存使用情况。你会在本章后面的“代”一节的末尾看到这个类。

还要注意，即使类型的实例构造函数抛出异常，类型的 **Finalize** 方法也会被调用。因此，你的 **Finalize** 方法不应假设对象处于良好、一致的状态。下面的代码演示了这一点：

```csharp
internal sealed class TempFile {
    private String m_filename = null;
    private FileStream m_fs;

    public TempFile(String filename) {
        // The following line might throw an exception.
        m_fs = new FileStream(filename, FileMode.Create);

        // Save the name of this file.
        m_filename = filename;
    }
}
```

对于第五种事件，每个 **Finalize** 方法大约有 2 秒的时间返回。如果某个 **Finalize** 方法未能在 2 秒内返回，CLR 就会直接终止进程——不再调用任何 **Finalize** 方法。此外，如果调用所有对象的 **Finalize** 方法耗时超过 40 秒，CLR 同样会直接终止进程。

> **注意** 这些超时值在我撰写本文时是正确的，但 Microsoft 将来可能会更改它们。**Finalize** 方法中的代码可以构造新对象。如果这发生在 CLR 关闭期间，CLR 会继续收集对象并调用其 **Finalize** 方法，直到不再有对象存在或 40 秒时间耗尽。

回顾本章前面介绍的 **GCBeep** 类型。如果 **GCBeep** 对象由于第一种、第二种或第三种垃圾回收原因而被终结，则会构造一个新的 **GCBeep** 对象。这是没问题的，因为应用程序会继续运行，并且假定将来还会发生更多的回收。然而，如果 **GCBeep** 对象由于第四种或第五种垃圾回收原因而被终结，就不应该构造新的 **GCBeep** 对象，因为该对象将在 AppDomain 卸载或 CLR 关闭时被创建。如果创建了这些新对象，CLR 将有一大堆无用的事情要做，因为它会继续调用 **Finalize** 方法。

为了防止构造新的 **GCBeep** 对象，**GCBeep** 的 **Finalize** 方法会调用 **AppDomain** 的 **IsFinalizingForUnload** 方法，并查询 **System.Environment** 的 **HasShutdownStarted** 属性。如果对象的 **Finalize** 方法是因为 AppDomain 正在卸载而被调用，**IsFinalizingForUnload** 方法返回 **true**。如果对象的 **Finalize** 方法是因为进程正在终止而被调用，**HasShutdownStarted** 属性返回 **true**。

### 终结的内部机制

从表面上看，终结似乎非常简单：你创建一个对象，当它被回收时，其 **Finalize** 方法就会被调用。但一旦深入探究，终结要比这复杂得多。

当应用程序创建一个新对象时，**new** 运算符会从堆中分配内存。如果对象的类型定义了 **Finalize** 方法，那么在类型实例构造函数被调用之前，一个指向该对象的指针会被放入 *终结列表*。终结列表是由垃圾回收器控制的一种内部数据结构。列表中的每一项都指向一个对象，该对象的 **Finalize** 方法应在该对象的内存可被回收之前调用。

图 21-5 显示了一个包含多个对象的堆。其中一些对象可以从应用程序的根访问，而另一些则不能。当对象 C、E、F、I 和 J 被创建时，系统检测到这些对象的类型定义了 **Finalize** 方法，因此将这些对象的指针添加到了终结列表中。
