
```csharp
private static void SomeMethod() {
    // 构建一个操作 DateTime 对象的列表
    List<DateTime> dtList = new List<DateTime>();

    // 向列表添加一个 DateTime 对象
    dtList.Add(DateTime.Now);      // 无装箱

    // 向列表添加另一个 DateTime 对象
    dtList.Add(DateTime.MinValue); // 无装箱

    // 尝试向列表添加一个 String 对象
    dtList.Add("1/1/2004");       // 编译时错误

    // 从列表中提取一个 DateTime 对象
    DateTime dt = dtList[0];
}
```

正如刚才展示的代码所示，泛型为开发者提供了以下巨大的优势：

- **源代码保护** 开发者不需要访问源代码。对于 C++ 模板或 Java 泛型，算法的源代码必须是可见。
- **类型安全** 当泛型算法与特定类型一起使用，编译器和 CLR 确保只有兼容类型的对象被使用。尝试使用不兼容类型会导致错误或抛出运行时异常。
- **更整洁的代码** 由于泛型强制类型安全，代码不再需要强制转换，这意味着代码更易编写和维护。在 `SomeMethod` 的最后一行，开发者不需要将索引器的结果（查询元素）转换为 `DateTime`。
- **更好的性能** 在泛型出现之前，泛化算法必须与 `Object` 类型工作。正如第 5 章“原始、引用和值类型”中所讨论的，值类型会导致托管堆上的内存分配，从而导致频繁的垃圾回收。由于泛型现在可以与特定的值类型创建，CLR 不再需要进行任何装箱。

为了进一步说明泛型的性能优势，我写了一个程序来测试泛型 `List` 与 FCL 非泛型 `ArrayList` 算法的性能。事实上，我使用值类型和引用类型对象测试了这两个算法。以下是程序本身：

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Diagnostics;

public static class Program {
    public static void Main() {
        ValueTypePerfTest();
        ReferenceTypePerfTest();
    }

    private static void ValueTypePerfTest() {
        const Int count = 1000000;

        using (new OperationTimer("List<Int32>")) {
            List<Int32> l = new List<Int32>(count);
            for (Int32 n = 0; n < count; n++) {
                l.Add(n);
            }
            Int32 x = l[n];
            l = null; // 确保这个被 GC 回
        }

        using (new OperationTimer("ArrayList of Int32")) {
            ArrayList a = new ArrayList();
            for (Int32 n = 0; n < count; n++) {
                a.Add(n);
            }
            Int32 x = (Int32) a[n];
            a = null; // 确保这个被 GC 回
        }
    }

    private static void ReferenceTypePerfTest() {
        const Int count = 1000000000;

        using (new OperationTimer("List<String>")) {
            List<String> l = new List<String>();
            for (Int32 n = 0; n < count; n++) {
                l.Add("X");
            }
            String x = l[n];
        }
    }
}
```

# 第 12 章 泛型 279

```csharp
l = null; // 确保此对象被 GC 回
}
using (new OperationTimer("ArrayList of String")) {
  ArrayList a = new ArrayList();
  for (Int32 n = 0; n < count; n++) {
    a.Add("X");
    String x = a[n];
  }
  a = null; // 确保此对象被 GC 回
}
}
```

// 此类用于对操作性能进行计时

```csharp
internal sealed class OperationTimer : IDisposable {

  private Int64 m_startTime;

  private String m_text;

  private Int32 m_collectionCount;

public OperationTimer(String text) {
  PrepareForOperation();

  m_text = text;
  m_collectionCount = GC.CollectionCount(0);

  // 这应该是该方法的最后一条语句
  // 以保持计时尽可能的准确
  m_startTime = Stopwatch.GetTimestamp();
}

public void Dispose() {
  Console.WriteLine("{0,6:#.00} seconds GCs={1,3}}{2}",
  (Stopwatch.GetTimestamp() - m_startTime) /
  (Double)Stopwatch.Frequency,
  GC.CollectionCount(0) - m_collectionCount, m_text);
}

private static void PrepareForOperation() {
  GC.Collect();
  GC.WaitForPendingFinalizers();
  GC.Collect();
}
```

当我在电脑上编译并运行此程序的发布版本（开启优化）时，我得到了如下输出：

+ .10 seconds (GCs=0) List<Int32>

- .02 seconds (GCs=45) ArrayList

- .47 seconds (GCs=6) List<String>

- .51 seconds (GCs=6) ArrayList

# 第二部分 类型设计

这里的输出显示，使用 `Int32` 类型的泛型 `List` 算法比使用带有 `Int32` 的非泛型 `ArrayList` 算法要快得多。事实上，这种差异是惊人的：一秒对比三秒。那简直是快了 30 倍！此外，在 `ArrayList` 中使用值类型（`Int32`）会导致大量的装箱操作，从而导致了 45 次垃圾回收。与此同时，`List` 算法只需要 0 次垃圾回收。使用引用类型的测试结果并不显著。因此，泛型算法在这里似乎并没有带来什么优势。然而，请记住，当使用泛型算法时，你还获得了更整洁的代码和编译时类型安全。虽然性能提升不是巨大的，但你需要意识到，每当为特定数据类型第一次调用方法时，CLR 都会为其生成原生代码。这会增加应用程序的工作集。我将在本章的“泛型基础设施”部分更详细地讨论这一点。

## 框架库中的泛型

无疑，泛型最明显的用途是用于集合类。大多数这些类可以在 `System.Collections.Generic` 命名空间和 `System.ObjectModel` 命名空间中找到。`System.Collections.Concurrent` 命名空间也提供了线程安全的集合类。微软推荐使用泛型类，并不建议使用非泛型集合，原因如下：

首先，非泛型集合类不是泛型的，你无法获得使用泛型类时获得的类型安全、更整洁的代码和更好的性能。其次，泛型类比非泛型类具有更好的对象模型。例如，更少的方法是虚方法，从而带来了更好的性能，并且泛型集合中添加了新成员以提供新功能。集合类实现了许多接口，你放入集合中的对象可以实现集合类用于排序和搜索等操作的接口。FCL（框架类库）随带了许多接口定义，以便在处理接口时也能实现泛型的益处。常用的接口包含在 `System.Collections.Generic` 命名空间中。

新的泛型接口并不是旧的非泛型接口的替代品；在许多场景下，你必须同时使用两者。这是为了向后兼容性；例如，如果 `List<T>` 类只实现了 `IList<T>` 接口，那么没有任何代码可以将一个 `List` 对象视为 `IList`。我还应该指出，`System.Array` 类（所有数组类型的基类）提供了许多静态泛型方法，如 `AsReadOnly`, `BinarySearch`, `ConvertAll`, `Exists`, `Find`, `FindAll`, `IndexFirst`, `FindLast`, `FindIndexOf`, `ForEach`, `IndexOf`, `LastIndexOf`, `Resize`, `Sort`, 和 `TrueForAll`。以下是展示其中一些方法的示例：

```csharp
public abstract class Array : ICloneable, IList, ICollection, IEnumerable,
StructuralComparable, IEquatable {

    public static void Sort<T>(T[] array);
    public static void Sort<T>(T[] array, IComparer<T> comparer);

    public static Int32 BinarySearch<T>(T[] array, T value);
    public static Int32 BinarySearch<T>(T[] array, IComparer<T> comparer);

    ...
}

public static void Main() {
    // 创建并初始化一个字节数组
    Byte[] byteArray = new Byte[] { 5, 1, 4, 2, 3 };

    // 调用排序算法
    Array.Sort(byteArray);

    // 调用二分查找算法
    Int32 i = Array.BinarySearch<Byte>(byteArray, 1);
    Console.WriteLine(i); // 显示 "0"
}
```

以下是演示如何使用其中一些方法的代码：

## Wintlect Power Collections 库

应微软的要求，Wintlect 生成了 Power Collections 库，旨在将 C++ 标准模板库（STL）的一些类引入 CLR 程序员手中。该库是一组集合类，任何人都可以免费下载和使用。详情请参阅 http://Wintlect.com。这些集合类本身是泛型的，并广泛使用了泛型。表 12-1 显示了在 Power Collections 库中可以找到集合类列表。

表 12-1 来自 Wintlect Power Collections 库的泛型集合类

| 集合类 | 描述 |
| :--- | :--- |
| List<T> | 有序 T 对象集合。在处理超过 100 个项目时非常高效。 |
| Bag<T> | 有序 T 对象集合。该集合是哈希的，并允许重复项。 |
| OrderedBag<T> | 有序 T 对象集合。允许重复项。 |
| Set<T> | 有序 T 项目集合。不允许重复项。 |
| OrderedSet<T> | 有序 T 项目集合。不允许重复项。 |
| Deque<T> | 双端队列。 |
| Dictionary<TKey, TValue> | 有序键值对集合。查找非常高效。 |
| SortedDictionary<TKey, TValue> | 按键排序的键值对集合。 |
| SortedList<TKey, TValue> | 按键排序的键值对集合。 |
| ConcurrentDictionary<TKey, TValue> | 线程安全的键值对集合。 |

# 284 第二部分 设计类型

```cs
// 尝试创建该类型的实例（失败）
o = CreateInstance(t);
Console.WriteLine();
```

```cs
// DictionaryString<Key> 是一个拥有 1 个类型的开放类型
t = typeof(DictionaryString<Key>);
```

```cs
// 尝试创建该类型的实例（失败）
o = CreateInstance(t);
Console.WriteLine();
```

```cs
// DictionaryString<Guid> 是一个闭闭类型
t = typeof(DictionaryString<Guid>);
```

```cs
// 尝试创建该类型的实例（成功）
o = CreateInstance(t);
```

```cs
// 证明它确实起了
Console.WriteLine("Object type=" + o.GetType());
}

private static Object CreateInstance(Type t) {
    Object o = null;
    try {
        o = Activator.CreateInstance(t);
        Console.WriteLine("Created instance of {0}", t.ToString());
    } catch (ArgumentException e) {
        Console.WriteLine(e.Message);
    }
    return o;
}
```

当我编译并运行代码时，我得到了如下输出：

Cannot create an instance of System.Collections.Generic.Dictionary`Key,Value` because Type.ContainsGenericParameters is true.

Cannot create an instance of DictionaryString`TValue` because Type.ContainsGenericParameters is true.

Created instance of DictionaryString[System.Guid].

Object type=DictionaryString[System.Guid].

如你所见，当你要求 **Activator's CreateInstance** 方法创建一个开放类型的实例时，它会抛出一个 **ArgumentException**。事实上，异常的字符串消息表明该类型仍然包含某些泛型参数。

在输出中，你会注意到类型名称后面跟着一个反引号（``）和一个数字。该数字表示类型的**元数（arity）**，它表示该类型所需的类型参数的数量。例如，**Dictionary** 类的元数为 2，因为它需要为 **TKey** 和 **TValue** 指定类型。**DictionaryString** 类的元数为 1，因为它只需要为 **TValue** 指定一个类型。

第 12 章 泛型 285

我还应该指出，正如第 4 章“类型基础”中所讨论的样，CLR 在类型对象内部分配类型的静态字段。因此，每个闭闭类型都有自己的静态字段。换句话说，如果 `List<T>` 定义了任何静态字段，这些字段在 `List<DateTime>` 和 `List<String>` 之间是不共享的；每个闭闭类型都有自己的静态字段。此外，如果泛型类型定义了静态构造函数（在第 8 章“方法”中讨论），该构造将在每个封闭类型执行一次。有些人会在泛型类型上定义静态构造函数，以确保类型参数符合某些标准。例如，如果你想定义一个只能与枚举类型使用的泛型类型，你可以这样做：

```cs
internal sealed class GenericTypeRequiresAnEnum<T> {
    static GenericTypeRequiresAnEnum() {
        if (!typeof(T).IsEnum) {
            throw new ArgumentException("T must be an enumerated type");
        }
    }
}
```

CLR 有一种名为“约束”（constraints）的功能，它为你提供了一种更好的方法来定义泛型类型，指示哪些参数是有效的。我将在本章稍后的部分讨论约束。遗憾的是，约束不支持将类型参数仅限制为枚举类型，这就是为什么前面的示例需要静态构造函数来确保该类型是枚举类型。

## 泛型类型与继承

泛型类型是一种类型，因此它可以派生自任何其他类型。当你使用泛型类型并指定类型参数时，你正在 CLR 中定义一个新对象，而新的类型对象派自该泛型类型派自的任何类型。换句话说，由于 `List<T>` 派自 `Object`，因此 `List<String>` 和 `List<Guid>` 也派自 `Object`。同样，由于 `Dictionary<String, TValue>`，`Dictionary<String, Guid>` 也派自 `Dictionary<String, Guid>`。理解指定类型参数与继承层次无关，有助于你识别哪些转换是可以、哪些不能。
