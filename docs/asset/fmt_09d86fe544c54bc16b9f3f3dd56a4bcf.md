
> 重要 如果你熟悉 C++，你会注意到 C# 定义 `Finalize` 方法所需的特殊语法看起来像你定义 C++ 析构函数的语法。C# 编程语言规范规定了这种析构函数。然而，`Finalize` 方法与 C++ 析构函数完全不工作，这给从另一种语言迁移的开发者造成了很大困惑。
> 问题在于，开发者错误地认为 C# 析构函数语法意味着对象将像在 C++ 中那样被确定性地析构。然而，CLR 不支持确定性析构，这是 C++ 提供的。`Finalize` 方法通常实现为调用 `Win32 CloseHandle`，传递原生资源的句柄。`FileStream` 类型定义了一个句柄字段来标识原生资源。`FileStream` 类型还定义了 `Finalize` 方法，它内部调用 `CloseHandle`；确保当 `FileStream` 对象被确定为垃圾时，句柄被关闭。如果封装原生资源的类型未能定义 `Finalize` 方法，原生资源将不会关闭，并将导致资源泄漏，直到进程终止，此时操作系统将回收原生资源。

# 使用 `CriticalFinalizer` 类型 保证析构化

为了让开发者的工作更简单、更安全，`System.Runtime.ConstrainedExecution` 命名空间定义了一个 `CriticalFinalizerObject` 类，如下：

```
public abstract class CriticalFinalizerObject {
    protected CriticalFinalizerObject() { /* 这里没有代码 */ }

    // 这是 Finalize 方法
    ~CriticalFinalizerObject() { /* 这里没有代码 */ }
}
```
我知道你觉得这个类看起来无趣，但 Runtime 以非常特殊的方式处理该类及其派类。特别是，CLR 通过三个核心功能扩展了它：

- 当任何 `CriticalFinalizerObject` 派生类型第一次构造时，CLR 会立即编译继承链中的所有 `Finalize` 方法。在对象构造时编译这些方法保证了当对象被确定为垃圾时，原生资源将被释放。如果没有提前编译 `Finalize` 方法，CLR 可能找不到足够的内存来编译 `Finalize` 方法，从而阻止其执行，导致原生资源泄漏。或者，如果 `Finalize` 方法引用了另一个程序集中的类型，而 CLR 未能定位该程序集。

- 在调用非 `CriticalFinalizerObject` 派类的 `Finalize` 方法后，CLR 会调用 `CriticalFinalizerObject` 派类的 `Finalize` 方法。这确保了托管资源类具有 `Finalize` 方法可以访问 `CriticalFinalizerObject` 派生类型。这确保了托管资源类具有 `Finalize` 方法可以访问 `CriticalFinalizerObject` 派生类型。这确保了托管资源类具有 `Finalize` 方法可以访问 `CriticalFinalizerObject` 派生类型。这确保了托管资源类具有 `Finalize` 方法可以访问 `CriticalFinalizerObject` 派生类型。这确保了托管资源类具有 `Finalize` 方法可以访问 `CriticalFinalizerObject` 派生类型。（等待，清理重复：CLR 在调用非 `CriticalFinalizerObject` 派类的 `Finalize` 方法后，调用 `CriticalFinalizerObject` 派类的 `Finalize` 方法。这确保了托管资源类具有 `Finalize` 方法可以访问 `CriticalFinalizerObject` 派生类型。）

- 在调用非 `CriticalFinalizerObject` 派类的 `Finalize` 方法后，CLR 会调用 `CriticalFinalizerObject` 派类的 `Finalize` 方法。这确保了托管资源类具有 `Finalize` 方法可以访问 `CriticalFinalizerObject` 派生类型。（完善逻辑：这确保即使在 `AppDomain` 被强行中止的情况下，原生资源也会释放。）

- 这确保了托管资源类具有 `Finalize` 方法可以访问 `CriticalFinalizerObject` 派生类型。

# `SafeHandle` 及其类型

# 21 自动内存管理（垃圾回收） 53

为了让开发者的生活更轻松、更安全，`System.Runtime.InteropServices` 命名空间包含一个名为 `SafeHandle` 类，如下（我在方法中添加了注释说明它们的作用）：

```
public abstract SafeHandle : CriticalFinalizerObject, IDisposable {
// 这是指向原生资源的句柄
protected IntPtr handle;

protected SafeHandle(IntPtr invalidHandleValue, Boolean ownsHandle) {
    this.handle = invalidHandleValue;
    // 如果 ownsHandle 为 true，则原生资源被关闭
    // 此 SafeHandle 派生对象被回收
}

protected void SetHandle(IntPtr handle) {
    this.handle = handle;
}
```

```
// 你可以通过调用 Dispose 或 Close 来显式释放资源
public void Dispose() { Dispose(true); }
public void Close() { Dispose(true); }
```

```
// 默认实现（所示）正是你需要的。
// 强烈不建议覆盖此方法。
protected virtual void Dispose(Boolean disposing) {
    // 默认实现忽略参数。
    // 如果资源已经释放，直接返回
    // 设置标记指示此资源已释放
    // 调用虚方法 ReleaseHandle
    // 调用 GC.Finalize(this) 防止调用 Finalize
    // 如果 ReleaseHandle 返回 true，则返回
    // 触发 ReleaseHandleFailed 托管调试助手 (MDA)
}
```

```
// 默认的析构化实现（所示）正是你需要的。
// 非常不建议覆盖此方法。
-SafeHandle() { Dispose(false); }
```

```
// 派生类覆盖此方法来实现释放资源的代码
protected abstract Boolean ReleaseHandle() {
```

```
public void SetHandleAsInvalid() {
    // 设置标记指示此资源已释放
    // 调用 GC.SuppressFinalize(this) 防止 Finalize 被调用
}
```

```
public Boolean IsClosed {
    get {
        // 返回标记指示资源是否已释放
    }
}
```

现在，微软意识到最常用的原生资源是由 Windows 句柄提供的（32 位系统上的 32 位值，64 位系统上的 64 位值）。再次，

## 第21 章 自动内存管理（垃圾回收）

关于 `SafeHandle` 类需要注意的第一点是它派自 `CriticalFinalizerObject`；这确保了它能获得 CLR 的特殊对待。第二点是该类是抽象的；预期会有另一个类派自 `SafeHandle`，并且该类将重写保护构造函数、抽象方法 `ReleaseHandle` 以及抽象属性 `IsInvalid` 的 getter。

在 Windows 中，如果句柄值为 0 或 -1，则它是无效的。`Microsoft.Win32.SafeHandles` 命名空间包含另一个 `SafeHandleZeroOrMinusOneIsInvalid` 的辅助类，其结构如下：

```csharp
public abstract class SafeHandleZeroOrMinusOneIsInvalid : SafeHandle {
    protected SafeHandleZeroOrMinusOneIsInvalid(Boolean ownsHandle) {
        base(IntPtr.Zero, ownsHandle) {
    }

    public override Boolean IsInvalid {
        if (base.handle == IntPtr.Zero) return true;
        if (base.handle == (IntPtr)(-1)) return true;
        return false;
    }
}
```

再次，你会注意到 `SafeHandleZeroOrMinusOneIsInvalid` 类是抽象的，因此，必须有另一个类派自它以重写保护构造函数和抽象方法 `ReleaseHandle`。.NET Framework 仅提供了少数派自 `SafeHandleZeroOrMinusOneIsInvalid` 的类，包括 `SafeFileHandle`、`SafeRegistryHandle`、`WaitHandle` 和 `SafeBuffer`。以下是 `SafeHandle` 类的样子：

```csharp
public sealed class SafeFileHandle : SafeHandleZeroOrMinusOneIsInvalid {
    public SafeFileHandle(IntPtr preexistingHandle, Boolean ownsHandle) {
        base(ownsHandle)
        base.SetHandle(preexistingHandle);
    }

    protected override Boolean ReleaseHandle() {
        // 告诉 Windows 我们想要关闭原生资源
        return Win32Native.CloseHandle(base.handle);
    }
}
```

`SafeWaitHandle` 的实现方式与上面 `SafeFileHandle` 类类似。之所以存在具有相似实现的不同类，唯一目的是实现类型安全；编译器不会将文件作为预期等待句柄方法的参数，反之亦然。`SafeRegistryHandle` 类的 `ReleaseHandle` 方法调用了 `Win32 RegCloseKey` 函数。

如果 .NET Framework 包含封装各种资源的额外类就很好。例如，可以想象诸如 `SafeProcessHandle`、`SafeThreadHandle`、`SafeTokenHandle`、`SafeFileMappingHandle`、`SafeArea`（其 `ReleaseHandle` 方法将调用 `Win32 UnmapViewOf` 函数）、`SafeLibrary`（其 `ReleaseHandle` 方法将调用 `Win32 FreeLibrary` 函数）、`SafeLocalAllocHandle`（其 `ReleaseHandle` 方法将调用 `Win32 LocalFree` 函数）等。

列出的所有类（以及更多）实际上随框架类库（FCL）一起发布。然而，这些类并没有公开；它们都是 `MSCore.dll` 或 `System.dll` 内部的。微软没有公开这些类，是因为他们不想测试它们，也不想花时间为它们编写文档。但是，如果你工作中需要这些任何一个类，我建议你使用如 `ILasm.exe` 或某些 IL 反编译器器来提取这些类的代码，并将代码集成到你的项目源代码中。所有这些类的实现都非常简单，从零开始编写它们也会相当容易。

## 使用 `SafeHandle` 类型与非托管代码互操作

如前所示，派自 `SafeHandle` 的类非常有用，因为它们确保了在发生垃圾回收时会释放原生资源。除了我们已经讨论的之外，`SafeHandle` 还提供了两个功能。在与非托管代码进行互操作的场景下，CLR 给派自 `SafeHandle` 的类型特殊对待。例如，让我们检查以下代码：

```csharp
using System;
using System.Runtime.InteropServices;
using Microsoft.Win32.SafeHandles;

internal static class SomeType {
    [DllImport("Kernel32", CharSet=CharSet.Unicode, EntryPoint="CreateEvent")]
    // 这个原型并不健壮
    private static extern IntPtr CreateEventB(IntPtr pSecurityAttributes, Boolean manualReset, Boolean initialState, String name);

    // 这个原型是健壮的
    [DllImport("Kernel32", CharSet=CharSet.Unicode, EntryPoint="CreateEvent")]
    private static extern SafeWaitHandle CreateEvent(
        IntPtr pSecurityAttributes, Boolean manualReset, Boolean initialState, String name);

    public static void SomeMethod() {
        IntPtr handle = CreateEventBatch(IntPtr.Zero, false, false, null);
        SafeWaitHandle swh = CreateEvent(IntPtr.Zero, false, false, null);
    }
}
```

你会注意到 `CreateEvent` 方法的原型返回一个 `IntPtr`。在 .NET Framework 2.0 版本之前，`Safe` 类不存在，你必须使用 `IntPtr` 类型来表示句柄。派自 `SafeHandle` 的类非常有用，因为它们确保了在发生垃圾回收时会释放原生资源。除了我们已经讨论的之外，`SafeHandle` 还提供了两个功能。在与非托管代码进行互操作的场景下，CLR 给派自 `SafeHandle` 的类型特殊对待。例如，让我们检查以下代码：

## 538 第 IV 部分 核心

```csharp
internal sealed class GCBeep {
    GCBeep() { // 这是 Finalize 方法
        Console.Beep();
```

```csharp
// 如果 AppDomain 正在卸载且进程没有关闭，
// 则创建一个将在下一次收集时进行终结化的对象。
if (!AppDomain.CurrentDomain.IsFinalizingForUnload) && Environment.HasShutdownStarted)
    new GCBeep();
```

```csharp
}
```

要使用此功能，你只需要构造一个类实例。然后，每当发生垃圾回收时，对象的 `Finalize` 方法就会被调用，该方法会调用 `Beep` 并构造一个新的 `GCBeep` 对象。当再次发生垃圾回收时，新的 `GCBeep` 对象的 `Finalize` 方法也会被调用。这里有一个演示了 `GCBeep` 类的示例程序：

```csharp
public static class Program {
    public static void Main() {
        // 构造单个 GCBeep 对象会导致每次 GC 开始时都产生蜂鸣声。
        new GCBeep();

        // 创建大量 100 字节的对象。
        for (Int32 x = 0; x < 10000; x++) {
            Console.WriteLine(x);
            Byte[] b = new GCBeep[100];
        }
    }
}
```

> 注意：虽然 `GCBeep` 类很有用，但我提供了一个更有用的 `GCNotification` 类，它允许你对应用程序进行插桩，从而提供了一种进一步了解应用程序内存使用情况的方法。你将在本章“代（Generations）”章节最后找到这个类。

此外请注意，即使类型的实例构造函数抛出异常，该类型的 `Finalize` 方法也会被调用。你的 `Finalize` 方法不应假设对象处于良好、一致的状态。以下代码演示了这一点：

```csharp
internal sealed class TempFile {
    private String _m_filename = null;
    private FileStream _m_fs;
```

```csharp
    public TempFile(String filename) {
        // 下面一行可能会抛出异常。
        m_fs = new FileStream(filename, FileMode.Create);
```

```csharp
        // 保存此文件的文件名。
        m_filename = filename;
    }
```

```csharp
    ~TempFile() {
        // 这是 Finalize 方法
        // 在这里正确的做法是测试 filename 是否为空，
        // 因为你无法确定 filename 是否在构造函数中已初始化。
        if (m_filename != null) File.Delete(m_filename);
    }
}
```

你可以改写以下代码：
