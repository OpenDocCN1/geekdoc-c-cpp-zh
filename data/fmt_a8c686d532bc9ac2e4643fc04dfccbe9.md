
## 分页与未托管内存分配

.NET 垃圾回收会累积未托管内存。根据定义，它无法为现实应用中可能出现的每个内存管理需求提供完美的解决方案。

在之前的章节中，我们检查了许多垃圾回收器表现糟糕且必须调优以提供足够性能的场景。一个可能让应用程序陷入瘫痪的示例涉及当物理内存不足以包含所有对象时使用垃圾回收器。

考虑运行在具有 8GB 物理内存（RAM）的机器上的应用程序。只要应用程序仍然能够分配内存（在 64 位系统上），它就可以轻松地扩展到任何内存量。应用程序分配了 12GB 的内存，其中最多有 8GB 将驻留在工作集（物理内存）中，至少有 4GB 将被交换到磁盘。Windows 工作集管理器将确保应用程序频繁访问的页面对象留在物理内存中，而包含应用程序访问的对象的页面将被交换到磁盘。

在正常运行期间，应用程序可能不会表现出分页现象，因为它很少访问被换出的对象。然而，当发生全垃圾回收时，GC 必须遍历每个可达对象以在标记阶段（mark phase）构建图。遍历每个可达对象意味着要从磁盘读取 4GB 数据以访问它们。由于物理内存已满，这还意味着必须向磁盘写入 4GB 数据，以为换出的对象释放物理内存。最后，在垃圾回收完成后，访问其频繁使用的对象（这些对象可能已被交换到磁盘）会引发额外的页错误。

硬盘在写入时提供的顺序读写传输速率约为 150MB/s（即使是快速的固态驱动器，其速度也不会超过此数值的2 倍）。因此，在分页换入和换出到磁盘的同时执行 8GB 的传输可能需要大约 55 秒。在此期间，应用程序正在等待 GC 完成（除非是并发 GC）；增加更多的处理器（即使用服务器版 GC）将无于事，因为 GC 是瓶颈。系统上的其他应用程序将遭受性能大幅下降，因为物理磁盘将由于分页请求而饱和。

解决此问题的唯一方法是分配未托管内存来存储那些可能被分页交换到磁盘的对象。未托管内存不受垃圾回收的影响，并且只有在应用程序需要时才会被访问。

另一个与控制分页和工作集管理相关的示例是将页面锁定在物理内存中。Windows 应用程序有一个记录在案的接口，可以向系统请求某些特定的内存区域不被交换到磁盘（不考虑异常情况）。此机制无法与 .NET 垃圾回收器结合使用，因为托管应用程序无法直接控制 CLR 执行的虚拟内存分配。然而，自定义的 CLR 宿可以作为 CLR 虚拟内存分配请求的一部分将页面锁定到内存中。

## 静态代码分析 (FxCop) 规则

Visual Studio 的静态代码分析 (FxCop) 有一组针对与垃圾回收常见的性能和正确性问题的规则。我们建议使用这些规则，因为它们通常可以在编码阶段捕获 Bug，而这是识别和发现 Bug 的成本最低阶段。关于 Visual Studio 内或外进行托管代码分析的更多信息，请参考 MSDN 在线文档。

随 Visual Studio 11 发布的 GC 相关的规则：

- 设计规则—CA1001—拥有可释放字段的类也应该是可释放的。此规则确保了通过聚合类型对类型成员进行确定性的终结化。

- 设计规则—CA1049—拥有原生资源的类也应该是可释放的。此规则确保为提供原生资源（如 `System.Runtime.InteropServices.HandleRef`）访问的类型正确地实现了 Dispose 模式。

- 设计规则—CA1063—实现 IDisposable。此规则确保了可释放类型正确地实现了 Dispose 模式。

- 性能规则—CA1821—移除空终结器。此规则确保那些带有空终结器的类型被移除，空终结器会降低性能并影响“中年危机”问题。

- 可靠性规则—CA2000—在锁定之前释放对象。此规则确保 `IDisposable` 类型的局部变量在离开作用域之前被释放。

- 可靠性规则—CA2006—使用 SafeHandle 封装原生资源。此规则确保在可能的情况下，使用 `SafeHandle` 类或其派生类之一而不是直接句柄（如 `System.IntPtr`）指向未托管资源。

- 使用规则—CA1816—GC.SuppressFinalize。此规则确保可释放类型在它们的终结器中调用抑制终结化。

- 使用规则—CA2213—可释放字段应该被释放。此规则确保可释放类型调用抑制终结化。

- 使用规则—CA2215—Dispose 方法应该调用 dispose（此处可能指内部逻辑）。此规则确保如果实现了 `IDisposable`，则正确地实现了 Dispose 模式。

- 使用规则—CA2216—可释放类型应声明终结器。此规则确保可释放类型为该场景提供终结器作为备份。

## 总结

在本章中，我们回顾了负责自动回收内存的实体垃圾回收器的动机和实现。我们检查了追踪垃圾回收的替代方案，包括引用计数垃圾回收和手动释放管理。垃圾回收器的核心是以下协作概念，我们进行了详细研究：

- 根（Roots）是构建可达对象图的起点。

- 标记（Mark）是垃圾回收器构建所有可达对象图并将其标记为使用的阶段。标记阶段可以与应用程序线程并发执行。

- 扫描（Sweep）是垃圾回收器移动可达对象并更新其引用的阶段。扫描阶段需要在停止所有线程后进行。

- 固定钉（Pinning）是一种将对象锁定在位置以便垃圾回收器无法移动它的机制。用于需要托管对象指针的托管代码，并会导致碎片化。

- GC 变体（Flavors）为特定应用程序的器行为提供静态调优，以更好地利用其内存分配和释放模式。

- 代模型根据对象的当前年龄描述其预期寿命。年轻对象预计死亡得很快；老对象预计活得更久。

- 代（Generations）是根据其预期划分对象的内存概念区域。代有助于频繁地进行回收概率较高的部分回收，并减少进行开销大且效率较低的全回收。

- 大对象堆（Large object heap）是用于大对象的内存区域。LOH 会产生碎片，但不会移动，从而减少了扫描阶段的成本。

- 段（Segments）是由 CLR 分配的虚拟内存区域。由于段的大小是固定的，虚拟内存可能会碎片。

- 终结化（Finalization）是一种以非确定性方式自动释放未使用资源的备份机制。尽可能优选确定性终结而非自动终结化，但也提供了其他替代方案。

垃圾回收的常见陷阱通常与其最强大的优化的优点有关：

- 代模型为良好的应用程序提供了性能优势，但可能会表现出“中年危机”现象，这直接影响性能。

# 第 4 章 垃圾回收

- 当托管对象通过引用传递给非托管代码时，固定（Pinning）是必要的，但它会在 GC 堆中引入内部碎片，包括低代内存。
- 段（Segments）确保以大块形式分配虚拟内存，但可能会表现出虚拟内存空间的外部碎片。
- 自动终结（Automatic finalization）提供了非托管资源的释放，但它伴随着高性能开销，且往往会导致“中年危机”、高压力内存泄漏和竞态条件。

以下是充分利用 .NET 垃圾回收器的的一些最佳实践列表：

- 分配临时对象以便其销毁，但让旧对象在整个应用程序生命周期内存活。
- 在分配初始化时固定大型数组，并根据需要将其拆分为小型缓冲区。
- 在 GC 失败的地方使用池化或非托管分配来管理内存。
- 实现确定性终结，并将自动终结作为备份策略。
- 使用 GC 因素调整您的应用程序，以找到在各种硬件和软件配置上哪种因素效果最好。

以下是可用于诊断内存相关问题并从内存管理角度查看应用程序行为的工具：

- CLR Profiler：可诊断内部碎片、应用程序中的密集内存分配路径，查看每次垃圾回收时回收了哪些对象，并获取有关保留对象大小和年龄的统计数据。
- SOS.DLL：可用于诊断内存泄漏、分析外部和内部碎片、获取垃圾回收计时、列出托管堆中的对象、检查终结视图以及 GC 线程和终结线程的状态。
- CLR 性能计数器（performance counters）：可用于获取垃圾回收的通用统计数据，包括每代的大小、分配速率、终结信息、固定对象计数等。
- CLR 托管程序（CLR hosting）：可作为诊断实用程序，分析段、垃圾回收频率、导致垃圾回收的原因以及源自 CLR 的非 GC 内存分配请求。

配备了垃圾回收理论、所有相关机制的细微差别、常见陷阱和最佳性能实践，以及诊断工具和场景后，你现在准备好开始优化应用程序中的内存管理征程，并采用适当的内存管理策略设计它们。

## 集合与泛型

几乎没有哪个代码示例未使用未使用 `List<T>` 或 `Dictionary<K,V>` 等集合。大型应用程序可能在并发中使用数百个集合实例。根据需求选择正确的集合类型——或尝试通过编写自己的集合来改进——为许多应用程序提供显著的性能收益。由于 .NET 2.0 的出现，集合与 CLR 的泛型实现紧密结合，我们从泛型开始讨论。

## 泛型

经常需要创建一个可以与任何数据类型同样良好运行的类或方法。多态和继承只能提供有限的帮助；一个要求参数具有完全泛型方法将被迫与 `System.Object` 工作，这导致了 .NET 2.0 之前泛型编程的主要问题。

- 类型安全：如何在编译时验证对泛型数据类型进行的操作，并显式地禁止任何可能在运行时失败的程序？
- 无装箱（No boxing）：当参数为 `System.Object` 引用时，如何避免值类型的装箱？

这些都不是小问题。为了理解原因，请考虑 .NET 1.1 中最简单集合之一 `ArrayList` 的实现。以下是一个简化的实现，但它展示了上述问题：

```csharp
public class ArrayList : IEnumerable, ICollection, IList, ... {
    private object[] items;
    private int size;
    public ArrayList(int initialCapacity) {
        items = new object[initialCapacity];
    }
    public void Add(object item) {
        if (size < items.length - 1) {
            items[size] = item;
            ++size;
        } else {
            //分配一个更大的数组，复制元素，然后将 'item' 放入其中
        }
    }
    public object this[int index] {
        get {
```

# 第 5 章 集合与泛型

```csharp
if (index < 0 || index >= size) throw IndexOutOfBoundsException(index);
return items[index];
}
set {
if (index < 0 || index >= size) throw IndexOutOfBoundsException(index);
items[index] = value;
}
//为了简洁省略了许多方法
```

我们在整个代码中高亮了所有 `System.Object` 的出现处，它是集合所基于的“泛型”类型。虽然这可能是一个有效的解决方案，但实际用法并不十分直接：

```csharp
ArrayList employees = new ArrayList(7);
employees.Add(new Employee("Kate"));
employees.Add(new Employee("Mike"));
Employee first = (Employee)employees[0];
```

这种丑陋的 `Employee` 转换是必要的，因为 `ArrayList` 没有保留其内部元素的信息。此外，它没有限制插入其中的对象具有任何特征。
考虑：

```csharp
employees.Add(42); // 编译通过并在运行时运行！
Employee third = (Employee)employees[2]; // 编译通过并在运行时抛出异常...
```

 42 不属于员工集合，但是，如果我们指定了 `ArrayList` 被限制为特定类型的实例。虽然可以创建一个限制项目为特定类型的 `ArrayList`，但这仍然是一个开销很大的操作，并且像 `employees.Add(42)` 这样的语句仍然编译失败。
这就是泛型编程的问题；基于 `System.Object` 的集合无法保证类型安全，并且将检查推迟到运行时。

## .NET Generics

泛型类和方法允许编写真正的泛型代码，这一方面不会回退到 System.Object，另一方面也不需要为每种数据类型进行特化。以下是一个泛型类型 `List<T>` 的草图，它取代了我们之前的 `ArrayList`，并解决了安全性和装箱问题：

```csharp
public class List<T> : IEnumerable<T>, IList<T>, ... {
    private T[] items;
    private int size;
    public List(int initialCapacity) {
        items = new T[initialCapacity];
    }
    public void Add(T item) {
        if (size < items.Length - 1) {
            items[size] = item;
            ++size;
        } else {
            //分配一个更大的数组，复制元素，然后将'item' 放入其中
        }
    }
    public T this[int index] {
        get {
            if (index < 0 || index >= size) throw IndexOutOfRangeException(index);
            return items[index];
        }
        set {
            if (index < 0 || index >= size) throw IndexOutOfRangeException(index);
            items[index] = value;
        }
    }
    //为了简洁省略了许多方法
}
```

> 注意：如果你不熟悉 C# 泛型的所有语法，Jon Skeet 的《C# in Depth》（Manning, 2010）是一本很好的教材。在本章的剩余部分，假设我们已经编写了泛型类，或者至少是泛型类，例如 .NET Framework 类。

如果你已经编写过泛型类或方法，就会知道将基于 `System.Object` 实例的伪泛型代码转换为具有一个或多个泛型类型参数的真正泛型代码有多简单。在需要时替换泛型类型参数来使用泛型类和方法也非常容易：

```csharp
List<Employee> employees = new List<Employee>();
employees.Add(new Employee("Kate"));
Employee first = employees[0]; //无需下载，完全类型安全
employees.Add(42); // 无法编译！
List<Point2D> line = new List<Point2D>(100000);
for (int i = 0; i < 100000; ++i) {
    line.Add(new Point2D(i, i)); //无装箱，不存储引用
}
```

# 第5章 集合与泛型

几乎像魔术一样，泛型集合是类型安全的（即它不允许存储不恰当的元素，并且对值类型不需要装箱）。即使是内部存储——元素数组——也会根据泛型类型进行相应的调整：当 T 是 Point2D 时，items 数组就是 Point2D[]，存储的是值而不是引用。我们稍后会揭开其中的魔术，但目前我们已经为泛型编程的基本问题有了语言级别的解决方案。

当我们从泛型参数的某些额外功能时，仅靠这个解决方案似乎是不够的。考虑一个在排序数组中执行二分查找的方法。它的完全泛型版本无法执行搜索，因为 `System.Object` 没有配备任何比较相关的设施：

```csharp
public static int BinarySearch<T>(T[] array, T element) {
    // 在算法的某处，我们需要进行比较：
  if (array[x] < array[y]) {
    ...
  }
}
```

`System.Object` 没有静态运算符 `<`，这就是为什么它简单地无法编译。事实上，我们必须向编译器证明，对于传递给方法的每一个泛型类型，它都能解析在该类型上的所有方法调用（包括运算符）。这就是泛型约束登场的地方。

## 泛型约束

泛型约束告诉编译器，在使用泛型时，允许某些类型作为泛型类型参数。共有五种约束：

```csharp
// T 必须实现一个接口：
public interface T : IFormattable {
    public string Format(T instance) {
      return instance.ToString("N", CultureInfo.CurrentUI);
    }
}
// OK，T 必须有 IFormattable.ToString
```

```csharp
// T 必须继承自一个基类：
public void Display<T>(T widget) where T : Widget {
  widget.Display(0, 0);
}
// OK，T 继承自具有 Display(int, int) 方法的 Widget
```

```csharp
// T 必须有无参数构造函数：
public T Create<T>() where T : new() {
    return new T();
}
// OK，T 具有无参数构造函数
// C# 编译器将 'new T()' 编译为对 Activator.CreateInstance<T>() 的调用，
// 这并非最优，但 IL 没有对应的这种约束
```
