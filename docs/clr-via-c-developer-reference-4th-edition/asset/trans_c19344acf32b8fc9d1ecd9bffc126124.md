

除了匿名类型和 Tuple 类之外的说明

```cs
dynamic e = new System.Dynamic.ExpandoObject();
e.x = 6; // 添加 Int32 类型 'x' 属性值为 6
e.y = "Jeff"; // 添加 String 类型 'y' 属性值为 "Jeff"
e.z = null; // 添加 Object 类型 'z' 属性值为 null
```

```cs
// 查看所有属性及其对应值：
foreach (var v in (IDictionary<string, Object>)e))
    Console.WriteLine("Key={0}, Value={1}", v.Key, v.Value);
```

```cs
// 移除 'x' 属性及其值
var d = (IDictionary<string, Object>)e;
d.Remove("x");
```

## 参数化属性

在上一节中，属性的 get 访问器方法不接受参数。因此，我将这些称为无参数属性。这些属性易于理解，因为它们有访问字段的感觉。除了这些类字段属性外，编程语言还支持我所说的参数化属性，其 get 访问器接受一个或多个参数，而 setter 方法接受两个或更多参数。不同的编程语言以不同的方式公开这些属性。此外，语言使用不同的术语来描述它们：C# 将它们称为索引器（indexers），Visual Basic 称为默认属性（default properties）。在本节中，我将关注 C# 如何通过参数化属性公开其索引。

在 C# 中，参数化属性（索引器）使用类似于数组的语法公开。换句话说，你可以将索引器视为 C# 开发者重载 `[]` 运算符的一种。这是一个 BitArray 类的示例，它允许使用类数组语法来索引类实例维护的位集。

```cs
using System;

public sealed class BitArray {
    // 存储位的私有字节字节数组
    private Byte[] m_byteArray;
    private Int32 m_numBits;

    // 分配字节数组并将所有位置为 0 的构造函数
    public BitArray(Int32 numBits) {
        // 首先验证参数。
        if (numBits <= 0)
            throw ArgumentOutOfRangeException("numBits must be > 0");

        // 保存位数。
        m_numBits = numBits;

        // 为位数组分配字节。
        m_byteArray = new byte[(numBits + 7) / 8];
    }

    // 这是索引器（带参数的属性）。
    public Boolean this[Int32 bitPos] {
        // 这是索引器的 get 器方法。
        get {
            // 首先验证参数
            if ((bitPos < 0) || (bitPos >= m_numBits))
                throw ArgumentOutOfRangeException("bitPos");

            // 返回被索引位的状态。
            return (m_byteArray[bitPos / 8] & (1 << (bitPos % 8))) == 0;
        }
        // 这是索引器的 setter 器方法。
        set {
            if ((bitPos < 0) || (bitPos >= m_numBits))
                throw ArgumentOutOfRangeException("bitPos", bitPos.ToString());
            if (value) {
                // 开启被索引的位。
                m_byteArray[bitPos / 8] = (byte)(m_byteArray[bitPos / 8] | (1 << (bitPos % 8)));
            } else {
                // 关闭被索引的位。
                m_byteArray[bitPos / 8] = (byte)(m_byteArray[bitPos / 8] & ~(1 << (bitPos % 8)));
            }
        }
    }
}
```

BitArray 类的索引器非常简单。

```cs
// 分配一个可以容 14 位的 BitArray。
BitArray ba = new BitArray(14);

// 通过调用 setter 开启所有偶数位。
for (Int32 x = 0; x < 14; x++) {
    ba[x] = (x % 2 == 0);
}

// 通过调用 get 访问器显示所有位的状态。
for (Int32 x = 0; x < 14; x++) {
    Console.WriteLine("Bit " + x + " is " + (ba[x] ? "On" : "Off"));
}
```

在 BitArray 示例中，索引器接受一个 Int32 参数 bitPos。所有索引器都必须至少有一个参数，但也可以有更多。这些参数（以及返回类型）可以是任何类型（void 除外）。具有多个参数的索引器示例可以在 System.Drawing.Imaging.ColorMatrix 类中找到，该类位于 System.Drawing.dll 程序集中。

创建一个索引器来在关联数组中查找值是非常常见的。事实上，System.Collections.Generic.Dictionary 类型提供了一个索引器，它接受一个键并返回与之关联的值。与无参数属性不同，只要签名不同，类型就可以提供多个重载的索引器。

就像无参数属性的 setter 访问器方法一样，索引器的 setter 访问器方法也包含一个参数，在 C# 中称为 `value`。此参数表示“被索引元素”的新值。

CLR 不区分无参数属性和参数化属性；对于 CLR 来说，每个仅仅是类型内部定义的一对方法和一对元数据。如前所述，不同的编程语言需要不同的语法来使用参数化属性。C# 要求使用 `[]` 作为表示索引器的语法纯粹是 C# 团队做出的选择。这一选择意味着 C# 允许仅在对象实例上定义索引器。C# 没有提供允许开发者定义静态索引属性的语法，尽管 CLR 支持静态特定属性。

由于 CLR 对待参数属性的处理就像对待无参数属性一样，编译器将在生成的托管程序集中颁发以下项中的两个或三个：

- 代表参数化属性 get 访问器方法的方法。只有当你为属性定义了 get 访问器方法时才会发射。
- 代表参数化属性 setter 访问器方法的方法。只有当你为属性定义了 setter 访问器方法时才会发射。
- 托管程序集元数据中的属性定义，始终会被发射。没有特殊的参数化属性定义表，对于 CLR 来说，参数化属性只是属性。

对于之前定义的 BitArray 类，编译器编译索引器的方式就像原始源代码被写成如下形式：

```cs
public sealed class BitArray {

    // 这是索引器的 get 访问器方法。
    public Boolean getItem(Int32 bitPos) { /* ... */ }

    // 这是索引器的 setter 访问器方法。
    public void setItem(Int32 bitPos, Boolean value) { /* ... */ }
}
```

编译器通过获取索引器名称的 `get_` 和 `set_` 来自动生成方法名称。由于 C# 语法不允许开发者指定索引器名称，C# 编译器必须为访问器方法选择一个默认名称；它们选择了 `Item`。因此，编译器发射的方法名称是 `get_Item` 和 `set_Item`。

当你查看 .NET Framework 文档时，可以通过查找名为 `Item` 的属性来判断一个类型是否提供了索引器。例如，System.Collections.Generic.List 提供了一个名为 `Item` 的公共实例；这就是 List 的索引器。

当你在 C# 中编程时，你看不到 `Item` 名称，你通常不在意编译器为你准备这个名称。但是，如果你在为其他语言设计索引器，你可能想通过给索引器提供 get 和 setter 方法来更改默认名称 `Item`。C# 允许通过使用 System.Runtime.CompilerServices.IndexerName 自定义属性重命名这些方法。以下代码演示了如何这样做。

```cs
using System;
using System.Runtime.CompilerServices;

public sealed class BitArray{

    [IndexerName("Bit")]
    public Boolean this[Int32 bitPos] {
        // 这里定义了至少一个访问器方法
    }
}
```

现在编译器将发射 `get_Bit` 和 `set_Bit` 而不是 `get_Item` 和 `set_Item`。编译时，C# 编译器看到 `IndexerName` 属性，这告诉编译器如何命名方法和属性元数据；该属性不会发射到程序集的元数据中。

这里有一些演示如何访问此 C# 索引器的 Visual Basic。

- 构建 BitArray 类型的实例。
Dim ba as New BitArray(10)
- Visual Basic 使用 代替 `[]` 指定数组元素。
  Console.WriteLine(ba(2)) - 显示 True 或 False
- Visual Basic 也允许通过其名称访问索引器。
  Console.WriteLine(ba.Bit(2)) - 显示与上一相同

在 C# 中，单个类型可以定义多个索引器，只要这些索引器允许不同的参数集。在其他编程语言中，每个可以有不同的名称。C# 不允许你这样做，因为它的语法没有通过名称引用索引器；编译器将不知道你指的是哪个索引器。尝试编译以下 C 源代码会导致

