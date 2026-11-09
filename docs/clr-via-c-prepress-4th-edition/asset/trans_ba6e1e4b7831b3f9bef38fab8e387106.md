
```csharp
void M1(List<FileStream> fList) { ... }
void M2(ICollection<Stream> collection) { ... }
void M3(IEnumerable<Object> oEnumerable) { ... }
```

注意，如果数组包含值类型元素，数组类型将不会实现元素基类型的接口。例如，如果有下面这行代码，

```csharp
DateTime[] dtArray; // An array of value types
```

那么 DateTime[] 类型将只实现 IEnumerable<DateTime>、ICollection<DateTime> 和 IList<DateTime>；它不会实现这些接口中针对 System.ValueType 或 System.Object 泛型化的版本。这意味着 dtArray 变量不能作为参数传递给前面展示的 M3 方法。原因在于值类型数组在内存中的布局方式与引用类型数组不同。本章前面已讨论过数组的内存布局。

## 传递和返回数组

当将数组作为参数传递给方法时，实际上传递的是对该数组的引用。因此，被调用的方法能够修改数组中的元素。如果不希望允许这样做，必须创建数组的副本，并将副本传入方法。注意，Array.Copy 方法执行的是浅拷贝，因此，如果数组的元素是引用类型，新数组将引用已存在的对象。

类似地，有些方法会返回对数组的引用。如果方法构造并初始化该数组，那么返回对数组的引用没有问题。但如果方法想返回对由字段维护的内部数组的引用，就必须决定是否希望方法的调用者可以直接访问该数组及其元素。如果希望，只需返回数组的引用。但大多数情况下，你不希望方法的调用者拥有这种访问权限，因此方法应构造一个新数组并调用 Array.Copy，返回对新数组的引用。同样要注意，Array.Copy 对原始数组进行的是浅拷贝。

如果定义的方法返回对数组的引用，并且该数组中没有元素，那么方法可以返回 null，也可以返回对零元素数组的引用。在实现这类方法时，Microsoft 强烈建议让方法返回零长度数组，因为这样可简化调用该方法的开发人员必须编写的代码。例如，下面这段易于理解的代码即使没有可迭代的预约也能正确运行。

```csharp
// This code is easier to write and understand.
Appointment[] appointments = GetAppointmentsForToday();
for (Int32 a = 0; a < appointments.Length; a++) {
    ...
}
```

如果没有可迭代的预约，下面这段代码也能正确运行。然而，下面这段：

```csharp
Int32 firstYear    = quarterlyRevenue.GetLowerBound(0);
Int32 lastYear     = quarterlyRevenue.GetUpperBound(0);
Int32 firstQuarter = quarterlyRevenue.GetLowerBound(1);
Int32 lastQuarter  = quarterlyRevenue.GetUpperBound(1);

for (Int32 year = firstYear; year <= lastYear; year++) {
    Console.Write(year + " ");
    for (Int32 quarter = firstQuarter; quarter <= lastQuarter; quarter++) {
        Console.Write("{0,9:C} ", quarterlyRevenue[year, quarter]);
    }
    Console.WriteLine();
}
```

如果编译并运行这段代码，将得到以下输出：

| 年份 | 第1季度 | 第2季度 | 第3季度 | 第4季度 |
|---|---|---|---|---|
| 2005 | $0.00 | $0.00 | $0.00 | $0.00 |
| 2006 | $0.00 | $0.00 | $0.00 | $0.00 |
| 2007 | $0.00 | $0.00 | $0.00 | $0.00 |
| 2008 | $0.00 | $0.00 | $0.00 | $0.00 |
| 2009 | $0.00 | $0.00 | $0.00 | $0.00 |

### 数组内部

在内部，CLR 实际上支持两种不同的数组：

- 下限为 0 的一维数组。这类数组有时称为 SZ（表示单维、从零开始）数组或向量。
- 下限未知的一维数组和多维数组。

实际上，可以通过执行以下代码看到不同类型的数组（输出显示在代码注释中）：

```csharp
using System;

public sealed class Program {
    public static void Main() {
        Array a;

        // Create a 1-dim, 0-based array, with no elements in it
        a = new String[0];
        Console.WriteLine(a.GetType());   // "System.String[]"

        // Create a 1-dim, 0-based array, with no elements in it
        a = Array.CreateInstance(typeof(String),
            new Int32[] { 0 }, new Int32[] { 0 });
        Console.WriteLine(a.GetType());   // "System.String[]"

        // Create a 1-dim, 1-based array, with no elements in it
        a = Array.CreateInstance(typeof(String),
            new Int32[] { 0 }, new Int32[] { 1 });
        Console.WriteLine(a.GetType());   // "System.String[*]"  <-- INTERESTING!

        Console.WriteLine();

        // Create a 2-dim, 0-based array, with no elements in it
        a = new String[0, 0];
        Console.WriteLine(a.GetType());   // "System.String[,]"

        // Create a 2-dim, 0-based array, with no elements in it
        a = Array.CreateInstance(typeof(String),
            new Int32[] { 0, 0 }, new Int32[] { 0, 0 });
        Console.WriteLine(a.GetType());   // "System.String[,]"

        // Create a 2-dim, 1-based array, with no elements in it
        a = Array.CreateInstance(typeof(String),
            new Int32[] { 0, 0 }, new Int32[] { 1, 1 });
        Console.WriteLine(a.GetType());   // "System.String[,]"
    }
```

每个 Console.WriteLine 旁边都有一条注释，指示输出。对于一维数组，从零开始的数组显示的类型名是 System.String[]，而从 1 开始的数组显示的类型名是 System.String[*]。* 表示 CLR 知道该数组不是从零开始的。注意，C# 不允许声明 String[*] 类型的变量，因此无法使用 C# 语法访问一维、非从零开始的数组。尽管可以调用 Array 的 GetValue 和 SetValue 方法来访问数组元素，但由于方法调用的开销，这种访问会很慢。

对于多维数组，从零开始和从 1 开始的数组都显示相同的类型名：System.String[,]。CLR 在运行时将所有多维数组都视为非从零开始。这可能会让你以为类型名应显示为 System.String[*,*]；然而，CLR 不对多维数组使用 *，因为它们始终会存在，而星号只会让大多数开发人员困惑。

访问一维、从零开始的数组的元素比访问非从零开始的一维数组或多维数组的元素稍快。原因有几个。第一，有特定的 IL 指令——例如 newarr、ldelem、ldelema、ldlen 和 stelem——用于操作一维、从零开始的数组，这些特殊的 IL 指令使 JIT 编译器生成优化后的代码。例如，JIT 编译器会生成假定数组从零开始的代码，这意味着访问元素时不必从指定索引中减去偏移量。第二，在常见情况下，JIT 编译器能够将索引范围检查代码提升到循环之外，使其只执行一次。例如，看看下面这段常见的代码：

```csharp
using System;

public static class Program {
    public static void Main() {
        Int32[] a = new int[5];
        for (Int32 index = 0; index < a.Length; index++) {
            // do something with a[index]
        }
    }
```

关于这段代码，首先要注意的是 for 循环测试表达式中对数组 Length 属性的调用。由于 Length 是属性，查询长度实际上代表一次方法调用。然而，JIT 编译器知道 Length 是 Array 类上的属性，并且 JIT 编译器实际上会生成只调用该属性一次、将结果存储到临时变量中的代码，并在循环的每次迭代中检查该临时变量。结果是 JIT 编译后的代码很快。事实上，一些开发人员低估了 JIT 编译器的能力，试图编写“聪明代码”来帮助 JIT 编译器。然而，你想到的任何聪明尝试几乎肯定会对性能产生负面影响，并使代码更难阅读，降低其可维护性。最好在上述代码中保留对数组 Length 属性的调用，而不是自己尝试将其缓存到局部变量中。

关于上述代码，第二点要注意的是，JIT 编译器知道 for 循环正在访问数组元素 0 到 Length – 1。因此，JIT 编译器生成的代码会在运行时测试所有数组访问是否都在数组的有效范围内。具体来说，JIT 编译器生成代码检查 if ( 0 >= a.GetLowerBound(0) && (Length - 1) <= a.GetUpperBound(0) )。该检查发生在循环之前。如果检查通过，JIT 编译器不会在循环内生成代码来验证每次数组访问是否在有效范围内。这使得循环内的数组访问非常快。

不幸的是，正如本章前面所提到的，访问非从零开始的一维数组或多维数组的元素，比访问一维、从零开始的数组慢得多。对于这些数组类型，JIT 编译器不会将索引检查提升到循环之外，因此每次数组访问都会验证指定的索引。此外，JIT 编译器还会添加代码，从指定索引中减去数组的下限，这也会降低代码速度，即使你使用的多维数组恰好从零开始。因此，如果性能对你很重要，可以考虑使用数组的数组（交错数组）而不是矩形数组。

C# 和 CLR 还允许使用不安全（不可验证）代码访问数组，这实际上是一种在访问数组时关闭索引边界检查的技术。注意，这种不安全的数组操作技术适用于元素类型为 SByte、Byte、Int16、UInt16、Int32、UInt32、Int64、UInt64、Char、Single、Double、Decimal、Boolean、枚举类型，或字段为上述任意类型的值类型结构的数组。

这是一个非常强大的功能，应极其谨慎地使用，因为它允许执行直接内存访问。如果这些内存访问超出数组边界，不会抛出异常；相反，你将破坏内存、违反类型安全，并可能打开安全漏洞！因此，包含不安全代码的程序集必须被授予完全信任，或者至少拥有已开启“跳过验证”的安全权限。
