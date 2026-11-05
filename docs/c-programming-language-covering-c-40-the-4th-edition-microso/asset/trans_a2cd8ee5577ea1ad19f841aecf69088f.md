
## 12. 数组

数组是一种数据结构，它包含若干通过计算得到的索引来访问的变量。数组中包含的变量也称为数组的元素，它们都具有相同的类型，这种类型称为数组的元素类型。

数组具有一个秩，它确定与每个数组元素关联的索引数目。数组的秩也称为数组的维度。秩为 1 的数组称为*一维数组*。秩大于 1 的数组称为*多维数组*。特定大小的多维数组通常称为二维数组、三维数组等。

数组的每个维度都有一个关联的长度，它是一个大于或等于零的整数。维度长度不是数组类型的一部分，而是在运行时创建数组类型的实例时确立。维度的长度确定该维度的有效索引范围：对于长度为 *N* 的维度，索引范围可以从 0 到 *N* - 1（含）。数组中元素的总数是数组中每个维度长度的乘积。如果数组的一个或多个维度的长度为零，则称该数组为空。

数组的元素类型可以是任何类型，包括数组类型。

### 12.1 数组类型

数组类型写作一个*非数组类型*，后跟一个或多个*秩说明符*：

```
    array-type:
        non-array-type rank-specifiers

    non-array-type:
        type

    rank-specifiers:
        rank-specifier
        rank-specifiers rank-specifier
```

```text
rank-specifier:
    [   dim-separators_opt   ]

dim-separators:
    ,
    dim-separators ,
```

非数组类型是任何本身不是数组类型的类型。

数组类型的秩由该数组类型中最左边的秩说明符给出。秩说明符指示该数组是一个秩为 1 加上该秩说明符中“,”标记数的数组。

数组类型的元素类型是删除最左边秩说明符后得到的类型：

- 形式为 T[R] 的数组类型是秩为 R、非数组元素类型为 T 的数组。
- 形式为 T[R][R]...[R] 的数组类型是秩为 R、元素类型为 T[R]...[R] 的数组。

实际上，秩说明符是在最终的非数组元素类型之前从左到右读取的。类型 int[][,][,] 是一个一维数组，其元素是 int 的二维数组的三维数组。

> **ERIC LIPPERT** 数组的数组的秩说明符以“反向”读取这一事实常常令人困惑。实际上，这种方案有一个很好的性质：索引操作与声明以相同顺序进行；你会按 `arr[a][b,c,d][e,f]` 那样索引那个复杂数组。

在运行时，数组类型的值可以是 null，也可以是对该数组类型实例的引用。

### 12.1.1 System.Array 类型

System.Array 类型是所有数组类型的抽象基类型。存在从任何数组类型到 System.Array 的隐式引用转换（§6.1.6），以及从 System.Array 到任何数组类型的显式引用转换（§6.2.4）。注意，System.Array 本身不是数组类型。相反，它是所有数组类型都派生自的类类型。

在运行时，System.Array 类型的值可以是 null，也可以是对任何数组类型实例的引用。

### 12.1.2 数组与泛型 IList 接口

一维数组 T[] 实现接口 System.Collections.Generic.IList<T>（简称 IList<T>）及其基接口。因此，存在从 T[] 到 IList<T> 及其基接口的隐式转换。此外，如果存在从 S 到 T 的隐式引用转换，那么 S[] 实现 IList<T>，并且存在从 S[] 到 IList<T> 及其基接口的隐式引用转换（§6.1.6）。如果存在从 S 到 T 的显式引用转换，那么存在从 S[] 到 IList<T> 及其基接口的显式引用转换（§6.2.4）。例如：

```csharp
using System.Collections.Generic;

class Test
{
    static void Main() {
        string[] sa = new string[5];
        object[] oa1 = new object[5];
        object[] oa2 = sa;

        IList<string> lst1 = sa;        // Okay
        IList<string> lst2 = oa1;       // Error: cast needed
        IList<object> lst3 = sa;        // Okay
        IList<object> lst4 = oa1;       // Okay

        IList<string> lst5 = (IList<string>)oa1;  // Exception
        IList<string> lst6 = (IList<string>)oa2;  // Okay
    }
}
```

赋值 lst2 = oa1 会产生编译时错误，因为从 object[] 到 IList<string> 的转换是显式转换，而不是隐式转换。强制转换 (IList<string>) oa1 将在运行时引发异常，因为 oa1 引用的是 object[] 而不是 string[]。然而，强制转换 (IList<string>)oa2 不会引发异常，因为 oa2 引用的是 string[]。

每当存在从 S[] 到 IList<T> 的隐式或显式引用转换时，也存在从 IList<T> 及其基接口到 S[] 的显式引用转换（§6.2.4）。

当数组类型 S[] 实现 IList<T> 时，所实现接口的某些成员可能会引发异常。该接口实现的确切行为超出了本规范的范围。

> **ERIC LIPPERT** 考虑一个反事实世界是很有趣的：CLR 在版本 1 中就有泛型类型。在那个反事实世界中，可能会有泛型数组类型 Array<>、Array2<> 等。在那个世界中，复杂数组类型的声明变得更加清晰：Array2<int,int> 是一个一维数组，其中每个元素都是整数的二维数组。

> **BILL WAGNER** 数组 T[] 通过为某些方法抛出异常来实现 IList<T>，这是现实世界中令人烦恼的问题之一，对此没有好的解决方案。IList<T> 具有添加或移除元素的方法。然而，数组具有固定大小，无法支持其中一些方法。即便如此，你还是想使用 IList<T> 接口中存在的对元素的随机访问。

## 12.2 数组创建

数组实例由数组创建表达式（§7.6.10.4）创建，或由包含数组初始值设定项（§12.6）的字段或局部变量声明创建。

创建数组实例时，会确立秩和每个维度的长度，然后它们在实例的整个生存期内保持不变。换句话说，不可能更改现有数组实例的秩，也不可能调整其维度的大小。

数组实例始终属于数组类型。System.Array 类型是抽象类型，不能实例化。

由数组创建表达式创建的数组的元素始终初始化为其默认值（§5.2）。

## 12.3 数组元素访问

数组元素使用形式为 A[I₁, I₂, …, Iₙ] 的元素访问表达式（§7.6.6.1）进行访问，其中 A 是数组类型的表达式，每个 Iₓ 是类型为 int、uint、long 或 ulong 的表达式，或者可以隐式转换为这些类型中的一种或多种。数组元素访问的结果是一个变量——即由索引选定的数组元素。

可以使用 foreach 语句（§8.8.4）枚举数组的元素。

## 12.4 数组成员

每个数组类型都继承 System.Array 类型声明的成员。

## 12.5 数组协变

对于任意两个引用类型 A 和 B，如果存在从 A 到 B 的隐式引用转换（§6.1.6）或显式引用转换（§6.2.4），那么也存在从数组类型 A[R] 到数组类型 B[R] 的相同引用转换，其中 R 是任意给定的秩说明符（但对两个数组类型相同）。这种关系称为数组协变。特别地，数组协变意味着数组类型 A[R] 的值实际上可以是对数组类型 B[R] 实例的引用，前提是存在从 B 到 A 的隐式引用转换。

由于数组协变，对引用类型数组元素的赋值包括运行时检查，以确保要赋给数组元素的值实际上是允许的类型（§7.17.1）。例如：

```csharp
class Test
{
    static void Fill(object[] array, int index, int count, object value) {
        for (int i = index; i < index + count; i++)
            array[i] = value;
    }

    static void Main() {
        string[] strings = new string[100];
        Fill(strings, 0, 100, "Undefined");
        Fill(strings, 0, 10, null);
        Fill(strings, 90, 10, 0);
    }
}
```

Fill 方法中对 array[i] 的赋值隐式包含运行时检查，以确保 value 引用的对象要么为 null，要么是与 array 的实际元素类型兼容的实例。在 Main 中，前两次 Fill 调用成功，但第三次调用在执行对 array[i] 的第一次赋值时导致引发 System.ArrayTypeMismatchException。发生该异常是因为装箱的 int 不能存储在 string 数组中。

> **ERIC LIPPERT** 这是我提名的 C#“最差特性”。它允许赋值在运行时失败，而源代码中没有任何表明这种失败可能发生的指示。它给极其常见的代码施加性能成本，以使罕见场景快速执行；安全地访问非密封引用类型的数组比协变数组转换常见得多。我更喜欢已添加到 IEnumerable<T> 的类型安全协变。

