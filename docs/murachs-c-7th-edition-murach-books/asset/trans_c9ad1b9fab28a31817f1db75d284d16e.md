

## 如何使用泛型

在第8章中，你学习了如何使用泛型集合，例如由`List<>`、`SortedList<>`、`Stack<>`和`Queue<>`类定义的集合。大多数情况下，只要需要处理对象集合，你都可以使用这些来自.NET Framework的集合或其他集合。然而，有时你可能需要使用泛型来定义自己的泛型集合，以添加.NET提供的泛型集合所不具备的功能。如果是这样，接下来的主题将向你展示如何做到这一点。此外，这些主题还将揭示.NET提供的泛型集合的内部工作原理。

### 如何编写定义泛型集合的类

图15-8的第1部分展示了一个名为`CustomList<>`的类，它定义了一个泛型集合。虽然这个类很简单，并且没有提供任何比`List<>`类更出色的额外功能，但它阐释了定义泛型集合所需的所有基本原理。

首先，在类名后面的尖括号内声明一个名为`T`的数据类型变量。这个变量表示从该类创建对象时为类指定的数据类型。例如，如果你像这样创建一个自定义列表类：

```
CustomList<Product> products = new CustomList<Product>();
```

编译器会在任何编写了`T`变量的位置替换为`Product`类型。因此，在编写`CustomList`类时，你可以使用`T`变量来表示为类指定的数据类型。

首先，该类声明了一个类型为`T`的私有`List<>`变量。因此，这个私有列表可以存储任何数据类型。然后，`Add()`方法将一个类型为`T`的对象添加到私有列表中。接下来，该类的只读索引器返回指定索引处类型为`T`的对象，`Count`属性返回列表中的项数。最后，该类声明了一个标准的`ToString()`方法，返回一个表示存储在列表中的类型为`T`的对象的字符串。

虽然这个`CustomList`类使用`T`作为类的类型参数名称，但你在这里可以使用任何参数名称。例如，你可以使用更长的名称，如`DocumentType`。然而，大多数泛型类使用`T`作为类型参数的名称。此规则的主要例外是处理包含键和值的字典的泛型集合。这些泛型集合通常使用`K`表示键类型，使用`V`表示值类型，就像这样：

```
public class CustomDictionary<K, V>
```

顺便提一下，这展示了如何定义接受两个类型参数的泛型类，这是可能的，但很少见。

### 一个使用泛型的`CustomList<>`类

```
public class CustomList<T>
{
    private List<T> list = new List<T>();

    // 一个 Add() 方法
    public void Add(T item) => list.Add(item);

    // 一个只读索引器
    public T this[int i] => list[i];

    // 一个只读属性
    public int Count => list.Count;

    // ToString() 方法
    public override string ToString()
    {
        string listString = "";

        for (int i = 0; i < list.Count; i++)
        {
            listString += list[i].ToString() + "\n";
        }
        return listString;
    }
}
```

### 描述

- 你可以使用泛型来定义一个类型安全的集合，该集合可以接受任何类型的元素。
- 要为泛型集合定义类，你需要在类名后面编写尖括号，并在这些括号内指定类型参数。然后，在类内部，你可以在任何可以使用数据类型的地方使用该类型参数。例如，你可以将其用作方法的返回类型或参数类型。
- 按照惯例，大多数程序员使用字母`T`作为大多数类的类型参数。然而，你在这里可以使用任何参数名称。

图15-8的第2部分展示了一些使用第1部分中定义的`CustomList<>`类的代码。首先，第一个测试创建了一个可以存储`int`类型的`CustomList<>`类，向列表中添加两个`int`值，并将这些值写入输出窗口。然后，第二个测试创建了一个可以存储`Product`类型的`CustomList<>`类，向列表中添加两个`Product`对象，并将这些对象写入输出窗口。

这个示例表明，`CustomList<>`类可以存储值类型（如`int`类型）或引用类型（如`Product`类型）。更重要的是，它表明`CustomList<>`类的工作方式与.NET定义的其他泛型类类似，尽管它目前还没有提供这些类中任何一个那么多的功能。请注意，此示例的输出假定`Product`类包含一个`ToString()`方法，该方法返回一个字符串，其中产品的代码、描述和价格以制表符分隔。

### 使用`CustomList<>`类的代码

```
// 测试 1
Debug.WriteLine("List 1 - ints");
CustomList<int> list1 = new CustomList<int>();
int i1 = 11;
int i2 = 7;
list1.Add(i1);
list1.Add(i2);
Debug.WriteLine(list1.ToString());

// 测试 2
Debug.WriteLine("List 2 - Products");
CustomList<Product> list2 = new CustomList<Product>();
Product p1 = new Product("JAVA", "Murach's Java Programming", 59.50m);
Product p2 = new Product("C#", "Murach's C#", 59.50m);
list2.Add(p1);
list2.Add(p2);
Debug.Write(list2.ToString());
```

### 生成的输出

```
List 1 - ints
11
7

List 2 - Products
JAVA    Murach's Java Programming    $59.50
C#      Murach's C#                 $59.50
```

### 描述

- 泛型`CustomList<>`类的工作方式与第8章中描述的泛型.NET集合类类似。
- 上面显示的生成输出假定`Product`类包含一个`ToString()`方法，该方法以制表符分隔的方式显示产品代码、描述和价格。

### .NET定义的一些泛型接口

.NET的泛型集合使用图15-9中描述的泛型接口。如果将这些接口与图15-2中呈现的接口进行比较，你会发现大多数泛型接口都有对应的常规接口。然而，泛型接口使用尖括号来指定接口的数据类型，就像泛型类使用尖括号来指定类的数据类型一样。此外，泛型接口存储在`System.Collections.Generic`命名空间中，并且被设计为与该命名空间中存储的泛型集合一起工作。

如果你决定定义自己的泛型集合，例如前面图中所示的`CustomList<>`类，你可能希望实现其中一些接口。例如，如果你想能够使用`foreach`循环迭代你的泛型集合，你需要实现`IEnumerable<>`接口。你将在图15-12中学习如何做到这一点。但首先，你将在下一图中学习如何实现`IComparable<>`接口。

### 一个常用的.NET泛型接口

| 接口 | 成员 | 描述 |
|---|---|---|
| IComparable<> | int CompareTo(T) | 比较类型为`T`的对象。 |

### 用于泛型集合的常用.NET接口

| 接口 | 成员 | 描述 |
|---|---|---|
| IEnumerable<> | IEnumerator<T> GetEnumerator() | 获取集合的类型为`T`的枚举器。 |
| ICollection<> | int Count<br>bool IsReadOnly<br>T SyncRoot<br>void Add(T)<br>void Clear()<br>bool Contains(T)<br>void CopyTo(array, int)<br>bool Remove(T) | 为可枚举集合提供基本属性。此接口继承自`IEnumerable<>`。 |
| IList<> | [int]<br>int IndexOf(T)<br>void Insert(int, T)<br>void RemoveAt(int) | 管理基本的对象列表。此接口继承自`ICollection<>`和`IEnumerable<>`。 |
| IDictionary<> | [int]<br>ICollection<K> Keys<br>ICollection<V> Values<br>bool Remove(K)<br>bool TryGetValue(K, V) | 管理键/值对集合。此接口继承自`ICollection<>`和`IEnumerable<>`。 |

### 描述

- .NET定义了许多泛型接口。这些接口对于处理定义泛型集合的类尤其有用，并且它们对应于图15-2中描述的大多数常规接口。
- `ICollection<>`接口继承自`IEnumerable<>`接口，这意味着任何实现`ICollection<>`的类也必须实现`IEnumerable<>`。类似地，`IList<>`和`IDictionary<>`接口继承自`ICollection<>`和`IEnumerable<>`。
- 用于处理泛型集合的接口存储在`System.Collections.Generic`命名空间中。
- 此表仅列出了每个接口最重要的成员。有关这些接口的完整描述及其成员列表，请参阅在线文档。

