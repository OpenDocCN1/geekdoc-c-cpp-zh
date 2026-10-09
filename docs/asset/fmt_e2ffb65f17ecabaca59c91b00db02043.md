
```
FileStream[] fs;
```

CLR 会自动为 AppDomain 创建一个 `FileStream[]` 类型。该类型隐式派生自 `System.Array` 类型，因此定义在 `System.Array` 类型上的所有实例方法和属性都将被 `FileStream[]` 类型继承，允许使用 `fsArray` 变量调用这些方法和属性。这使得处理数组变得极其方便，因为 `System.Array` 提供了许多有方法和属性，例如 `Clone`、`CopyTo`、`GetLength`、`GetLowerBound`、`GetUpperBound`、`Length`、`Rank` 等。

`System.Array` 类型还暴露了大量非常有用的静态方法来操作数组。这些方法都接受数组的引用作为参数。一些实用的静态方法包括 `AsReadOnly`、`BinarySearch`、`Search`、`ConstrainedCopy`、`ConvertAll`、`Copy`、`Exists`、`Find`、`FindAll`、`FindIndex`、`FindLastIndex`、`LastIndexOf`、`ForEach`、`IndexOf`、`Resize`、`Reverse`、`Sort` 和 `TrueAll`。这些方法都有许多重载。事实上，许多方法提供了泛型重载以实现编译时的类型安全和良好的性能。鼓励你查看 SDK 文档，以了解这些方法的强大。

## 所有数组隐式实现 IEnumerable、ICollection 和 IList

有很多方法操作各种集合对象，因为这些方法的声明使用了 `IEnumerable`、`ICollection` 和 `IList` 等参数。可以将数组传递给这些方法，因为 `System.Array` 实现了这些非泛型接口，因为这些接口将所有元素视为 `System.Object`。然而，如果 `System.Array` 能实现这些接口的泛型等效版本，具有更好的编译时类型安全性和性能将会更好。

尽管，CLR 没有让 `System.Array` 实现 `IEnumerable<T>`、`ICollection<T>` 和 `IList<T>`，这是由于与多维数组和非零基数组相关的问题。在 `System.Array` 上定义这些接口将允许所有数组类型支持这些接口。然后，CLR 采用了一个小技巧：当创建一个维度的、零下界的数组类型时，CLR 会自动让该数组类型实现 `IEnumerable<T>`、`ICollection<T>` 和 `IList<T>`（其中 `T` 是数组的元素类型），并且只要数组的所有基类型是引用类型，就会为它们所有基类型实现这三个接口。下面的层次结构有助于阐明这一点：

```
Array[(非泛型 IEnumerable, ICollection, IList)
Object[] (IEnumerable, ICollection, List of Object)
String[] (IEnumerable, ICollection, List of String)
Stream[] (IEnumerable, ICollection, List of Stream)
FileStream[] (IEnumerable, ICollection, List of FileStream)

(其他引用类型的数组)
```

例如，如果你有下面这行代码：

```
FileStream[] fsArray;
```

当 CLR 创建 `FileStream[]` 类型时，它将自动实现 `IEnumerable<FileStream>`、`ICollection<FileStream>` 和 `IList<FileStream>` 接口。此外，`FileStream[]` 还会实现基类型的接口：`IEnumerable<Stream>`、`IEnumerable<Object>`、`ICollection<Stream>`、`ICollection<Object>`、`IList<Stream>` 和 `IList<Object>`。由于所有接口都由 CLR 自动实现，`fsArray` 变量可以在任何使用这些接口的地方。例如，`fsArray` 变量可以传递给具有以下任何原型的方法：

```
void M1(IList<FileStream> fsList) { ... }
void M(ICollection<Stream> sCollection) { ... }
void M(IEnumerable<Object> enumerable) { ... }
```

## 传递和返回数组

注意，如果数组包含值类型元素，数组类型将实现元素基类型的接口。例如，如果你有下面这行代码：

```
DateTime[] dtArray; // 一个值类型的数组
```

那么 `DateTime` 类型将仅实现 `IEnumerable<DateTime>`、`ICollection<DateTime>` 和 `IList<DateTime>`；它不会实现这些针对 `System.ValueType` 或 `System.Object` 泛化的接口版本。这意味着 `dtArray` 变量不能作为参数传递给前面所示的 `M` 方法。原因是值类型数组在内存中的布局与引用类型数组不同。数组内存布局在本章前面讨论过。

当将数组作为参数传递给方法时，你实际上传递的是该数组的引用。如果你不想允许这样做，你必须创建数组的副本并将副本传递给方法。注意 `Array.Copy` 执行的是浅拷贝，因此，如果数组元素是引用类型，则新数组将指向现有对象。

同样，某些方法返回数组的引用。如果方法构造并初始化了一个数组，返回该数组的引用是可以的。但如果方法想要返回由字段维护的内部数组的引用，你必须决定是否希望方法的调用者直接访问该数组及其元素。如果你不希望方法调用者具有此类访问权限，方法应该构造一个新数组并返回新数组的引用。请注意 `Array.Copy` 执行的是浅拷贝。

## 创建非零下界数组

早些我提到可以创建并处理具有非零下界的数组。你可以调用 `Array` 的静态方法 `CreateInstance` 来动态创建数组。该方法有多个重载，允许你指定数组的元素类型、数组的维度、每个维度的下界以及每个维度的元素数量。`CreateInstance` 为数组分配内存，将参数信息保存在数组的开销部分，并返回数组的引用。如果数组有两个或维度，你可以将 `CreateInstance` 返回的引用转换为 `Element[]` 变量（其中 `Element` 是类型名称），以便你访问数组中的元素。如果数组只有一个维度，在 C# 中，你必须使用 `Array` 的 `GetValue` 和 `SetValue` 方法来访问数组元素。

下面的代码演示了如何动态创建一个 `System.Decimal` 的二维数组。第一个维度代表从 2005 年到 2009 年的年份，第二个维度代表从 1 到 4 的季度。代码遍历了动态数组的所有元素。我在代码中硬编码了数组边界，这可以获得更好的性能，但我决定使用 `System.Array` 的 `GetLowerBound` 和 `GetUpperBound` 方法来演示它们的用法：

```csharp
using System;

public class DynamicArrays {
    public static void Main() {
        // I 一个二维数组 [2005..2009][1..4]
        Int32[] lowerBounds = { 2005, 1 };
        Int32[] lengths = { 5, 4 };
        Decimal[,] quarterlyRevenue = (Decimal[,])
            Array.CreateInstance(typeof(Decimal), lowerBounds, lengths);

        Console.WriteLine("{0,4} {1,9} {2,9} {3,9}", "Year", "Q1", "Q2", "Q3", "Q4");
        Int32 firstYear = quarterlyRevenue.GetLowerBound(0);
    }
}
```

`Int32 lastYear = quarterlyRevenue.GetUpperBound(0);`

`Int32 firstQuarter = quarterlyRevenue.GetLowerBound(1);`

`Int32 lastQuarter = quarterlyRevenue.GetUpperBound(1);`

```csharp
for (Int32 year = firstYear; year <= lastYear; year++) {
    Console.WriteLine(year + " ");
    for (Int32 quarter = firstQuarter; quarter <= lastQuarter; quarter++) {
        Console.WriteLine("{0,9:C}", quarterlyRevenue[year, quarter]);
    }
    Console.WriteLine();
}
}
```

如果你编译并运行这段代码，你将得到以下结果：

| 年 | Q1 | Q2 | Q3 | Q4 |

| :--- | :--- | :--- | :--- | :--- |

| 2005 | $0.00 | $0.00 | $0.00 | $0.00 |

| 2006 | $0.00 | $0.00 | $0.00 | $0.00 |

| 2007 | $0.00 | $0.00 | $0.00 | $0.00 |

| 2008 | $0.00 | $0.00 | $0.00 | $0.00 |

| 2009 | $0.00 | $0.00 | $0.00 | $0.00 |

## 数组访问性能

在内部，CLR 支持两种数组：

- 下界为 0 的单维数组。这些数组有时被称为 SZ（single-dimensional 的缩写）。

你实际上可以通过执行以下代码来看到不同类型的数组（输出显示在代码的注释中）：

```csharp
using System;

public sealed class Program {
    public static void Main() {
        Array a;

        // 创建一个 1 维、从 0 开始的数组，其中没有元素
        a = new String[0];
        Console.WriteLine(a.GetType()); // "System.String[]"

        // 创建一个 1 维、从 0 开始的数组，其中没有元素
        a = Array.CreateInstance(typeof(String), new Int32[] { 0 });
        Console.WriteLine(a.GetType()); // "System.String[]"

        // 创建一个 1 维、从 1 开始的数组，其中没有元素
        a = Array.CreateInstance(typeof(String), new Int32[] { 0 }, new Int32[] { 1 });
        Console.WriteLine(a.GetType());    // "System.String[]*" <-- 有趣！
    }
}
```

```csharp
Console.WriteLine();
```

```csharp
// 创建一个 2 维、从 0 开始的数组，其中没有元素
a = new String[0, 0];
Console.WriteLine(a.GetType());    // "System.String[,]]"
```

```csharp
// 创建一个 2 维、从 0 开始的数组，其中没有元素
a = Array.CreateInstance(typeof(String), new Int32[] { 0, 0 }, new Int32[] { 0, 0 });
Console.WriteLine(a.GetType());    // "System.String[,]]"
```

```csharp
// 创建一个 2 维、从 1 开始的数组，其中没有元素
a = Array.CreateInstance(typeof(String), new Int32[] { 0, 0 }, new Int32[] { 1, 1 });
Console.WriteLine(a.GetType());    // "System.String[,]]"
```

每个 `Console.WriteLine` 旁边都有一个注释指示输出内容。对于单维数组，从 0 开始的数组显示类型名称为 `System.String[]`，而从 1 开始的数组显示类型名称为 `System.String[,]]`。CLR 知道该数组不是从 0 开始的。注意，C# 不允许你声明类型为 `String[*]` 的变量，因此无法使用 C# 语法访问非从 0 开始的单维数组。虽然你可以调用 `Array` 的 `GetValue` 和 `SetValue` 方法来访问数组元素，但这种访问将产生于方法调用的开销。

对于多维数组，从 0 开始和从 1 开始的数组都显示相同的类型名称：`System.String[,]]`。CLR 在运行时将所有多维数组都视为不是从 0 开始的。这会让你认为类型名称应该显示为 `System.String[*]`；然而，CLR 不在多维数组中使用 `*`，因为它们是显式存在的，且星号会困扰大多数开发者。

访问从 0 开始的单维数组元素，比访问非从 0 开始的单维数组或多维数组元素要快一点。这其中有几个原因：首先，有特定的 IL 指令（如 `newarr`、`ldelem`、`ldlen` 和 `elelelem`）用于操作从 0 开始的单维数组，而这些特殊的 IL 指令会导致 JIT 编译器产生优化后的代码。例如，JIT 编译器将产生假设数组是从 0 开始的代码，这意味着在访问元素时，不需要从指定的索引中减去偏移量。其次，在常见情况下，JIT 编译器能够将索引范围检查提取到循环之外，使其只执行一次。例如，查看以下常见的写法：

### 第 16 章 数组 401

最后，请注意，不安全的二维数组访问技术与安全的二维数组访问技术速度不相，但如果你考虑到它访问的是单维数组（仅需一次分配），而创建的是交错数组（需要多次内存分配），那么它会被认为是所有技术中是最快的。显然，不安全技术是有代价的，而且当你自己的代码可以使用这种技术时，请注意使用该技术有三个严重的缺点：

- 操控数组元素的代码比使用其他技术操作元素的代码更难阅读和编写，因为你使用了 C# 的 `fixed` 语句并执行了内存地址计算。

- 如果你在计算中犯了错误，你将访问到不属于数组的内存。这可能导致计算错误、内存损坏、类型安全违规以及潜在的安全漏洞。

- 由于这些潜在问题，CLR（公共语言运行时）禁止在低安全性环境（如 Microsoft Silverlight）中运行 `unsafe` 代码。

## 不安全的数组访问与固定大小数组

不安全的数组访问非常强大，因为它允许你访问：

- 托管在堆上的托管数组对象内部的元素（上一节已演示）。

- 位于非托管堆上的数组内部的元素。第 14 章“字符、字符串与文本处理”中的 `SecureString` 示例演示了如何对调用 `System.Runtime.InteropServices.Marshal` 类的 `SecureStringToCoTaskMemUnicode` 方法返回的数组进行访问。

- 位于线程栈上的数组内部的元素。

在内存分配极其关键的情况下，你可以避免在堆上创建托管数组对象，而是而使用 C# 的 `stackalloc` 语句在栈上分配数组（其工作原理类似于 C 语言的 `alloca` 函数）。`stackalloc` 语句可用于创建一个值类型元素的零基索引一维数组，且该值不能包含任何引用类型。实际上，你应该将其视为分配了一个可以使用 `unsafe` 指针操作的内存块，因此，你不能将此内存缓冲区的地址传递给大多数 FCL（框架类库）方法。当然，栈分配的内存（数组）会在方法返回时自动释放；这正是我们获得性能提升的地方。使用此功能要求你在使用 C# 编译器运行时 `/unsafe` 选项。

下面代码中的 `StackallocDemo` 方法演示了如何使用 C# 的 `stackalloc` 语句。
