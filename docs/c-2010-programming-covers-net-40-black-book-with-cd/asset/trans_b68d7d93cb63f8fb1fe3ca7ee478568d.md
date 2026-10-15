
SortedList 对象始终根据其键的值进行排序，并且没有单独的方法来根据其中存储的值对集合进行排序。

SortedList 类的类层次结构如下：

```
System.Object
System.Collections.SortedList
```

表 32.5 列出了 SortedList 类的重要属性：

### 表 32.5：SortedList 类的著名属性

| 属性 | 描述 |
|---|---|
| Capacity | 检索或设置 SortedList 对象可以容纳的元素数量 |
| Count | 检索 SortedList 对象中存在的元素数量 |
| IsFixedSize | 检索一个值，指定 SortedList 对象是否具有固定大小 |
| IsReadOnly | 检索一个值，指定 SortedList 对象是否为只读 |
| IsSynchronized | 检索一个值，指定对 SortedList 对象的访问是否同步 |
| Item | 检索或设置 SortedList 对象中与特定键关联的值 |
| Keys | 检索 SortedList 对象中的键集合 |
| SyncRoot | 检索一个用于同步访问 SortedList 对象的对象 |
| Values | 检索 SortedList 对象中的值集合 |

表 32.6 列出了 SortedList 类的重要方法：

### 表 32.6：SortedList 类的著名方法

| 方法 | 描述 |
|---|---|
| Add() | 将具有指定键和值的项添加到 SortedList 对象中 |
| Clear() | 从 SortedList 对象中移除所有项 |
| Clone() | 创建 SortedList 对象的副本 |
| Contains() | 如果指定的项在 SortedList 对象中，则返回 true |
| ContainsKey() | 如果指定的键在 SortedList 对象中，则返回 true |
| ContainsValue() | 如果指定的值在 SortedList 对象中，则返回 true |
| CopyTo() | 将 SortedList 对象中的项复制到指定索引处的一维数组中 |
| GetByIndex() | 检索 SortedList 对象中指定索引处的值 |
| GetEnumerator() | 返回遍历 SortedList 对象的 IDictionaryEnumerator |
| GetKey() | 检索 SortedList 对象中指定索引处的键 |
| GetKeyList() | 从 SortedList 对象中检索键列表 |
| GetValueList() | 从 SortedList 对象中检索值 |
| IndexOfKey() | 返回指定键在 SortedList 对象中的从零开始的索引 |
| IndexOfValue() | 返回指定值在 SortedList 对象中首次出现的从零开始的索引 |
| Remove() | 从 SortedList 对象中移除具有指定键的项 |
| RemoveAt() | 移除 SortedList 对象中指定索引处的项 |
| SetByIndex() | 替换 SortedList 对象中指定索引处的值 |
| TrimToSize() | 将 SortedList 对象的容量（用于容纳项）设置为 SortedList 对象中实际存储的项数 |

## Stack 类

Stack 类遵循后进先出（LIFO）顺序。最后添加到 Stack 对象的项将最先被读取。Stack 对象是一个 LIFO 容器。当您向 Stack 对象添加项时，称为将项推入（push）Stack 对象；当您从 Stack 对象移除项时，称为从 Stack 对象弹出（pop）该项。这些操作被称为 push 和 pop，因为 push 添加项，而 pop 移除项。

![](img/e073a4882197be4ab61103cbe0bcb394_1518_0.png)

Stack 类的类层次结构如下：

```
System.Object
System.Collections.Stack
```

### 表 32.7：Stack 类的著名属性

| 属性 | 描述 |
|---|---|
| Count | 检索 Stack 对象中存在的元素数量 |
| IsSynchronized | 检索一个值，指定对 Stack 对象的访问是否同步 |
| SyncRoot | 检索一个可用于同步访问 Stack 对象的对象 |

### 表 32.8：Stack 类的著名方法

| 方法 | 描述 |
|---|---|
| Clear() | 从 Stack 对象中移除所有项 |
| Clone() | 创建 Stack 对象的副本 |
| Contains() | 如果项在 Stack 对象中，则返回 true |
| CopyTo() | 将 Stack 对象中的项复制到指定索引处的一维数组中 |
| GetEnumerator() | 返回 Stack 对象的 IEnumerator 对象 |
| Peek() | 返回 Stack 对象顶部的项，但不将其移除 |
| Pop() | 移除并返回 Stack 对象顶部的项 |

## BitArray 类

BitArray 类用于管理使用值 1 和 0 的二进制表示数组，其中 1 代表 True，0 代表 False。BitArray 对象是可调整大小的，这在您事先不知道位数时非常有用。您可以使用整数索引从 BitArray 集合类中访问项。此集合中使用的索引从零开始。

BitArray 类的类层次结构如下：

```
System.Object
System.Collections.BitArray
```

表 32.11 列出了 BitArray 类的重要属性：

### 表 32.11：BitArray 类的著名属性

| 属性 | 描述 |
|---|---|
| Count | 检索 BitArray 对象中包含的元素数量 |
| IsReadOnly | 检索一个值，指定 BitArray 对象是否为只读 |
| IsSynchronized | 检索一个值，指定对 BitArray 对象的访问是否同步 |
| Item | 检索或设置 BitArray 对象中特定位置处的位值 |
| Length | 检索或设置 BitArray 对象中的元素数量 |
| SyncRoot | 检索一个可用于同步访问 BitArray 对象的对象 |

表 32.12 列出了 BitArray 类的重要方法：

### 表 32.12：BitArray 类的著名方法

| 方法 | 描述 |
|---|---|
| And() | 对当前 BitArray 对象中的项与指定 BitArray 对象中的对应项执行按位 AND 运算。 |
| Clone() | 创建 BitArray 对象的副本。 |
| CopyTo() | 将 BitArray 对象中的项复制到指定索引处的一维数组中。 |
| Get() | 检索 BitArray 对象中指定索引处的位值。 |
| GetEnumerator() | 返回遍历 BitArray 对象的枚举器。 |
| Not() | 反转当前 BitArray 对象中的所有位值，以便设置为 true 的元素变为 false，反之亦然。 |
| Or() | 对当前 BitArray 对象中的项与指定 BitArray 对象中的对应项执行按位 OR 运算。如果一个或两个操作数为 true，则返回 true；如果两个操作数均为 false，则返回 false。 |
| Set() | 将 BitArray 对象中指定位置的位设置为指定值。 |
| SetAll() | 将 BitArray 对象中的所有位设置为指定值。 |
| Xor() | 对当前 BitArray 对象中的项与指定 BitArray 对象中的对应项执行按位异或运算。如果其中一个操作数为 true，则返回 true；如果两个操作数具有相同的布尔值，则返回 false。 |

> 注意
> 要执行按位异或（Xor）运算，两个 BitArray 对象的长度应相同。

现在让我们来了解 C# 中的泛型概念。

## 理解泛型

泛型可以定义为一种技术，通过该技术，您可以将类或方法中一个或多个编程元素的类型规范延迟到使用该类或方法之时。在泛型中，不是指定参数的数据类型，而是定义标签，这些标签以后可以被使用泛型方法或类时指定的数据类型所替换。让我们通过以下代码片段来理解泛型的概念：

```
public class MyGenericCollection<Tp>
{
  private Tp[] Arr;
  public MyGenericCollection(int Size) {
    Arr = new Tp[Size + 1];
  }
  public Tp GetItems(int index) {
    return Arr[index];
  }
  public void SetItems(int index, Tp value) {
    Arr[index] = value;
  }
}
```

在前面的代码片段中，我们声明了一个名为 MyGenericCollection 的类，其中包含一个名为 Tp 的标签。在后面的定义中，我们还声明了一个 Tp 类型的数组。在下面的代码片段中，我们为标签 Tp 指定了一个整数，该整数在运行时将类定义中所有出现的 Tp 替换为整数：

```
MyGenericCollection<int> MGColInt;
```

当 Tp 被替换为整数后，MyGenericCollection 类现在使 Arr 数组成为整数类型。您还可以定义本质上是泛型的方法，如下面的代码片段所示：

```
public string Sum<T>(T val1, T val2)
{
  ...
}
```

在前面的代码片段中，我们声明了一个名为 Sum 的泛型方法，其中包含两个 T 类型的参数 val1 和 val2。当您调用泛型方法时，需要为这些参数传递值。

以下代码片段显示了 Sum() 方法的用法：

```
private void button3_Click(object sender, System.EventArgs e)
{
  Arithmetic objA1 = MGColA.Items[0];
  Arithmetic objA2 = MGColA.Items[1];
  Person objP1 = MGColP.Items[0];
  Person objP2 = MGColP.Items[1];
  TextBox1.Text = Sum(objA1, objA2);
  TextBox2.Text = Sum(objP1, objP2);
}
```

现在让我们探索一些泛型集合类。

### .NET 中的泛型集合类

.NET 提供了许多类来创建泛型集合。泛型类是集合类的替代品，并且是强类型的。这些类中包含的方法提供不同的功能，例如元素的排序、元素顺序的反转以及在被包含的元素中搜索特定元素。泛型类还允许您创建键/值对的泛型集合。这些键/值对允许您添加、排序和搜索元素。一些泛型集合类如下：

- List<T> 类
- LinkedList<T> 类
- SortedList<TKey, TValue> 类

