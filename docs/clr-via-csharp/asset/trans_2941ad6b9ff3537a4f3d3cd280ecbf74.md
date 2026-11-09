
**表 21-1** GCCollectionMode 枚举类型定义的符号

| 符号名称 | 描述 |
|---|---|
| **Default** | 与不传标志调用 `GC.Collect` 相同。目前，这与传递 `Forced` 相同，但在 CLR 的未来版本中可能会改变。 |
| **Forced** | 强制立即对直到并包括指定代在内的所有代执行回收。 |
| **Optimized** | 垃圾回收器仅在回收有成效时（即释放大量内存或减少碎片）才执行回收。如果垃圾回收不会产生成效，则该调用没有任何效果。 |

在大多数情况下，应避免调用任何 **Collect** 方法；最好让垃圾回收器自行运行，并根据实际应用程序行为微调其代预算。然而，如果你编写的是控制台用户界面 (CUI) 或图形用户界面 (GUI) 应用程序，那么应用程序代码拥有该进程以及该进程中的 CLR。对于这些应用程序类型，你*可能希望*在某些时刻使用 **Optimized** 的 **GCCollectionMode** 来建议执行垃圾回收。通常，**Default** 和 **Forced** 模式用于调试和测试。

例如，如果刚刚发生了某个非周期性事件，而该事件很可能导致大量旧对象死亡，那么你可以考虑调用 **Collect** 方法。在这种情况下调用 **Collect** 可能并不算太糟，原因是垃圾回收器基于过去对未来的预测对于非周期性事件不太可能准确。

例如，应用程序在初始化之后或用户保存数据文件之后，强制对所有代执行一次完整垃圾回收可能是合理的。当 Windows Form 控件承载在网页上时，每次卸载页面都会执行一次完整回收。不要显式调用 **Collect** 来试图改善应用程序的响应时间；调用它是为了减少进程的工作集。

**GC** 类型还提供了一个 **WaitForPendingFinalizers** 方法。此方法只是挂起调用线程，直到处理 freachable 队列的线程清空该队列，并调用每个对象的 **Finalize** 方法。在大多数应用程序中，你不太可能需要调用此方法。不过，我偶尔见过这样的代码：

```csharp
GC.Collect();
GC.WaitForPendingFinalizers();
GC.Collect();
```

这段代码强制进行垃圾回收。回收完成后，不需要终结的对象的内存会被回收。但确实需要终结的对象，其内存还不能被回收。第一次调用 **Collect** 返回后，专门的终结线程正在异步调用 **Finalize** 方法。对 **WaitForPendingFinalizers** 的调用会让应用程序的线程休眠，直到所有 **Finalize** 方法都被调用。当 **WaitForPendingFinalizers** 返回时，所有已终结的对象现在才真正成为垃圾。此时，第二次调用 Collect 会强制进行另一次垃圾回收，从而回收这些现已终结的对象所占用的全部内存。

对于某些应用程序（尤其是倾向于在内存中保留大量对象的服务器应用程序），垃圾回收器执行包含第 2 代的完整回收所需的时间可能过长。事实上，如果回收需要很长时间才能完成，那么客户端请求可能会超时。为了帮助这类应用程序，GC 类提供了一个 RegisterForFullGCNotification 方法。使用此方法以及一些额外的辅助方法（WaitForFullGCApproach、WaitForFullGCComplete 和 CancelFullGCNotification），应用程序现在可以在垃圾回收器即将执行完整回收时收到通知。然后，应用程序可以调用 GC.Collect 以在更合适的时机强制回收，或者应用程序可以与另一台服务器通信，以便更好地对客户端请求进行负载均衡。有关更多信息，请查阅 .NET Framework SDK 文档中的这些方法。注意，你应始终成对调用 WaitForFullGCApproach 和 WaitForFullGCComplete 方法，因为 CLR 在内部将它们作为成对方法处理。

最后，GC 类提供了两个静态方法，让你可以确定对象当前所在的代：

```csharp
Int32 GetGeneration(Object obj)
Int32 GetGeneration(WeakReference wr)
```

GetGeneration 的第一个版本接受对象引用作为参数，第二个版本接受 WeakReference 引用作为参数。返回的值将介于 0 和 GC.MaxGeneration 之间（含这两者）。

下面的代码将帮助你理解代的工作原理。该代码还演示了刚刚讨论的 GC 方法的用法。

```csharp
using System;

internal sealed class GenObj {
    ~GenObj() {
        Console.WriteLine("In Finalize method");
    }
}

public static class Program {
    public static void Main() {
        Console.WriteLine("Maximum generations: " + GC.MaxGeneration);

        // Create a new GenObj in the heap.
        Object o = new GenObj();

        // Because this object is newly created, it is in generation 0.
        Console.WriteLine("Gen " + GC.GetGeneration(o)); // 0

        // Performing a garbage collection promotes the object's generation.
        GC.Collect();
        Console.WriteLine("Gen " + GC.GetGeneration(o)); // 1

        GC.Collect();
        Console.WriteLine("Gen " + GC.GetGeneration(o)); // 2

        GC.Collect();
        Console.WriteLine("Gen " + GC.GetGeneration(o)); // 2 (max)

        o = null; // Destroy the strong reference to this object.

        Console.WriteLine("Collecting Gen 0");
        GC.Collect(0);                  // Collect generation 0.
        GC.WaitForPendingFinalizers();  // Finalize is NOT called.

        Console.WriteLine("Collecting Gens 0, and 1");
        GC.Collect(1);                  // Collect generations 0 & 1.
        GC.WaitForPendingFinalizers();  // Finalize is NOT called.

        Console.WriteLine("Collecting Gens 0, 1, and 2");
        GC.Collect(2);                  // Same as Collect()
        GC.WaitForPendingFinalizers();  // Finalize IS called.
    }
}
```

生成并运行此代码会得到以下输出：

```
Maximum generations: 2
Gen 0
Gen 1
Gen 2
Gen 2
Collecting Gen 0
Collecting Gens 0, and 1
Collecting Gens 0, 1, and 2
In Finalize method
```

### 线程劫持

在本章前面，我解释了垃圾回收算法。然而，在那次讨论中我做了一个很大的假设：只有一个线程在运行。在现实世界中，很可能有多个线程访问托管堆，或者至少操作在托管堆内分配的对象。当一个线程触发垃圾回收时，其他线程不得访问任何对象（包括其自身堆栈上的对象引用），因为垃圾回收器很可能会移动这些对象，从而改变它们的内存位置。

因此，当垃圾回收器想要开始垃圾回收时，所有正在执行托管代码的线程都必须被挂起。CLR 使用几种不同的机制来安全地挂起线程，以便执行垃圾回收。之所以有多种机制，是为了让线程尽可能长时间地运行，并尽可能减少开销。我不想在这里深入所有细节，但可以说，Microsoft 已经做了大量工作来减少垃圾回收涉及的开销。Microsoft 将继续随着时间的推移修改这些机制，以确保未来实现高效的垃圾回收。

当 CLR 想要开始垃圾回收时，它会立即挂起所有正在执行托管代码的线程。然后，CLR 检查每个线程的指令指针，以确定该线程正在何处执行。接着，将指令指针地址与 JIT 编译器生成的表进行比较，以确定该线程正在执行什么代码。

如果线程的指令指针位于某个表所标识的偏移处，则称该线程已到达 *安全点*。*安全点* 是指可以安全地让线程保持挂起状态直到垃圾回收完成的位置。如果线程的指令指针不在内部方法表所标识的偏移处，则该线程不在安全点，CLR 无法执行垃圾回收。在这种情况下，CLR *劫持* 该线程：CLR 修改线程的堆栈，使返回地址指向 CLR 内部实现的一个特殊函数。然后恢复该线程。当当前执行的方法返回时，该特殊函数将执行，从而挂起该线程。

然而，该线程可能在相当长一段时间内都不会从其方法返回。因此，在线程恢复执行后，CLR 会等待大约 250 毫秒，让该线程 *被劫持*。在此时间之后，CLR 再次挂起该线程并检查其指令指针。如果该线程已到达安全点，则垃圾回收可以开始。如果该线程仍未到达安全点，CLR 会检查是否调用了另一个方法；如果调用了，CLR 会再次修改堆栈，以便该线程从最近执行的方法返回时 *被劫持*。然后，CLR 恢复该线程，并再等待几毫秒后重试。

当所有线程都已到达安全点或已 *被劫持* 时，垃圾回收就可以开始。垃圾回收完成后，所有线程都会恢复，应用程序继续运行。*被劫持* 的线程会返回到最初调用它们的方法。

这个算法有一个小转折。当 CLR 想要开始垃圾回收时，它会挂起所有正在执行托管代码的线程，但不会挂起正在执行非托管代码的线程。一旦所有正在执行托管代码的线程都到达安全点或 *被劫持*，就允许开始垃圾回收。正在执行非托管代码的线程可以继续运行，因为它们正在使用的任何对象都应已被固定。如果当前正在执行非托管代码的线程返回到托管代码，该线程会立即被挂起，直到垃圾回收完成。

事实证明，CLR 大多数时候使用 *劫持*，而不是使用 JIT 编译器生成的表来确定线程是否处于安全点。原因是 JIT 编译器——
