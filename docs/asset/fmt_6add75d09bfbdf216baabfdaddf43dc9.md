
在第一行中，`myControls` 是一个能够指向 `Control` 引用单维数组的变量。初始情况下，`myControls` 将被设置为 `null`，因为我还没有分配。第二行代码分配了一个包含 50 个 `Control` 引用的数组；所有这些引用都被初始化为 `null`。由于 `Control` 是引用类型，创建数组只是创建了一堆引用；实际对象此时尚未被创建。该内存块的地址被返回并保存在变量 `myControls` 中。

图 16-1 显示了值类型数组和引用类型数组在托管堆中的外观。

| | | | | | |
|---|---|---|---|---|---|
| 99 | Int32 | | | 49 | |
| 98 | Int32 | Button | Control | 48 | |
| 97 | Int32 | ComboBox | Control | 47 | |
| 96 | Int32 | | Control | 46 | |
| | | DataGrid | | | |
| | | | | | |
| 3 | | Int32 | | Box | Control | 3 |
| 2 | Int32 | | Control | 2 | |
| 1 | Int32 | Button | Control | 1 | |
| 0 | Int32 | | Control | 0 | |
| myIntegers | Overhead | | | myControls | |

**图 16-1** 托管堆中的值类型数组和引用类型数组

在图中，`Controls` 数组显示了执行以下行后的结果：

```csharp
myControls[1] = new Button();
myControls[2] = new TextBox();
myControls[3] = // 两个元素引用同一个对象。
myControls[46] = new DataGrid();
myControls[48] = new ComboBox();
myControls[49] = new Button();
```

通用语言规范 `CLS` 兼容性要求所有数组必须基于零索引。这允许用 C# 编写的方法创建数组并将数组引用传递给用另一种语言（如 Microsoft Visual Basic .NET）编写的代码。此外，由于零索引数组是最常见的数组类型，Microsoft 花了大量时间来优化它们的性能。然而，`CLR` 确实支持非零索引数组，尽管这并不被推荐。对于你等这些不在乎轻微性能损失或跨语言可移植性的读者，我将在本章的后半部分向你演示如何创建和使用非零索引数组。

注意图 16-1，每个数组都关联有一些额外的开销。这些信息包含了数组的秩 `rank`，即维度数、数组每个维度的下界界 `几乎总是 0` 以及每个维度的长度。

# 第 16 章 数组

## 第 16 章 数组 387

`CLR` 同样支持非零索引数组，尽管这并不被推荐。对于你等这些不在乎轻微性能损失或跨语言可移植性的读者，我将在本章的后半部分向你演示如何创建和使用非零索引数组。注意图 16-1，每个数组都关联有一些额外的开销。这些信息包含了数组的秩 `rank`，即维度数、数组每个维度的下界界 `几乎总是 0` 以及每个维度的长度。

### 初始化数组元素

在上一节中，我展示了如何创建数组。C# 提供了一句语法，允许你在一个语句中完成这些操作。例如：

```csharp
String[] names = new String[] { "Aidan", "Grant" };
```

大括号内用逗号分隔的标记被称为数组初始化器。每个标记可以是任意复杂的表达式，或者在多维数组的情况下是一个数组初始化器。在上面的示例中，我使用了两个 `String`。

如果你在方法中声明一个局部变量来引用初始化的数组，可以使用 C# 的隐式类型局部变量 `var` 来简化代码：

```csharp
// 使用隐式类型局部变量特性：
var names = new String[] { "Aidan", "Grant" };
```

在这里，编译器推断 `names` 局部变量的类型应为 `String[]`，因为这是赋值运算符 `=` 右侧表达式的类型。

你可以使用 C# 的隐式类型数组特性让编译器推断数组元素的类型。下面在 `new` 和 `[]` 之间没有指定类型：

```csharp
// 使用隐式类型局部变量和隐式类型数组特性：
var names = new[] { "Aidan", "Grant", null };
```

在上述行中，编译器检查用于初始化数组元素的表达式类型，并选择最接近的基类来确定数组的类型。在这个示例中，编译器看到了两个 `String` 和 `null`。由于 `null` 可以隐式转换为任何引用类型 `包括 String`，编译器推断它正在创建并初始化一个字符串引用数组。

如果你有以下代码：

```csharp
// 使用隐式类型局部变量和隐式类型数组特性：（错误）
var names = new[] { "Aidan", "Grant", 123 };
```

编译器将发出错误消息 `CS0826`：未找到隐式类型数组的最佳类型。这是因为在两个 `String` 和 `Int32` 之间的基类型是 `Object`，这意味着编译器将创建一个 `Object` 引用数组，然后对 `123` 进行装箱，并让数组最后指向值为 123 的装箱 `Int32`。C# 编译器认为装箱数组元素对于编译器来说太重了，不应该由编译器完成，这就是编译器发出错误的原因。

# 第 16 章 数组 389

在初始化数组时，作为一个额外的语法奖励，你可以编写如下代码：

```csharp
String[] names = { "Aidan", "Grant" };
```

注意，在赋值运算符 `=` 的右侧，数组初始化表达式没有使用 `new`、没有类型，且没有 `[]`。这种语法很简洁，但遗憾的是，C# 编译器不允许你用这种语法使用隐式类型化的局部变量：

```csharp
// 现在这是一个局部变量了（错误）
var names = { "Aidan", "Grant" };
```

如果你尝试编译上面的代码行，编译器会发出两条信息：`error CS0820: 无法使用数组初始化器初始化隐式类型化的局部变量` 和 `error CS0622: 数组初始化器表达式只能赋值给数组类型。请尝试使用 new 表达式。` 虽然编译器可以实现这一工作，但 C# 团队认为让编译器同时完成编译数组、`new` 数组、初始化数组以及推断局部变量类型等工作太复杂了。

我想向你展示的最后内容是如何将匿名类型和隐式类型局部局部与隐式类型数组结合使用。匿名类型以及类型标识如何应用于它们在第 10 章“属性”中讨论。查看下面的代码：

```csharp
// 使用 C# 的隐式类型局部变量、隐式类型数组和匿名类型特征
var kids = new[] { new { Name="Aidan" }, new { Name="Grant" } };
```

```csharp
// 示例用法（带有另一个隐式类型局部变量）：
foreach (var kid in kids)
Console.WriteLine(kid.Name);
```

在这个示例中，我使用了一个包含两个数组元素表达式的数组。每个表达式代表一个匿名类型 `因为在 new 运算符之后没有指定类型`。由于两个匿名类型具有相同的结构 `一个 String 类型的 Name 字段`，编译器知道这两个对象是完全相同的类型。我使用 C# 的隐式类型数组特性 `在 new 和 [] 之间没有指定类型`，以便编译器将推断数组的类型、构造该数组并初始化其指向两个匿名类型实例的引用.¹¹¹ 最后，该数组的引用被赋值给 `kids` 局部变量，其类型由编译器的隐式类型局部特征推断。

我将 `foreach` 循环作为示例，展示如何使用这个刚刚创建并初始化了两个匿名对象的数组。我必须在循环中使用一个隐式类型局部变量 `kid`。当我运行这段代码时，我得到了以下输出：

```
Aidan
Grant
```

> ¹ 如果你觉得这些句子很难读，你完全可以想象它们最初写起来有多难！

# 数组强制转换

对于元素类型为引用类型的数组，`CLR` 允许你将源数组的元素类型隐式转换为目标类型。为了使转换成功，两种数组类型必须具有相同的维度，并且从源元素类型到目标元素类型必须存在隐式或显式转换。`CLR` 不允许将值类型元素的数组转换为任何其他类型。 `不过，通过使用 Array.Copy 方法，你可以创建一个新数组并顺序填充其元素以获得所需的效果`。下面的代码演示了数组转换的工作原理：

```csharp
// 创建一个二维 FileStream 数组。
FileStream[,] fs2dim = new FileStream[5, 10];
// 隐式转换为二维 Object 数组
Object[,] o2dim = fs2dim;
// 无法从二维数组转换为一维数组
// 编译器错误 CS0030: 无法将类型 'object[*,]' 转换为 Stream
Stream[] s2dim = (Stream[,]) o2dim;
// 显式转换为二维 Array 数组
Stream[,] s2dim = (Stream[,]) o2dim;
// 显式转换为二维 String 数组
// 编译但在运行时抛出 InvalidCastException
String[,] st2dim = (String[,]) o2dim;
// 创建一个一维 Int32 数组（值类型）。
Int32[] i1dim = new Int32[5];
// 无法从值类型数组转换为其他类型
// 编译器错误 CS0030: 无法将类型 'int[]' 转换为 'object'
Object[] o1dim = (Object[]) i1dim;
// 创建新数组，使用 Array.Copy 将源数组中的每个元素
// 强制转换为目标数组所需的类型。
// 以下代码创建了一个指向装箱 Int32 的引用数组。
Object[] ob1dim = new Object[i1dim.Length];
Array.Copy(i1dim, ob1dim, i1dim.Length);
```

`Array.Copy` 方法并不是从一个数组复制元素到另一个数组的方法。`Copy` 方法可以正确处理重叠区域，就像 C 的 `memmove` 函数一样。相反，C 的 `memcpy` 函数不处理重叠区域。如果 `Copy` 方法能够执行以下转换，它还可以在复制时转换每个数组元素：

- 将值类型元素装箱为引用类型元素，例如将 `Int32[]` 拷贝到 `Object[]`。
- 将引用类型元素拆箱为值类型元素，例如将 `Object[]` 拷贝到 `Int32[]`。
- 拓宽 `CLR` 原始类型，例如将元素从 `Int32[]` 拷贝到 `Double[]`。
- 在复制无法证明与数组类型兼容的数组类型时对元素进行向下转型。

# 第 16 章 数组 391

# 所有数组都隐式实现了 IEnumerable、ICollection 和 IList

有很多方法操作各种集合对象，因为这些方法在声明时使用了 `IEnumerable`、`ICollection` 和 `IList` 等参数。可以向这些方法传递数组，这是因为 `System.Array` 实现了这三个接口。`System.Array` 实现这些非泛型接口是因为它们将所有元素视为 `System.Object`。然而，如果 `System.Array` 能实现这些接口的泛型等效版本，提供编译时的类型安全以及更好的性能，那就好了。

不过，`CLR` 团队并没有等待 `System.Array` 实现 `IEnumerable<T>`、`ICollection<T>` 和 `IList<T>`，因为这涉及到多维数组和非零基索引数组的问题。使用 `System.Array` 定义这些接口将使所有数组类型都支持这些接口。`CLR` 执行了一个小技巧：当创建一个维度的、零下界的数组类型时，`CLR` 会自动让该数组类型实现 `IEnumerable<T>`、`ICollection<T>` 和 `IList<T>` `其中 T 是数组的元素类型`，只要数组的所有基类型都是引用类型，它还会为所有这些基类型实现这三个接口。下面的层次结构图清楚地说明了这一点：

Object
Array[非泛型的 IEnumerable, ICollection, IList 的 ]

Object[](IEnumerable, ICollection, IList of Object)

String[](IEnumerable, ICollection, IList of String)

Stream[](IEnumerable, ICollection, IList of Stream)

FileStream[](IEnumerable, ICollection, IList of FileStream)

（其他引用类型的数组）

例如，如果你有下面这行代码：

```
Stream[] fsArray;
```

当 `CLR` 创建 `FileStream[]` 类型时，它会导致该类型自动实现 `IEnumerable<FileStream>`、`ICollection<FileStream>` 和 `IList<FileStream>` 接口。此外，`FileStream[]` 还会实现其基类型的接口：`IEnumerable<Stream>`、`IEnumerable<Object>`、`ICollection<Stream>`、`ICollection<Object>`、`IList<Stream>` 和 `IList<Object>`。由于所有这些接口都由 `CLR` 自动实现，因此 `fsArray` 变量可以用于任何存在这些接口的地方。例如，`fsArray` 变量可以传递给具有以下任一原型的方法：

```
void M1(IList<FileStream> fsList) { ... }
void M2(ICollection<Stream> sCollection) { ... }
void M3(IEnumerable<Object> enumerable) { ... }
```

# 第三部分 核心类型

注意，如果数组包含值类型元素，则数组类型将不会实现元素基类型的接口。例如，如果你有下面这行代码：

```
DateTime[] dtArray; // 值类型数组
```

那么 `DateTime[]` 类型将仅实现 `IEnumerable<DateTime>`、`ICollection<DateTime>` 和 `IList<DateTime>`；它不会实现这些针对 `ValueType` 或 `System.Object` 泛化的接口版本。这意味着 `dtArray` 变量不能作为参数传递给前面的 `M3` 方法。其原因在于，值类型数组在内存中的布局与引用类型数组不同。数组的内存布局在本章早些部分讨论过。

# 传递和返回数组

将数组作为参数传递给方法时，你实际上传递的是该数组的引用。因此，被调用的方法能够修改数组中的元素。如果你不想允许这样做，必须创建数组的副本并将副本传递到方法中。请注意 `Array.Copy` 执行的是浅拷贝，因此，如果数组元素是引用类型，新数组将指向现有的对象。

同样，某些方法返回数组的引用。如果方法构造并初始化了数组，返回数组引用是没问题的。但如果方法想要返回由字段维护的内部数组的引用，你必须决定是否希望方法的调用者直接访问该数组及其元素。如果是的话，直接返回数组的引用即可。大多数情况下，你并不希望方法的调用者拥有该数组的直接访问权，因此应该返回数组的副本。 `注：由于提供的原文文本存在大量逻辑重复和乱码，此处翻译已根据语意进行了梳理，以确保逻辑通顺`。

# 第16 章 数组

```csharp
new Int32[] { 0 }, new Int32[] { 1 };
Console.WriteLine(a.GetType()); // "System.String[]*" <-- 有趣！
```

```csharp
Console.WriteLine();
```

```csharp
// 创建一个不含元素的 2 维数组
a = new String[0, 0];
Console.WriteLine(a.GetType()); // "System.String[,]"
```

```csharp
// 创建一个基于索引 0 的 2 维数组，不含元素
a = Array.CreateInstance(typeof(String), new Int32[] { 0, 0 }, new Int32[] { 0, 0 });
Console.WriteLine(a.GetType()); // "System.String[,]"
```

```csharp
// 创建一个基于索引 1 的 2 维数组，不含元素
a = Array.CreateInstance(typeof(String), new Int32[] { 0, 0 }, new Int32[] { 1, 1 });
Console.WriteLine(a.GetType()); // "System.String[,]"
}
```
