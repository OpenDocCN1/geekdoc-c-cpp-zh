
`Array.Copy` 不仅仅是一个从一个数组拷贝到另一个数组的方法。`Copy` 方法可以正确处理重叠的内存区域，相比之下，C# 的 `memcpy` 函数无法正确处理重叠区域。`Copy` 方法在执行拷贝期间，还可以对每个数组元素进行转换。`Copy` 方法能够执行以下转换：

- 将值类型元素装箱为引用类型元素，例如将 `Int32[]` 拷贝到 `Object[]`。
- 将引用类型元素拆箱为值类型元素，例如将 `Object[]` 拷贝到 `Int32[]`。
- 拓宽 CLR 原始值类型，例如将元素从 `Int32[]` 拷贝到 `Double[]`。
- 在无法证明与数组类型兼容的数组之间拷贝元素时进行向下转换，例如当数组类型为 `Object` 时。

在某些情况下，你可能需要将数组转换为特定类型以便使用该类型中的元素。这是一个示例：

```cs
// 定义接口
public interface IComparable
{
    int CompareTo(object obj);
}

// 实现接口的结构体
internal struct MyType : IComparable
{
    public int Value;
    public MyType(int value)
    {
        Value = value;
    }

    public int CompareTo(object obj)
    {
        if (obj is MyType other)
        {
            return Value.CompareTo(other.Value);
        }
        return -1;
    }
}

// 使用接口
public class Program
{
    public static void Main()
    {
        IComparable[] array = new IComparable[] { new MyType(10), new MyType(5), new MyType(8) };
        Array.Sort(array);
        foreach (var item in array)
        {
            Console.WriteLine(((MyType)item).Value);
        }
    }
}
```

# 所有数组隐式实现 IEnumerable、ICollection 和 IList

有很多方法可以对各种集合对象的操作，因为这些方法的声明中使用了诸如 `IEnumerable`、`ICollection` 和 `IList` 等参数。可以将数组传递给这些方法，因为 `System.Array` 实现了这三个接口。`System.Array` 实现这些非泛型接口是因为它们将所有元素视为 `System.Object`。然而，如果 `System.Array` 能实现这些接口的泛型等价项将会更好，提供更好的编译时类型安全性能。

CLR 团队并没有让 `System.Array` 实现 `IEnumerable<T>`、`ICollection<T>` 和 `IList<T>`，因为这涉及到多维数组和非零基数组的问题。在 `System.Array` 上定义这些接口将使所有数组类型都支持这些接口。相反，当创建一个单维、零基的数组类型时，CLR 会执行一个小技巧：CLR 会自动让该类型实现 `IEnumerable<T>`、`ICollection<T>` 和 `IList<T>`（其中 T 是数组的元素类型），并且只要其基类型是引用类型，就会为该数组的所有基类型实现这三个接口。下面的层次结构图清晰地说明了这一点。

Object

```
Array (非泛型 IEnumerable, ICollection, IList)
Object[] (IEnumerable, ICollection, List of Object)
String[] (IEnumerable, ICollection, List of String)
Stream[] (IEnumerable, ICollection, List of Stream)
FileStream[] (IEnumerable, ICollection, List of FileStream)
(其他引用类型的数组)
```

因此，例如，如果你有以下代码：

```
FileStream[] fsArray;
```

当 CLR 创建 `FileStream[]` 类型时，它会导致该类型自动实现 `IEnumerable<FileStream>`、`ICollection<FileStream>` 和 `IList<FileStream>` 接口。此外，`FileStream[]` 类型还将实现基类型的接口：`IEnumerable<Object>`、`IEnumerable<Stream>`、`ICollection<Object>`、`ICollection<Stream>` 和 `IList<Object>`。由于所有接口都是由 CLR 自动实现的，因此 `fsArray` 变量可以用任何存在这些接口的地方。例如，`fsArray` 变量可以传递给具有以下任何原型的方法：

```
void M1(IList<FileStream> fsList) { }
void M2(ICollection<Stream> sCollection) { }
void M3(IEnumerable<Object> oEnumerable) { }
```

注意，如果数组包含值类型元素，则数组类型将不会实现元素基类型的接口。例如，如果你有以下代码：

```
DateTime[] dtArray; // 一个值类型的数组
```

那么 `DateTime[]` 类型将仅实现 `IEnumerable<DateTime>`、`ICollection<DateTime>` 和 `IList<DateTime>`；它不会实现针对 `System.ValueType` 或 `System.Object` 泛型的接口版本。这意味着 `dtArray` 变量不能作为参数传递给之前所示的 `M` 方法。这是因为值类型数组在内存中的布局与引用类型数组不同。数组的内存布局在本章的早部分讨论过。

# 传递和返回数组

将数组作为参数传递给方法时，你实际上传递的是该数组的引用。因此，被调用的方法能够修改数组中的元素。如果你不想允许这样做，必须创建数组的副本并将副本传递给方法。注意 `Array.Copy` 方法执行的是浅拷贝，因此，如果数组元素是引用类型，则新数组将指向已经存在的对象。

同样，某些方法返回数组的引用。如果方法构造并初始化了数组，返回数组的引用是可以的。但如果方法想要返回由字段创建的内部数组的引用，你必须决定是否允许方法的调用者直接访问此数组及其元素。如果是的话，返回数组的引用。但大多数情况下，你不希望方法的调用者拥有这种访问权限，因此方法应该创建一个数组并调用 `Array.Copy`，返回新数组的引用。同样，要意识到 `Array.Copy` 对原始数组进行浅拷贝。

如果你定义了一个返回数组引用的方法，且该数组没有元素，你可以返回 `null` 或返回一个包含零元素的数组引用。当你实现此类方法时，微软强烈建议通过返回零长度数组来实现该方法，因为这简化了调用该方法的开发者必须编写的代码。例如，如果没有需要遍历的预约。

```
// 这段代码更容易编写和理解。
Appointment[] appointments = GetAppointmentsForToday();
for (int32 a = 0; a < appointments.Length; a++) {
    ...
}
```

如果没有需要遍历的预约，这段代码也能正确运行。然而，这种

```
// 这段代码更难编写和理解。
Appointment[] appointments = GetAppointmentsForToday();
if (appointments != null) {
```

```
for (Int32 a = 0; a < appointments.Length; a++) {
  // 对 appointments[a] 进行操作
}
```

如果你将方法设计为返回零元素数组而不是 `null`，方法的调用者在处理它们时会更加方便。顺便说一下，你也应该对字段这样做。如果你的类型有一个指向数组的字段，你应该考虑即使没有元素也让字段引用一个数组。

# 创建非零边界数组

我提到过可以创建并处理具有非零边界的数组。你可以通过指定下界来动态创建自己的数组。CLR 为数组分配内存，数组中的元素数量由上界和下界之间的差决定。如果你创建一个一维数组，下界通常是 0。如果你创建一个多维数组，可以为每个维度指定下界。

CLR 还支持不同类型的数组：

- 下界为 0 的单维数组。这些数组有时被称为 SZ（单维零基）数组或向量。
- 未知下界的单维和多维数组。

你可以通过执行以下代码来实际看到不同类型的数组（输出显示在代码注释中）：

```cs
using System;

public sealed class Program {
  public static void Main() {
  Array a;

  // 创建一个零元素的零基一维数组
  a = new String[0];
  Console.WriteLine(a.GetType()); // "System.String"

  // 创建一个零元素的零基一维数组
  a = Array.CreateInstance(typeof(String),
  new Int32[] { 0 }, new Int32[] { 0 });
  Console.WriteLine(a.GetType()); // "System.String"

  // 创建一个零元素的一基一维数组
  a = Array.CreateInstance(typeof(String),
  new Int32[] { 0 }, new Int32[] { 1 });
  Console.WriteLine(a.GetType()); // "System.String[]" --- 有趣！

  Console.WriteLine();
  }
}
```

```csharp
// 创建一个2维的、从0开始索引的数组，其中没有元素
a = new String[0, 0];
Console.WriteLine(a.GetType()); // "System.String[]",
```

```csharp
// 创建一个2维的、从1开始索引的数组，其中没有元素
a = Array.CreateInstance(typeof(String),
new Int32[][] { { 0, 0 }, new Int32[] { 0, 0 } });
Console.WriteLine(a.GetType()); // "System.String[]",
```

```csharp
// 创建一个2维的、从1开始索引的数组，其中没有
a = Array.CreateInstance(typeof(String),
new Int32[][] { 0, 0 }, new Int32[] { 1, 1 } });
Console.WriteLine(a.GetType()); // "System.String[]",
```

接下来每个 `Console.WriteLine` 都是指示输出的注释。对于多维数组，

基于0索引的数组显示的类型名称为 `System.String[,]`，而基于1索引的数组显示的

类型名称为 `System.String[*]`。*星号 表示 CLR 知晓这不是基于0索引的。注意，

C# 不允许你声明类型为 `String[*]` 的变量，因此无法使用 C# 语法来访问

单维的、非0索引的数组。虽然你可以调用 `Array.GetValue` 和 `SetValue` 来访问数组

的元素，但这种访问将产生方法调用的开销。

对于多维数组，基于0索引和基于1索引的数组在运行时都显示相同的类型名称：

`System.String[,]`。这会让你认为类型名称应该显示为

`System.String[*,*]`；然而，CLR 不在多维数组中使用 * 号，因为它们总是会出现的，

而且星号只会混淆开发者。

访问单维基于0索引数组的元素比访问非0索引的单维数组或多维数组的

元素要快一点。这有几个原因。首先，有一些 IL 指令——例如 `newlem`, `ldelem`, `ldelem`, `lddlem` 和 `stelem`——JIT 编译器使用这些指令来优化代码。例如，JIT

编译器会生成假设数组是基于0索引的代码，这意味着在访问元素时

不需要从索引中减去偏移量。其次，在通常情况下，JIT 编译器能够将索引范围检查的代码提升到循环外，导致其只执行一次。

```csharp
using System;

public class Program {
    public static void Main() {
    Int32[] a = new Int32[5];
    for(Int32 index = 0; index < a.Length; index++) {
        // 对 a[index] 执行某些操作
    }
    }
}
```

第16章 数组 385

关于这段代码首先要注意的一点是在循环测试表达式中对数组 `Length` 属性的调用。

由于 `Length` 是一个属性，查询长度实际上代表了一个方法调用。然而，JIT 编译器知道 `Length` 是 `Array` 类上的一个属性，

JIT 编译器实际上会生成调用它的代码，并将结果存储在临时变量中，

该变量将在循环的每次迭代中进行检查。结果是 JIT 后的代码非常快。事实上，有些开发者低估了 JIT 编译器的能力，并尝试编写“聪明”的代码来试图帮助 JIT 编译器。

然而，你想出的任何尝试几乎肯定会对性能产生负面影响，并让你的代码更难读，降低其可维护性。要么我们在代码中省略对数组 `Length` 属性的调用，

而不是尝试将其缓存在局部变量中。

关于前面的代码要注意的第二点是，JIT 编译器知道对于

循环 数组元素 - 1。所以 JIT 编译器产生代码来检查所有的

访问是否在数组的有效范围内。具体来说，JIT 编译器产生代码检查

`(i >= 0) && ((Length - a.LowerBound(0)) - 1) < a.UpperBound(0))`。这种检查发生在循环之前。JIT 编译器会生成代码来验证每次访问是有效的。这允许循环内的访问是快速的。

遗憾的是，如本文提到的，访问非0索引的单维数组

或多维数组比基于0索引的单维数组慢得多。对于这些类型，JIT 编译器不会将索引检查提升到循环外，所以 JIT 编译器添加代码从索引中减去数组的边界，这减慢了代码，即使你使用的是基于0索引的数组。如果你关心性能，你可能想

使用交错数组（jagged array）而不是矩形数组。C# 和 CLR 允许你通过不安全的（非验证的）代码访问数组，这实际上允许你在访问数组时关闭索引检查。这种技术适用于元素为

`SByte`, `Byte`, `Int16`, `UInt16`, `Int32`, `UInt32`, `Int64`, `UInt64`, `Char`, `Double`, `Boolean`

枚举类型或值类型的数组。这是一个强大的功能，允许你执行直接内存访问。如果这些内存访问超出了数组边界，不会抛出异常；你会损坏内存，违反类型安全并可能留下安全漏洞！由于由于，包含不安全代码的程序集必须授予完全信任或至少跳过验证的权限。下面的 C# 代码演示了访问二维数组的三种技术（安全的、交错的是不安全的）。
