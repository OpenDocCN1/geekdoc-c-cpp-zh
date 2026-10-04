

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

接下来每个 Console.WriteLine 都是指示输出的注释。对于多维数组，
基于0索引的数组显示的类型名称为 System.String[,]，而基于1索引的数组显示的
类型名称为 System.String[*]。*星号 表示 CLR 知晓这不是基于0索引的。注意，
C# 不允许你声明类型为 String[*] 的变量，因此无法使用 C# 语法来访问
单维的、非0索引的数组。虽然你可以调用 Array.GetValue 和 SetValue 来访问数组
的元素，但这种访问将产生方法调用的开销。

对于多维数组，基于0索引和基于1索引的数组在运行时都显示相同的类型名称：
System.String[,]。这会让你认为类型名称应该显示为
System.String[*,*]；然而，CLR 不在多维数组中使用 * 号，因为它们总是会出现的，
而且星号只会混淆开发者。

访问单维基于0索引数组的元素比访问非0索引的单维数组或多维数组的
元素要快一点。这有几个原因。首先，有一些 IL 指令——例如 newlem, ldelem, ldelem,
lddlem 和 stelem——JIT 编译器使用这些指令来优化代码。例如，JIT
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

关于这段代码首先要注意的一点是在循环测试表达式中对数组 Length 属性的调用。
由于 Length 是一个属性，查询长度实际上代表了一个方法调用。然而，JIT 编译器知道 Length 是 Array 类上的一个属性，
JIT 编译器实际上会生成调用它的代码，并将结果存储在临时变量中，
该变量将在循环的每次迭代中进行检查。结果是 JIT 后的代码非常快。事实上，有些开发者低估了 JIT 编译器的能力，并尝试编写“聪明”的代码来试图帮助 JIT 编译器。
然而，你想出的任何尝试几乎肯定会对性能产生负面影响，并让你的代码更难读，降低其可维护性。要么我们在代码中省略对数组 Length 属性的调用，
而不是尝试将其缓存在局部变量中。

关于前面的代码要注意的第二点是，JIT 编译器知道对于
循环 数组元素 - 1。所以 JIT 编译器产生代码来检查所有的
访问是否在数组的有效范围内。具体来说，JIT 编译器产生代码检查
(i >= 0) && ((Length - a.LowerBound(0)) - 1) < a.UpperBound(0))。这种检查发生在循环之前。JIT 编译器会生成代码来验证每次访问是有效的。这允许循环内的访问是快速的。
遗憾的是，如本文提到的，访问非0索引的单维数组
或多维数组比基于0索引的单维数组慢得多。对于这些类型，JIT 编译器不会将索引检查提升到循环外，所以 JIT 编译器添加代码从索引中减去数组的边界，这减慢了代码，即使你使用的是基于0索引的数组。如果你关心性能，你可能想
使用交错数组（jagged array）而不是矩形数组。C# 和 CLR 允许你通过不安全的（非验证的）代码访问数组，这实际上允许你在访问数组时关闭索引检查。这种技术适用于元素为
SByte, Byte, Int16, UInt16, Int32, UInt32, Int64, UInt64, Char, Double, Boolean
枚举类型或值类型的数组。这是一个强大的功能，允许你执行直接内存访问。如果这些内存访问超出了数组边界，不会抛出异常；你会损坏内存，违反类型安全并可能留下安全漏洞！由于由于，包含不安全代码的程序集必须授予完全信任或至少跳过验证的权限。下面的 C# 代码演示了访问二维数组的三种技术（安全的、交错的是不安全的）。

```csharp
using System;
using System.Diagnostics;

public static class Program {
    private const Int32 numElements = 10000;

    public static void Main() {
    // 声明一个二维数组
    Int32[,] aDim = new Int32[numElements, numElements];

    // 将二维数组声明为交错数组（向量的向量）
    Int32[][] jagged = new Int32[numElements][];
    for (Int32 x = 0; x < numElements; x++)
        jagged[x] = new Int32[numElements];

    // 1: 使用通常的安全技术访问数组的所有元素
    SafeDimArrayAccess(aDim);

    // 2: 使用交错技术访问数组的所有元素
    SafeJaggedArrayAccess(jagged);

    // 3: 使用不安全的技术访问数组的所有元素
    UnsafeDimArrayAccess(aDim);
}}

    private static Int32 SafeDimArrayAccess(Int32[,] a) {
        Int32 sum = 0;
        for (Int32 x = 0; x < numElements; x++) {
            for (Int32 y = 0; y < numElements; y++) {
                sum += a[x, y];
            }
        }
        return sum;
    }

    private static Int32 SafeJaggedArrayAccess(Int32[][] a) {
        Int32 sum = 0;
        for (Int32 x = 0; x < numElements; x++) {
            for (Int32 y = 0; y < numElements; y++) {
                sum += a[x][y];
            }
        }
        return sum;
    }

    private static unsafe Int32 UnsafeDimArrayAccess(Int32[,] a) {
        Int32 sum = 0;
        fixed (Int32* pi = a) {
            for (Int32 x = 0; x < numElements; x++) {
                Int32* baseOfDim = pi + x * numElements;
                for (Int32 y = 0; y < numElements; y++) {
                    sum += pi[baseOfDim + y];
                }
            }
        }
        return sum;
    }
```

UnsafeDimArrayAccess 方法标记了 unsafe 修饰符，这是使用 C# 的 fixed 语句所要求的。要编译此代码，你需要在调用 C# 编译器时指定 /unsafe 选项，或者在 Visual Studio 项目属性面板的生成 选项卡上勾选“允许不安全代码”复选框。

显然，不安全技术有你自己的代码使用的时机和场合，而且使用这种技术有三个严重的缺点：

- 操作不安全数组元素的代码比使用其他技术操作元素的代码更难读和写，因为你正在使用 C# 的 fixed 语句并执行内存地址计算。

- 如果你在计算中出错，你将访问到不属于数组的内存。这可能导致计算错误、内存损坏、类型安全违例以及潜在的安全漏洞。

- 由于潜在的问题，CLR 禁止不安全代码在低安全性环境（如 Microsoft Silverlight）中运行。

# 不安全数组访问与固定大小数组

不安全数组访问是一个强大的功能，因为它允许你访问：

- 位于堆上的托管数组对象的内部元素（如前节所示），

- 位于非托管堆上的数组元素。第14章“字符、字符串与文本处理”中的 SecureString 示例演示使用不安全数组访问从 System.Runtime.InteropServices.Marshal 类的 StringToStringMemUnicode 方法返回的数组。

- 位于线程栈上的数组元素。

