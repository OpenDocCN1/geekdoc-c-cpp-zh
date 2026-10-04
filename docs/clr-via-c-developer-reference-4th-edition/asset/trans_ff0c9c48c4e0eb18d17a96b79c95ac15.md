
这里是显示此点的的代码。

```cs
private static void Method() {
    // 构建一个操作 DateTime 对象的列表
    List<DateTime> dtList = new List<DateTime>();

    // 将一个 DateTime 对象添加到列表
    dtList.Add(DateTime.Now);    // 无装箱

    // 将另一个 DateTime 添加列表
    dtList.Add(DateTime.MinValue); // 无装箱

    // 尝试将一个 String 对象添加到列表
    dtList.Add("1/2004");    // 编译时错误

    // 从列表中提取一个 DateTime 对象
    DateTime dt = dtList[0];
}
```

如上述代码所示，泛型为开发者带来了以下巨大益处：

- **源码保护**：使用泛型算法不需要访问算法的源代码。然而，使用 C++ 模板时，算法的源代码对使用该算法的开发者可见。

- **类型安全**：当泛型与特定类型一起使用时，编译器和 CLR 会理解并确保只有与指定数据类型兼容的对象才能在算法中使用。尝试使用不兼容的对象将导致编译错误或抛出运行时异常。在示例中，尝试向 Add 方法传递 String 对象会导致编译器发出错误。

- **代码更整洁**：由于编译器强制类型安全，源代码中需要的类型转换更少，这意味着你的代码更容易编写和维护。在 Method 的最后一行中，开发者不需要使用 `(DateTime)` 强制转换即可将索引器的结果（查询索引 0 处的元素）放入 `dt` 变量中。

为了强调泛型的性能优势，我编写了一个程序，测试了泛型 List 算法与非泛型 ArrayList 算法的性能。事实上，我同时使用值类型对象和引用类型对象测试了这两种算法的性能。以下是程序本身。

```cs
using System;
using System.Collections;
using System.Collections.Generic;
using System.Diagnostics;
```

```cs
public static class Program {
    public static void Main() {
        ValueTypePerf();
        ReferenceTypePerf();
    }

    private static void ValueTypePerf() {
        const Int32 count = 1000000000;

        using (new OperationTimer("List<Int32>")) {
            List<Int32> list = new List<Int32>();
            for (Int32 n = 0; n < count; n++) {
                list.Add(n); // 无装箱
                Int32 x = list[n]; // 无拆箱
            }
            list = null; // 确保被垃圾回收
        }

        using (new OperationTimer("ArrayList of Int32")) {
            ArrayList list = new ArrayList();
            for (Int32 n = 0; n < count; n++) {
                list.Add(n); // 装箱
                Int32 x = (Int32)list[n]; // 解箱
            }
            list = null; // 确保被垃圾回收
        }
    }

    private static void ReferenceTypePerf() {
        const Int32 count = 1000000000;

        using (new OperationTimer("List<String>")) {
            List<String> list = new List<String>();
            for (Int32 n = 0; n < count; n++) {
                list.Add("X"); // 引用拷贝
                String x = list[n]; // 引用拷贝
            }
            list = null; // 确保被垃圾回收
        }

        using (new OperationTimer("ArrayList of String")) {
            ArrayList list = new ArrayList();
            for (Int32 n = 0; n < count; n++) {
                list.Add("X"); // 引用拷贝
                String x = (String)list[n]; // 转换检查 & 引用拷贝
            }
        }
    }
}
```

```cs
}
a = null; // 确保被垃圾回收
}
}
```

```cs
// 此类用于对操作性能进行计时
internal sealed class OperationTimer : IDisposable {
private Stopwatch m_stopwatch;
private String m_text;
private Int32 m_collectionCount;
```

```cs
private OperationTimer(String text) {
PrepareForOperation();
```

```cs
m_text = text;
m_collectionCount = GC.CollectionCount(0);
```

```cs
// 这应该是该方法的最后一条语句
// 以尽可能保持计时的准确
m_stopwatch = Stopwatch.Start();
```

```cs
public void Dispose() {
Console.WriteLine("GCs=(1,3)) 2", (m_stopwatch.Elapsed);
GC.CollectionCount(0) - m_collectionCount, m_text);
}
```

```cs
private static void PrepareForOperation() {
GC.Collect();
GC.WaitForPendingFinalizers();
GC.Collect();
```

当我在我的计算机上编译并运行此程序（开启了优化）时，我得到了如下输出：

```
00:00:01.246959 (GCs=6) List<Int32>
00:00:10.855008 (GCs=390) ArrayOf Int32
00:00:02.542784 (GCs=4) List<String>
00:00:02.7944831 (GCs=7) ArrayListOf String
```

输出显示，使用 Int32 类型的泛型 List 算法远快于使用带 Int32 的非泛型 ArrayList。事实上，这种差异是惊人的：1.6 秒对比近 11 秒。在 ArrayList 中使用值类型（Int32）产生的约 ~7ms 导致了大量的装箱操作，从而导致 390 次垃圾回收。与此同时，ArrayList 只需要 6 次垃圾回收。

使用引用类型的测试结果并不那样单一。在这里我们看到，时间和垃圾回收次数是相同的。因此，使用泛型算法在这里似乎并没有任何益处。然而，请记住，当使用泛型算法时，你还会获得更整洁的代码和编译时类型安全。所以虽然性能提升不是巨大的，但使用泛型算法时获得的其他益处通常是种改进。

> 注意 你需要意识到，CLR 在第一次为特定类型调用每个方法时，会为该方法生成原生代码。这将增加应用程序的工作集大小，从而影响性能。我将在“泛型基础”章节中详细讨论。

## 框架类库中的泛型

无疑，泛型最明显的用法是在集合类中，FCL 定义了许多供你使用的泛型类。大多数这些类可以在 `System.Collections.Generic` 命名空间中找到。在 `System.Collections.ObjectModel` 命名空间中也有许多。此外，`System.Collections.Concurrent` 命名空间提供了线程安全的泛型类。微软建议程序员使用泛型集合类，不再建议使用非泛型类，原因如下：首先，非泛型类不是泛型的，你无法获得使用泛型集合时带来的类型安全、更整洁以及更好的性能。其次，泛型类比非泛型类具有更好的对象模型。例如，虚方法更少，从而提高了性能，并且泛型集合中增加了新的成员以提供功能。

集合类实现了许多接口，你放入集合的对象也实现了这些排序和搜索操作接口。FCL 带有许多泛型接口定义，以便在处理接口时实现泛型的益处。常用的接口包含在 `System.Collections.Generic` 命名空间中。

新的泛型接口并不是旧非泛型接口的替代品；在许多场景下，你需要使用两者。这是为了向下兼容。例如，如果 `List<T>` 类只实现 `IList` 接口，那么代码无法创建一个实现 `IList` 的 `List<DateTime>` 对象。

我还应该指出，作为所有类型基类的 `System.Array` 类提供了许多静态泛型方法，如 `AsReadOnly`、`BinarySearch`、`ConvertAll`、`Exists`、`Find`、`FindAll`、`IndexOf`、`FindLast`、`LastIndexOf`、`ForEach`、`Resize`、`Sort` 和 `TrueForAll`。这里是显示其中一些方法的示例。

```cs
public abstract class Array : ICloneable, IList, ICollection, IEnumerable,
IStructable, IEquatable {

public static void Sort<T>(T[] array);
public static void Sort<T>(T[] array, IComparer<T> comparer);

public static Int32 BinarySearch<T>(T[] array, T value);
public static Int32 BinarySearch<T>(T[] array, T value,
IComparer<T> comparer);
}
```
