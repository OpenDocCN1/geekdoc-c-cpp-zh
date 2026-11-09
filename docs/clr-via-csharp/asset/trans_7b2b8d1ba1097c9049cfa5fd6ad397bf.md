
对于 ASP.NET 应用程序，客户端请求到达时，会构造大量新对象，这些对象代表客户端执行工作，然后将结果发送回客户端。此时，所有用于满足客户端请求的对象都成为垃圾。换句话说，每个 ASP.NET 应用程序请求都会导致创建大量垃圾。由于这些对象在创建后几乎立即变得不可达，因此每次垃圾回收都会回收大量内存。这使进程的工作集保持得非常低，并且垃圾回收器的性能非常出色。

事实上，应用程序的大多数根都位于线程栈上的参数或局部变量中。如果线程的栈很短，垃圾回收器检查根并标记可达对象所需的时间就很少。换句话说，如果避免深度嵌套的栈，垃圾回收会快得多。避免深栈的一种方法是避免使用递归方法。

另一方面，如果垃圾回收器回收第 0 代并发现有很多存活对象，则说明垃圾回收中回收的内存不多。在这种情况下，垃圾回收器会将第 0 代的预算增大到可能 512 KB。现在，发生的回收次数会减少，但当回收发生时，应回收更多内存。顺便提一下，如果一次回收后回收的内存不足，垃圾回收器会在抛出 **OutOfMemoryException** 之前执行一次完整回收。

在整个讨论中，我一直在讲垃圾回收器如何在每次回收后动态修改第 0 代的预算。但垃圾回收器也会使用类似的启发式方法修改第 1 代和第 2 代的预算。当这些代被垃圾回收时，垃圾回收器会再次查看回收了多少内存以及有多少对象存活。根据垃圾回收器的发现，它也可能增大或缩小这些代的阈值，以提高应用程序的整体性能。最终结果是，垃圾回收器会根据应用程序所需的内存负载自动进行微调——这非常酷！

下面所示的 **GCNotification** 类类似于本章前面“对托管资源使用终结化”一节中讨论的 **GCBeep** 程序。不过，**GCNotification** 类会在发生第 0 代或第 2 代回收时引发事件。利用这些事件，你可以让计算机在每次回收时发出蜂鸣声，或者计算两次回收之间经过了多少时间、两次回收之间分配了多少内存等等。借助这个类，你可以轻松地对应用程序进行检测，从而更好地了解应用程序如何使用内存。

```csharp
public static class GCNotification {
    private static Action<Int32> s_gcDone = null;  // The event's field

    public static event Action<Int32> GCDone {
        add {
            // If there were no registered delegates before, start reporting notifications now
            if (s_gcDone == null) { new GenObject(0); new GenObject(2); }
            s_gcDone += value;
        }
        remove { s_gcDone -= value; }
    }

    private sealed class GenObject {
        private Int32 m_generation;
        public GenObject(Int32 generation) { m_generation = generation; }
        ~GenObject() { // This is the Finalize method
            // If this object is in the generation we want (or higher),
            // notify the delegates that a GC just completed
            if (GC.GetGeneration(this) >= m_generation) {
                Action<Int32> temp = Interlocked.CompareExchange(ref s_gcDone, null, null);
                if (temp != null) temp(m_generation);
            }

            // Keep reporting notifications if there is at least one delegate registered,
            // the AppDomain isn't unloading, and the process isn't shutting down
            if ((s_gcDone != null)
                && !AppDomain.CurrentDomain.IsFinalizingForUnload()
                && !Environment.HasShutdownStarted) {
                // For Gen 0, create a new object; for Gen 2, resurrect the object & let
                // the GC call Finalize again the next time Gen 2 is GC'd
                if (m_generation == 0) new GenObject(0);
                else GC.ReRegisterForFinalize(this);
            } else { /* Let the objects go away */ }
        }
    }
}
```

## 用于本机资源的其他垃圾回收功能

有时，本机资源会占用大量内存，但包装该资源的托管对象占用的内存很少。最典型的例子是位图。位图可能占用数兆字节的本机内存，但托管对象很小，因为它只包含一个 HBITMAP（4 字节或 8 字节的值）。从 CLR 的角度来看，进程可以在执行回收之前分配数百个位图（使用很少的托管内存）。但是，如果进程正在操作许多位图，进程的内存消耗将以惊人的速度增长。为了解决这种情况，GC 类提供了以下两个静态方法：

```csharp
public static void AddMemoryPressure(Int64 bytesAllocated);
public static void RemoveMemoryPressure(Int64 bytesAllocated);
```

包装可能很大的本机资源的类应使用这些方法向垃圾回收器提示实际消耗了多少内存。在内部，垃圾回收器会监视这种压力，当压力变高时，会强制进行垃圾回收。

有些本机资源的数量是固定的。例如，Windows 以前有限制，只能创建五个设备上下文。对应用程序可以打开的文件数量也曾有限制。同样，从 CLR 的角度来看，进程可以在执行回收之前分配数百个对象（这些对象使用很少的内存）。但是，如果这些本机资源的数量有限，尝试使用超过可用数量的资源通常会导致抛出异常。为了解决这种情况，**System.Runtime.InteropServices** 命名空间提供了 **HandleCollector** 类：

```csharp
public sealed class HandleCollector {
    public HandleCollector(String name, Int32 initialThreshold);
    public HandleCollector(String name, Int32 initialThreshold, Int32 maximumThreshold);
    public void Add();
    public void Remove();

    public Int32 Count { get; }
    public Int32 InitialThreshold { get; }
    public Int32 MaximumThreshold { get; }
    public String Name { get; }
}
```

包装可用数量有限的本机资源的类应使用此类的实例，向垃圾回收器提示实际消耗了多少个该资源的实例。在内部，此类对象会监视计数，当计数变高时，会强制进行垃圾回收。

**注意** 在内部，**GC.AddMemoryPressure** 和 **HandleCollector.Add** 方法会调用 **GC.Collect**，强制垃圾回收在第 0 代达到其预算之前开始。通常，强烈不建议强制启动垃圾回收，因为它通常会对应用程序的性能产生不利影响。但是，调用这些方法的类这样做是为了让有限的本机资源可供应用程序使用。如果本机资源耗尽，应用程序将失败。对于大多数应用程序来说，性能降低总比完全无法运行要好。

以下代码演示了内存压力方法和 **HandleCollector** 类的使用及其效果：

```csharp
using System;
using System.Runtime.InteropServices;

public static class Program {
    public static void Main() {
        MemoryPressureDemo();                 // 0   causes infrequent GCs
        MemoryPressureDemo(10 * 1024 * 1024); // 10MB causes frequent GCs

        HandleCollectorDemo();
    }

    private static void MemoryPressureDemo(Int32 size) {
        Console.WriteLine();
        Console.WriteLine("MemoryPressureDemo, size={0}", size);
        // Create a bunch of objects specifying their logical size
        for (Int32 count = 0; count < 15; count++) {
            new BigNativeResource(size);
        }

        // For demo purposes, force everything to be cleaned-up
        GC.Collect();
    }
}
```
