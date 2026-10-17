
```csharp
using System;
using System.InteropServices;

public static class Program {
    public static void Main() {
        // 0 导致频繁 GC
        MemoryPressureDemo(0); // 10MB 导致频繁 GC
        MemoryPressureDemo(10 * 1024 * 1024);

        HandleCollectorDemo();

        // 为了演示目的，强制清理
        GC.Collect();
    }

    private static void MemoryPressureDemo(long size) {
        Console.WriteLine();
        Console.WriteLine("MemoryPressureDemo, size={0}", size);
        // 创建一组指定大小的对象
        for (Int32 count = 0; count < 15; count++) {
            new BigNativeResource(size);
        }
    }

    private static void HandleCollectorDemo() {
        Console.WriteLine();
        Console.WriteLine("HandleCollectorDemo");
        for (Int32 count = 0; count < 10; count++) new LimitedResource();
    }
}

private sealed class BigNativeResource {
    private readonly Int32 m_size;

    public BigNativeResource(long size) {
        m_size = size;
        // 让 GC 认为该对象在物理上更大
        if (m_size > 0) GC.AddMemoryPressure(m_size);
        Console.WriteLine("BigNativeResource create.");
    }

    ~BigNativeResource() {
        // 让 GC 对象释放内存
        if (m_size > 0) GC.RemoveMemoryPressure(m_size);
        Console.WriteLine("BigNativeResource destroy.");
    }
}

private sealed class LimitedResource {
    // 创建一个 HandleCollector，告诉它存在两个或多个此类对象时应进行收集
    private static readonly HandleCollector s_hc = new HandleCollector("LimitedResource", 2);

    public LimitedResource() {
        // 通知 HandleCollector 一个 LimitedResource 已添加到堆中
        s_hc.Add(this);
        Console.WriteLine("LimitedResource create. Count={0}", s_hc.Count());
    }

    ~LimitedResource() {
        // 通知 HandleCollector 一个 LimitedResource 已从堆中移除
        s_hc.Remove(this);
        Console.WriteLine("LimitedResource destroy. Count={0}", s_hc.Count());
    }
}
```

如果你编译并运行前面的代码，输出将与下面的输出相似。

```
MemoryPressureDemo, size=0
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.

MemoryPressureDemo, size=10485760
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource destroy.
```

```
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
```

```
HandleCollectorDemo
LimitedResource create. Count=1
LimitedResource create. Count=2
LimitedResource create. Count=3
LimitedResource destroy. Count=3
LimitedResource destroy. Count=2
LimitedResource destroy. Count=1
LimitedResource create. Count=2
LimitedResource create. Count=3
LimitedResource destroy. Count=2
LimitedResource create. Count=3
LimitedResource destroy. Count=3
LimitedResource destroy. Count=2
LimitedResource destroy. Count=1
LimitedResource create. Count=1
LimitedResource create. Count=2
LimitedResource create. Count=3
LimitedResource destroy. Count=2
LimitedResource destroy. Count=1
```

# 终化内部机制

从表面上看，终化（finalization）似乎非常简单：你创建一个对象，当它被回收时，其 `Finalize` 方法会被调用。但深入研究后发现，终化比这要复杂得多。

当应用程序创建一个新对象时，在调用类型的 `Finalize` 实例构造函数之前，对象的指针会被放置在*终化列表*（finalization list）中。终化列表是由垃圾回收器控制的内部数据结构。列表中的每个项都指向一个对象，在回收该对象的内存之前，必须调用其 `Finalize` 方法。

图 21-13 显示了一个包含若干对象的堆。其中一些对象可以从应用程序根到达，而另一些则不能。当创建对象 C、E、F、I 和 J 时，系统检测到这些对象的类型都定义了 `Finalize` 方法，因此将这些对象的引用添加到终化列表中。

![](img/0ce3b788d061e3d3095fa554b1a34adf_568_0.png)

图 21-13 显示其终化列表中包含指针的托管堆。

> 注意：尽管 `System.Object` 定义了 `Finalize` 方法，但 CLR 知道要忽略它；在构造类型实例时，如果该类型的 `Finalize` 方法是继承自 `System.Object` 的，则该对象不被视为可终化的。必须由派生类型之一重写 `Object` 的 `Finalize` 方法。

当发生垃圾回收时，对象 B、E、G、H、I 和 J 被确定为垃圾。垃圾回收器扫描终化列表以寻找这些对象的引用。一旦找到引用，该引用将从终化列表中移除，并附加到可到达队列（freachable queue）中。可到达队列（读作 "F-reachable"）是垃圾回收器的另一个内部数据结构。可到达队列中的每个引用都标识一个准备好调用 `Finalize` 方法的对象。回收后，托管堆看起来如图 21-14 所示。

![](img/0ce3b788d061e3d3095fa554b1a34adf_568_1.png)

图 21-14 显示指针从终化列表移动到可到达队列的托管堆。

在此图中，你看到对象 B、G 和 H 占据的内存已被回收——因为这些对象没有 `Finalize` 方法。然而，对象 E、I 和 J 占据的内存无法被回收，因为它们的 `Finalize` 方法尚未被调用。

有一个特殊的优先级 CLR 线程专门用于调用 `Finalize` 方法。使用专用线程是为了避免如果使用应用程序的普通优先级线程可能会出现的线程同步问题。当可终化队列为空时（通常情况），该线程会睡眠。当出现项时，该线程会被唤醒，从队列中移除每个项并调用每个对象的 `Finalize` 方法。由于该线程的工作方式，你不应该在 `Finalize` 方法中执行任何对执行代码的线程做任何假设的代码。例如，在 `Finalize` 方法中访问线程本地存储。

未来，CLR 可能会使用多个线程。你应该避免编写任何假设 `Finalize` 方法将按顺序调用的代码。仅使用一个终化线程，在多个 CPU 终化对象但只有一个线程执行 `Finalize` 方法的情况下，可能会出现性能和可扩展性问题——该线程可能无法跟上分配的速度。

终化列表与可终化队列之间的交互非常迷人。首先，我告诉你可终化队列是如何命名的。“F”是显而易见的，代表*终化*（finalization）；可终化队列中的每个项都是指向托管堆中已调用 `Finalize` 方法的对象的引用。但名称中的*可到达*（reachable）部分意味着对象是可到达的。换句话说，可终化队列被视为根，就像静态字段是根一样。因此，可终化队列中的引用保持对象可到达且不是垃圾。

简而言之，当对象不可到达时，垃圾回收器将其收集为垃圾。当垃圾回收器将对象的引用从终化列表移动到可终化队列时，该对象不再被视为垃圾，其内存无法被回收。实际上，回收将是必要的，因为对象会被提升到另一个代。图 21-15 显示了第二次回收后托管堆的状态。

| 根：字段与变量 | | | |

|---|---|---|---|

| A | C | D | F |

| C | F | | |

终化列表

可到达队列

图 21-15 第二次回收后的对象状态。

```cs
// 如果索引不为 0，则实例属性返回 true
public Boolean IsAllocated { get; }
```

```cs
// 对于固定条目，此返回对象的地址
public IntPtr AddrOfPinnedObject();
```

```cs
public override Int32 GetHashCode();
public override Boolean Equals(object o);
```

基本上，要控制或监控对象的生命周期，你需要使用 `GCHHandle` 的静态方法 `Alloc`，传递你想要监控/控制的对象的引用，以及 `GHandleType`（该类型是一个标志位，指示你想要如何监控/控制该对象）。`GHandleType` 是定义如下的枚举类型。

```cs
public enum GHandleType {
    Weak = 0, // 用于监控对象是否存在
    WeakTrackResurrection = 1, // 用于监控对象是否存在
    Normal = 2, // 用于控制对象的生命周期
    Pinned = 3 // 用于控制对象的生命周期
}
```

现在，以下是每个标志的含义：

- **Weak** 此标志允许你监控对象的生命周期。具体而言，你可以检测垃圾回收器何时确定该对象从应用程序代码中无法访问。注意，对象的 `Finalize` 方法可能已经执行也可能尚未执行，因此对象可能仍在内存中。

- **WeakTrackResurrection** 此标志允许你监控对象的生命周期。具体而言，你可以检测垃圾回收器何时确定该对象从应用程序代码中无法访问。注意，对象的 `Finalize` 方法（如果存在）肯定已经执行，且对象的内存已被回收。

- **Normal** 此标志允许你控制对象的生命周期。具体而言，你是在告诉垃圾回收器，即使应用程序中可能没有引用该对象的根，该对象也必须留在内存中。当运行垃圾回收时，该对象的内存可以被压缩（移动）。不接受 `GHandleType` 标志的 `Alloc` 方法会分配指定的 `GHandleType.Normal`。

- **Pinned** 此标志允许你控制对象的生命周期。具体而言，你是在告诉垃圾回收器，即使应用程序中可能没有引用该对象的根，该对象也必须留在内存中。当运行垃圾回收时，该对象的内存不能被压缩。这通常在你想要将内存句柄传递给原生代码时有用。原生代码可以写入托管堆中的这块内存，同时确保 GC 不移动该对象。

当你调用 `GCHHandle` 的静态 `Alloc` 方法时，它会扫描 `AppDomain` 的 GC 句柄表，查找存储传递给 `Alloc` 的对象的可用引用，并将标志设置为你传递给 `GHandleType` 参数的值。然后，`Alloc` 返回一个 `GCHandle` 实例。`GCHandle` 是一个轻量级类型，包含一个实例字段（`IntPtr`），它指向表中的条目索引。当你想要释放 GC 句柄表中的此条目时，获取 `GCHandle` 实例并调用 `Free` 方法（这将通过将其 `IntPtr` 字段置零来使 `GCHandle` 实例失效）。

以下是垃圾回收器使用 GC 句柄表的方式。当发生垃圾回收时：

- 垃圾回收器扫描 GC 句柄表查找所有的 `Weak` 条目。如果是指向未标记对象的 `Weak` 条目，该引用将识别出一个不可访问的对象（垃圾），且该条目的引用值将被更改为 null。

- 垃圾回收器扫描终结列表。如果列表中的引用指向一个未标记的对象，该引用将识别出一个不可访问的对象，且该引用将从终结列表移动到可存队列（freachable queue）。此时，对象会被标记，因为该对象现在被认为是可访问的。

- 垃圾回收器扫描 GC 句柄表查找所有的 `WeakTrackResurrection` 条目。如果 `WeakTrackResurrection` 条目指向一个未标记的对象（该对象现在被可存队列中的条目引用），该引用将识别出一个不可访问的对象（垃圾），且该条目的引用值将被更改为 null。

- 垃圾回收器压缩内存，挤出不可访问对象留下的空隙。固定（Pinned）对象不会被压缩（移动）；垃圾回收将在它们周围移动其他对象。

现在你已经了解了该机制，让我们来看何时使用它。最容易理解的标志是 `Normal` 和 `Pinned` 标志，所以让我们从这两个标志开始。这两个标志通常在与原生代码操作时使用。

`Normal` 标志用于当你需要向原生代码提供指向托管对象的指针，因为在未来的某个时刻，原生代码将调回托管代码并传递该指针。如果发生了垃圾回收，对象可能会移动，导致指针失效。因此，在此你会将返回的 `GCHandle` 实例转换为 `IntPtr` 并将 `IntPtr` 传递给原生代码。当原生代码调回托管代码时，托管代码可以将传递的 `IntPtr` 回 `GCHandle`，然后查询 `Target` 属性以获取托管对象的引用（或当前地址）。当原生代码不再需要该引用时，你会调用 `GCHandle` 的 `Free` 方法，这将允许下一次垃圾回收释放该对象（假设没有其他根引用它）。
