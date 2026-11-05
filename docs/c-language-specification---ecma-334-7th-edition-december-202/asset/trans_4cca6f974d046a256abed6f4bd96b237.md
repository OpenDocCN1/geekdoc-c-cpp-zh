
## 17. 数组

### 17.1 通用

数组是一种数据结构，其中包含若干通过计算得到的索引进行访问的变量。包含在数组中的变量，也称为数组的元素，全部为同一类型，该类型称为数组的元素类型。

数组具有一个秩，决定了与每个数组元素关联的索引数量。数组的秩也称为数组的维度。秩为一的数组称为单维数组。秩大于一的数组称为多维数组。特定大小的多维数组通常被称为二维数组、三维数组，等等。数组的每个维度都有一个相关联的长度，该长度为大于或等于零的整数。维度的长度不是数组类型的一部分，而是当数组类型的实例在运行时创建时确定的。维度的长度决定了该维度的索引有效范围：对于长度为 N 的维度，索引的范围可以从 0 到 N - 1 包含。数组中的元素总数是数组中各维度长度的乘积。如果数组的一个或多个维度的长度为零，则该数组称为空数组。

数组的元素类型本身也可以是数组类型 (§17.2.1)。这种数组的数组与多维数组不同，可用于表示“锯齿数组”。

示例：

```csharp
int[][] pascals =
{
    new int[] {1},
    new int[] {1, 1},
    new int[] {1, 2, 1},
    new int[] {1, 3, 3, 1}
};
```

end example

每个数组类型都是引用类型 (§8.2)。数组的元素类型可以是任何类型，包括值类型和数组类型。

### 17.2 数组类型

#### 17.2.1 通用

数组类型的语法生成式在 §8.2.1 中给出。

数组类型写成 `non_array_type` 后跟一个或多个 `rank_specifier`。

`non_array_type` 是任何本身不是 `array_type` 的类型。

数组类型的秩由 `array_type` 中最左边的 `rank_specifier` 给出：`rank_specifier` 表示该数组的秩为一加上 `rank_specifier` 中 `,` 标记的数量。

数组类型的元素类型是通过删除最左边的 `rank_specifier` 得到的类型：

- 形式为 `T[R]` 的数组类型是秩为 R 且元素类型为非数组类型 T 的数组。
- 形式为 `T[R][R1]...[Rx]` 的数组类型是秩为 R 且元素类型为 `T[R1]...[Rx]` 的数组。

实际上，`rank_specifier` 是从左到右读取，位于最终的非数组元素类型之前。

示例：类型 `T[][,,][,]` 中的类型是 int 的二维数组的三维数组的单维数组。 end example

在运行时，数组类型的值可以为 null 或对该数组类型实例的引用。

注意：根据 §17.6 的规则，该值也可能是对协变数组类型的引用。 end note

#### 17.2.2 System.Array 类型

类型 System.Array 是所有数组类型的抽象基类型。从任何数组类型到 System.Array 以及 System.Array 实现的任何接口类型都存在隐式引用转换 (§10.2.8)。从 System.Array 以及 System.Array 实现的任何接口类型到任何数组类型都存在显式引用转换 (§10.3.5)。System.Array 本身不是 `array_type`。相反，它是一个 `class_type`，所有 `array_type` 均派生自它。

在运行时，System.Array 类型的值可以为 null 或对任何数组类型实例的引用。

#### 17.2.3 数组与通用集合接口

单维数组 `T[]` 实现接口 `System.Collections.Generic.IList<T>`（简称为 `IList<T>`）及其基接口。因此，从 `T[]` 到 `IList<T>` 及其基接口存在隐式转换。此外，如果从 S 到 T 存在隐式引用转换，则 `S[]` 实现 `IList<T>`，并且从 `S[]` 到 `IList<T>` 及其基接口存在隐式引用转换 (§10.2.8)。如果从 S 到 T 存在显式引用转换，则从 `S[]` 到 `IList<T>` 及其基接口存在显式引用转换 (§10.3.5)。

同样，单维数组 `T[]` 也实现接口 `System.Collections.Generic.IReadOnlyList<T>`（简称为 `IReadOnlyList<T>`）及其基接口。因此，从 `T[]` 到 `IReadOnlyList<T>` 及其基接口存在隐式转换。此外，如果从 S 到 T 存在隐式引用转换，则 `S[]` 实现 `IReadOnlyList<T>`，并且从 `S[]` 到 `IReadOnlyList<T>` 及其基接口存在隐式引用转换 (§10.2.8)。如果从 S 到 T 存在显式引用转换，则从 `S[]` 到 `IReadOnlyList<T>` 及其基接口存在显式引用转换 (§10.3.5)。

*示例：* 例如：

```csharp
class Test
{
    static void Main()
    {
        string[] sa = new string[5];
        object[] oa1 = new object[5];
        object[] oa2 = sa;

        IList<string> lst1 = sa;  // Ok
        IList<string> lst2 = oa1; // Error, cast needed
        IList<object> lst3 = sa;  // Ok
        IList<object> lst4 = oa1; // Ok

        IList<string> lst5 = (IList<string>)oa1; // Exception
        IList<string> lst6 = (IList<string>)oa2; // Ok

        IReadOnlyList<string> lst7 = sa; // Ok
        IReadOnlyList<string> lst8 = oa1; // Error, cast needed
        IReadOnlyList<object> lst9 = sa; // Ok
        IReadOnlyList<object> lst10 = oa1; // Ok
        IReadOnlyList<string> lst11 = (IReadOnlyList<string>)oa1; // Exception
        IReadOnlyList<string> lst12 = (IReadOnlyList<string>)oa2; // Ok
    }
}
```

赋值 `lst2 = oa1` 会生成编译时错误，因为从 `object[]` 到 `IList<string>` 的转换是显式转换，而不是隐式转换。强制转换 `(IList<string>)oa1` 会在运行时抛出异常，因为 `oa1` 引用的是 `object[]` 而不是 `string[]`。然而强制转换 `(IList<string>)oa2` 不会抛出异常，因为 `oa2` 引用的是 `string[]`。

*示例结束*

每当从 `S[]` 到 `IList<T>` 存在隐式或显式引用转换时，从 `IList<T>` 及其基接口到 `S[]` 也存在显式引用转换 (§10.3.5)。

当数组类型 `S[]` 实现 `IList<T>` 时，已实现接口的某些成员可能会抛出异常。接口实现的精确行为超出了本规范的范围。

### 17.3 数组创建

数组实例由 `array_creation_expressions` (§12.8.16.5) 创建，或由包含 `array_initializer` (§17.7) 的字段或局部变量声明创建。

数组实例也可以在评估涉及参数数组的参数列表时隐式创建 (§15.6.2.6)。

当数组实例创建时，每个维度的秩和长度被确定，并且在实例整个生命周期内保持不变。换句话说，不可能更改现有数组实例的秩，也不可能调整其维度的大小。

数组实例始终为数组类型。System.Array 类型是抽象类型，不能实例化。

由 `array_creation_expressions` 创建的数组的元素始终初始化为其默认值 (§9.3)。

### 17.4 数组元素访问

数组元素使用形式为 `A[I1, I2, ..., Ix]` 的 `element_access` 表达式 (§12.8.11.2) 进行访问，其中 A 是数组类型的表达式，每个 `I_i` 是类型为 int、uint、long、ulong 的表达式，或可以隐式转换为其中一种或多种类型。数组元素访问的结果是一个变量，即由索引选定的数组元素。

数组的元素可以使用 foreach 语句 (§13.9.5) 进行枚举。

### 17.5 数组成员

每个数组类型都继承 System.Array 类型声明的成员。

### 17.6 数组协变

对于任意两个 `reference_type` A 和 B，如果从 A 到 B 存在隐式引用转换 (§10.2.8) 或显式引用转换 (§10.3.5)，则从数组类型 `A[R]` 到数组类型 `B[R]` 也存在相同的引用转换，其中 R 是任意给定的 `rank_specifier`（但对两个数组类型相同）。这种关系称为数组协变。

数组协变特别意味着，数组类型 `A[R]` 的值实际上可能是数组类型 `B[R]` 的实例的引用，前提是从 B 到 A 存在隐式引用转换。

由于数组协变，对引用类型数组元素的赋值包括运行时检查，以确保分配给数组元素的值实际上是允许的类型 (§12.21.2)。

*示例：*

```csharp
class Test
{
    static void Fill(object[] array, int index, int count, object value)
    {
        for (int i = index; i < index + count; i++)
        {
            array[i] = value;
        }
    }

    static void Main()
    {
        string[] strings = new string[100];
        Fill(strings, 0, 100, "Undefined");
        Fill(strings, 0, 10, null);
        Fill(strings, 90, 10, 0);
    }
}
```

Fill 方法中对 `array[i]` 的赋值隐式包含运行时检查，以确保 value 要么为空引用，要么是对与数组实际元素类型兼容的对象类型的引用。在 Main 中，Fill 的前两次调用成功，但第三次调用在执行对 `array[i]` 的第一次赋值时导致抛出 `System.ArrayTypeMismatchException`。该异常发生是因为装箱的 int 不能存储在字符串数组中。

*示例结束*

数组协变特别不扩展到 `value_type` 的数组。例如，不存在允许将 `int[]` 视为 `object[]` 的转换。

### 17.7 数组初始化器

数组初始化器可以在字段声明 (§15.5)、局部变量声明 (§13.6.2) 和数组创建表达式 (§12.8.16.5) 中指定：
