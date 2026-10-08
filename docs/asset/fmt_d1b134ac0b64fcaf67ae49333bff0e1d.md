
`System.GC` 类型允许应用程序对垃圾回收器进行一些直接控制。首先，你可以通过读取 `GC.MaxGeneration` 属性来查询托管堆支持的最大代数；该属性始终返回 2。

你还可以通过调用以下两个静态方法之一来强制垃圾回收器执行集合：

- `void GC.Collect(Int32 Generation)`
- `void GC.Collect()`
- `void GC.Collect(Int32 generation, GCCollectionMode mode)`

第一个方法允许你指定要回收的某代（或几代）。你可以传递任何从 0 到 `GC.MaxGeneration`（包含边界）的整数。传递 0 会导致回收第 0 代，传递 1 会回收第 1 代和第 0 代，传递 2 则会回收第 2 代、第 1 代和第 0 代。不带参数的 `Collect` 方法版本会强制对所有代进行全量回收，等同于调用：

```
GC.Collect(GC.MaxGeneration);
```

`Collect` 的第三种重载允许你传递一个代数和一个 `GCCollectionMode`。表 21-1 描述了各种 GC 集合模式符号。

```csharp
public static class Program {
    public static void Main() {
        try {
            // 逻辑上预留 1.5 GB 内存
            using (MemoryFailPoint mfp = new MemoryFailPoint(1500)) {
                // 在此处执行内存密集型算法
            }
        } // Dispose 将逻辑上释放 1.5 GB 内存
    } catch (InsufficientMemory e) {
        // 无法预留内存
        Console.WriteLine(e);
    }
}
```

# 第 21 章 自动内存管理（垃圾回收）

表 21-1 由 `GCCollectionMode` 类型定义的符号

| 符号名称 | 描述 |
| :--- | :--- |
| Default | 与不带标志调用 `GC.Collect` 相同。现在与传递 `Forced` 相同，但在 CLR 的未来版本中可能会发生。 |
| Forced | 强制对包括指定代数在内的所有代立即执行集合。 |
| Optimized | 只有当集合能够产生成效（即释放大量内存或减少碎片）时，垃圾回收器才会执行集合。如果垃圾回收不会产生成效，则该调用将不起作用。 |

在大多数情况下，你应该避免调用任何 `Collect` 方法；最好的办法让垃圾回收器自行运行，并根据实际应用程序行为微调其代数预算。然而，如果你正在编写控制台用户界面（CUI）或图形用户界面（GUI）应用程序，你的应用程序代码拥有该进程以及其中的 CLR。对于这些类型的应用程序，你可能希望使用 `Optimized` `GCCollectionMode` 在某些时刻建议进行垃圾回收。`Default` 和 `Forced` 正常模式用于调试和测试。

例如，如果某个非周期性事件刚刚导致旧对象可能死亡，你可以考虑调用 `Collect` 方法。在这种情况下调用 `Collect` 可能不理想的原因是，收集器基于过去对未来的预测对于非周期性事件可能并不准确。

例如，在应用程序初始化之后或用户保存数据文件之后，让应用程序强制对所有代进行垃圾回收可能是有意义。当 Windows Form 控件托管在 Web 页面上时，每次加载页面都会执行一次全量回收。不要通过显式调用 `Collect` 来尝试提高应用程序的响应时间；调用它是为了减少你进程的工作工作集。

`GC` 类型还有一个 `WaitForPendingFinalizers` 方法。该方法简单地挂起调用线程，直到处理终结队列的线程清空队列并调用每个对象的 `Finalize` 方法。在大多数应用程序中，你不太可能调用此方法。尽管如此，你可能会看到这样的代码：

```
GC.Collect();
GC.WaitForPendingFinalizers();
GC.Collect();
```

这段代码强制执行垃圾回收。当集合完成后，不需要终化的对象的内存将被回收。而需要终化的对象目前还无法回收其内存。在第一次调用 `Collect` 返回后，特殊的专用终结线程会异步地调用 `Finalize` 方法。调用 `WaitForPendingFinalizers` 会让应用程序线程睡眠，直到所有 `Finalize` 方法都被调用完毕。当 `WaitForPendingFinalizers` 返回时，所有已终化的对象现在都是真正的垃圾了。

# 第四部分 核心设施

此时，第二次调用 `Collect` 强制执行另一次垃圾回收，回收所有已被终结对象所占用的内存。

对于某些应用程序（特别是于在内存中保留大量对象的服务器应用程序），垃圾回收器执行包含第 2 代在内的全回收所需的时间可能过长。事实上，如果一次集合需要长时间才能完成，客户端就会请求帮助。为了帮助这类应用程序，`GC` 类提供了 `RegisterForFullGCApproach`、`WaitForFullGCComplete` 和 `CancelForFullGCNotification`，应用程序现在可以在垃圾回收器即将执行全量回收时收到通知。然后应用程序可以调用 `GC.Collect` 在更合适的时刻强制执行回收，或者应用程序可以与另一个服务器通信以更好地加载客户端请求。有关更多信息，请查阅 .NET Framework SDK 文档中的这些方法。请注意，你应该始终成对调用 `WaitForFullGCApproach` 和 `WaitForFullGCComplete` 方法，因为 CLR 将它们作为成对处理。

最后，`GC` 类提供了两个静态方法，允许你确定对象当前处于哪一代：

```
Int32 GetGeneration(Object obj)
Int32 GetGeneration(WeakReference wr)
```

第一个版本的 `GetGeneration` 接收对象引用作为参数，第二个版本接收 `WeakReference` 引用作为参数。返回值将在 0 到 `GC.MaxGeneration` 之间。

以下代码将帮助你理解代数的工作原理。它还展示了刚刚讨论的 GC 方法。

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

        // 在堆中创建一个新的 GenObj
        Object o = new GenObj();

        // 因为这个对象是新创建的，它在第 0 代
        Console.WriteLine("Gen " + GC.GetGeneration(o)); // 0
    }
}
```

# 第 21 章 自动内存管理（垃圾回收）

```csharp
// 执行回收提升了对象的代数。
GC.Collect();
Console.WriteLine("Gen " + GC.GetGeneration(o)); // 1
GC.Collect();
Console.WriteLine("Gen " + GC.GetGeneration(o)); // 2
GC.Collect();
Console.WriteLine("Gen " + GC.GetGeneration(o)); // 2 (max)

o = null; // 销毁对该对象的强引用

Console.WriteLine("Collecting Gen 0");
GC.Collect(0); // 回收第 0 代
GC.WaitForPendingFinalizers(); // 没有调用终化

Console.WriteLine("Collecting Gen 0, and 1");
GC.Collect(1); // 回收第 0 和 1 代
GC.WaitForPendingFinalizers(); // 没有调用终化

Console.WriteLine("Collecting Gen 0, 1, and 2");
GC.Collect(2); // 等于 Collect()
GC.WaitForPendingFinalizers(); // 调用了终化
```

构建并运行此代码将产生以下输出：

- Maximum generations: 2
- Gen 0
- Gen 1
- Gen 2
- Gen 2
- Collecting Gen 0
- Collecting Gens 0, and 1
- Collecting Gens 0, 1, and 2
- In Finalize method

## 线程劫持

在本章之前的章节中，我解释了垃圾回收算法。然而，在那个讨论期间，我做了一个巨大的假设：只有一个线程在运行。在现实世界中，可能有多个线程访问托管堆，或者至少操作托管堆中的对象。当一个线程触发垃圾回收时，其他线程不得访问任何对象（包括其堆栈上的对象引用），因为垃圾回收器可能会移动这些对象，改变它们的内存位置。当垃圾回收器想要开始垃圾回收时，所有执行托管代码的线程都必须挂起。CLR 使用几种不同的机制来安全地挂起线程，以便执行垃圾回收。原因是

# 第四部分 核心设施

有多种机制可以保持线程尽可能长时间运行，并尽可能地减少开销。我在这里不想涉及所有的细节，但足以说明，微软已经做了大量工作来减少垃圾回收相关的开销。微软将随着时间推改进这些机制，以确保未来高效的垃圾回收。

当 CLR 想要启动垃圾回收时，它会立即挂起所有执行托管代码的线程。然后，CLR 会检查每个线程的指令指针（instruction pointer），以确定线程当前执行的位置。随后，将指令指针地址与 JIT 编译器生成的表进行比较，以确定正在执行什么代码。

如果线程的指令指针位于表中识别的偏移量处，则认为该线程已到达安全点（safe point）。安全点是一个可以允许线程挂起直到垃圾回收完成的地方。如果线程的指令指针没有位于内部方法表识别的偏移量处，则该线程不在安全点，CLR 无法直接执行垃圾回收。在这种情况下，CLR 会*劫持*（hijacks）线程：CLR 修改线程的栈，使返回地址指向 CLR 内部实现的一个特殊函数。然后恢复线程。当当前执行的方法返回时，该特殊函数将执行，从而挂起线程。

然而，线程可能一段时间内都不会从其方法返回。因此，在线程恢复执行后，CLR 会等待大约 250 毫秒让线程被劫持。在此时间之后，CLR 再次挂起线程并检查其指令指针。如果线程已到达安全点，则可以垃圾回收。如果线程仍未到达安全点，CLR 会检查是否调用了其他方法；如果是，CLR 将修改栈，以便在线程从最正在执行的方法返回时被劫持。然后 CLR 恢复线程并再次等待几毫秒后再次尝试。

当所有线程都到达安全点或被劫持后，垃圾回收就可以开始。当垃圾回收完成后，所有线程都会恢复，应用程序继续运行。被劫持的线程将返回到最初调用它们的方法。

该算法有一个小转折。当 CLR 想要启动垃圾回收时，它会挂起所有执行托管代码的线程，但不会挂起执行非托管代码的线程。一旦所有执行托管代码的线程都处于安全点或被劫持，就可以开始垃圾回收。执行非托管代码的线程被允许继续运行，它们正在使用的任何对象都将被固定（pinned）。如果当前执行非托管代码的线程返回到托管代码，该线程将立即挂起，直到垃圾回收完成。

事实证明，CLR 在大多数时候使用劫持，而不是使用 JIT 编译器生成的表来判断线程是否处于安全点。其原因是 JIT 编译器生成的表需要大量内存并会增加工作集（working set），这会显著损害性能。因此，JIT 编译器生成的表仅包含没有调用其他方法的循环部分的信息。如果方法包含调用其他方法的循环，或者没有循环，JIT 编译器生成的表中就没有多少信息，此时使用劫持来挂起线程。

# 第 21 章 自动内存管理（垃圾回收） 585

# 垃圾回收模式

当 CLR 启动时，会选择一种 GC 模式，此模式在进程生命周期内无法更改。有两种基本的 GC 模式：

- *Workstation*（工作站）这种模式为客户端应用程序微调了垃圾回收器。垃圾回收器假设机器上还运行着其他应用程序，不会独占 CPU 资源。工作站模式有两个子模式：带有并发回收器的工作站和不带并发回收器的工作站模式。我很快会描述该回收器。
- *Server*（服务器）这种模式为服务器端应用程序微调了垃圾回收器。垃圾回收器假设机器上没有运行其他应用程序（客户端或服务器），并且它假设机器上的所有 CPU 都可以用于垃圾回收。这种 GC 模式会导致托管堆拆分为若干区域，每个 CPU 一个区域。当启动垃圾回收时，垃圾回收器每个 CPU 有一个线程；每个线程与其他线程并行收集它自己的区域。并行收集对于服务器应用程序效果良好，因为服务器的工作线程倾向于表现出一致的行为。此功能要求应用程序运行在具有多个 CPU 的计算机上，以便线程能够同时工作以提高性能。

默认情况下，应用程序使用 Workstation GC 运行，并开启并发模式。然而，服务器应用程序（如 ASP.NET 或 SQL Server）托管 CLR 会请求 CLR 加载 Server GC。但是，如果服务器应用程序运行在单处理器机器上，CLR 将加载不带并发回收器自身的 GC。

自托管 CLR 的应用程序可以通过创建配置文件（如在第 2 章“构建、打包、部署和管理应用程序和类型”以及第 3 章“共享程序集和强名称程序集”中讨论过的），在其中包含一个针对应用程序的 `gcServer` 元素，来告诉 CLR 使用服务器回收器。这是一个配置文件的示例：

```
<configuration>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
</configuration>
```

# 第四部分 核心设施

当应用程序运行时，它可以查询 `GCSettings` 类的 `IsServerGC` 只读布尔属性来询问 CLR 是否正在以 Server 模式运行：

```
using System;
using System.Runtime; // GCSettings 在此命名空间

public static class Program {
    public static void Main() {
        Console.WriteLine("Application is running with GC=" + GCSettings.IsServerGC);
    }
}
```

Workstation GC 可以在并发或非并发模式运行。在并发模式下，垃圾回收器有一个额外的后台线程，在应用程序运行时进行收集。当线程分配的对象导致第 0 代超过其配额时，垃圾回收器会挂起所有线程并确定要收集哪些代。如果垃圾回收器需要收集第 0 代或第 1 代，它将按正常方式进行。然而，如果需要收集第 2 代，则会增加第 0 代的配额以分配新对象，并恢复应用程序线程。

在应用程序线程运行时，垃圾回收器有一个普通优先级的后台线程，用于标记不可达对象。这会与应用程序线程竞争 CPU 时间，导致应用程序任务执行得较慢。一旦对象被标记，垃圾回收器再次挂起所有线程并决定是否压缩内存。如果垃圾回收器压缩内存，则内存将进行压缩，修复根引用，并恢复应用程序线程。这种垃圾回收比通常所需的短，因为不可达对象集已经构建完成。然而，垃圾回收器可能不会压缩内存；事实上，垃圾回收器倾向于这种方法。

总结：并发回收为用户创建了更好的交互体验，最适合交互式 UI 或 GUI 应用程序。对于某些应用程序，并发回收实际上会损害性能并消耗更多内存。在测试应用程序时，您应该尝试开启和关闭并发回收，并观察哪种方式对您的应用程序性能和内存占用最佳。

您可以通过为应用程序创建一个配置文件（如第 2 和第 3 章讨论过的），其中包含一个 `gcConcurrent` 元素来告诉 CLR 不要使用并发回收器。这是一个配置文件的示例：

```
<configuration>
  <runtime>
    <gcConcurrent enabled="false"/>
  </runtime>
</configuration>
```

```xml
<configuration>
  <runtime>
    <gcConcurrent enabled="false"/>
  </runtime>
</configuration>
```

除了描述的模式外，垃圾回收器还支持无同步分配。在多处理器系统中，托管堆的第 0 代内存被划分为多个内存区域（arenas），每个线程一个。这允许多个线程同时进行分配，因此不需要对堆进行排他访问。

虽然 GC 模式是针对进程配置的，在进程运行时无法更改，但您的应用程序可以通过 `GCSettings` 类的 `GCLatencyMode` 属性对垃圾回收进行某些控制。此读/写属性可以被设置为 `GCLatencyMode` 枚举类型中的任何一个值，如表 21-2 所示。

## 表 21-2 由 `GCLatencyMode` 枚举类型定义的符号

| 符号名称 | 描述 |
|---|---|
| Batch (Server GC 模式的默认值) | 在 Workstation GC 模式下，此延迟模式会关闭并发 GC。在 Server GC 模式下，这是唯一的有效延迟模式。 |
| Interactive (Workstation GC 模式的默认值) | 在 Workstation GC 模式下，此延迟模式会开启并发 GC。在 Server GC 模式下，此延迟模式无效。 |
| LowLatency | 在 Workstation GC 模式下，在短期的、时间敏感的操作（如绘制动画）中使用此延迟模式，这些操作可能会导致第 2 代回收被中断。在 Server GC 中，此延迟模式无效。 |
