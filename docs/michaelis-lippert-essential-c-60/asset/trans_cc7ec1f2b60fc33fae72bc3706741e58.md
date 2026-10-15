

![](img/25683ccec0773ba5b8794b11f2b12877_683_0.png)

## 图 16.1：通用集合接口层次结构

字典类通常只提供按键索引，而不按位置索引。

相比之下，列表按特定顺序存储值，并通过位置访问它们。从某种意义上说，列表只是字典的一种特例，其中“键”始终是整数，并且“键集合”始终是从零开始的连续非负整数集合。尽管如此，这一差异足够显著，值得用完全不同的类型来表示。

因此，在选择集合类来解决数据存储或检索问题时，首先要查找的两个接口是 `IList<T>` 和 `IDictionary<TKey, TValue>`。这两个接口表示集合类型是侧重于根据给定位置索引检索值，还是侧重于根据给定关联键检索值。

这两个接口都要求实现它们的类提供索引器。对于 `IList<T>`，索引器的操作数对应于所检索元素的位置：索引器接受一个整数，并允许你访问列表中的第 n 个元素。对于 `IDictionary<TKey, TValue>` 接口，索引器的操作数对应于与值关联的键，并允许你访问该值。

## ICollection<T>

`IList<T>` 和 `IDictionary<TKey, TValue>` 都实现了 `ICollection<T>`。未实现 `IList<T>` 或 `IDictionary<TKey, TValue>` 的集合很可能会实现 `ICollection<T>`（尽管并非必然，因为集合可以实现更基本的要求 `IEnumerable` 或 `IEnumerable<T>`）。`ICollection<T>` 派生自 `IEnumerable<T>`，并包含两个成员：`Count` 和 `CopyTo()`。

- `Count` 属性返回集合中元素的总数。乍一看，这似乎足以使用 `for` 循环遍历集合中的每个元素，但事实上，集合还需要支持按索引检索，而 `ICollection<T>` 接口并不包含这一点（尽管 `IList<T>` 包含）。

- `CopyTo()` 方法提供了将集合转换为数组的能力。该方法包含一个索引参数，以便你可以指定在目标数组中插入元素的位置。要使用该方法，你必须初始化目标数组，使其从索引位置开始具有足够的容量来容纳 `ICollection<T>` 中的所有元素。

## 主要集合类

有五类主要的集合类，它们在数据的插入、存储和检索方式上有所不同。每个泛型类都位于 `System.Collections.Generic` 命名空间中，其对应的非泛型类位于 `System.Collections` 命名空间中。

## 列表集合：`List<T>`

`List<T>` 类具有与数组相似的属性。关键区别在于，这些类会随着元素数量的增加而自动扩展。（相比之下，数组的大小是固定的。）此外，列表可以通过显式调用 `TrimToSize()` 或设置 `Capacity` 来缩小（见图 16.2）。

![](img/25683ccec0773ba5b8794b11f2b12877_685_0.png)

**图 16.2：** `List<>` 类图

这些类被归类为**列表集合**，其显著功能是每个元素可以像数组一样通过索引单独访问。因此，你可以使用索引运算符设置和访问列表集合类中的元素，其中索引参数的值对应于集合中元素的位置。清单 16.1 显示了一个示例，输出 16.1 显示了结果。

## 清单 16.1：使用 `List<T>`

```
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        List<string> list = new List<string>();

        // 列表会在添加元素时自动扩展。
        list.Add("Sneezy");
        list.Add("Happy");
        list.Add("Dopey");
        list.Add("Doc");
        list.Add("Sleepy");
        list.Add("Bashful");
        list.Add("Grumpy");

        list.Sort();

        Console.WriteLine(
            $"按字母顺序排列 { list[0] } 是第一个"
            + $"矮人，而 { list[6] } 是最后一个。");

        list.Remove("Grumpy");
    }
}
```

## 输出 16.1

```
按字母顺序排列 Bashful 是第一个矮人，而 Sneezy 是最后一个。
```

C# 是从零开始索引的；因此，清单 16.1 中的索引 0 对应于第一个元素，索引 6 表示第七个元素。按索引检索元素不涉及搜索，而是一项快速简单的“跳转”到内存中某个位置的操作。

`List<T>` 是一个有序集合；`Add()` 方法将给定项追加到列表末尾。在调用清单 16.1 中的 `Sort()` 之前，“Sneezy”是第一个，“Grumpy”是最后一个；调用之后，列表按字母顺序排序，而不是按添加项的顺序排序。某些集合会在添加元素时自动排序，但 `List<T>` 不在此列；需要对元素进行排序时必须显式调用 `Sort()`。

要移除元素，可以使用 `Remove()` 或 `RemoveAt()` 方法，分别用于移除给定元素或移除特定索引处的元素。

## 高级主题

## 自定义集合排序

你可能想知道清单 16.1 中的 `List<T>.Sort()` 方法是如何知道将列表元素按字母顺序排序的。`string` 类型实现了 `IComparable<string>` 接口，该接口有一个方法 `CompareTo()`。它返回一个整数，指示传入的元素是大于、小于还是等于当前元素。如果元素类型实现了泛型 `IComparable<T>` 接口（或非泛型 `IComparable` 接口），排序算法默认会使用它来确定排序顺序。

但如果元素类型没有实现 `IComparable<T>`，或者默认的比较逻辑不满足你的需求，该怎么办？要指定非默认的排序顺序，你可以调用 `List<T>.Sort()` 的重载，该重载接受一个 `IComparer<T>` 作为参数。

`IComparable<T>` 和 `IComparer<T>` 之间的区别很微妙但很重要。第一个接口表示“我知道如何将自己与同一类型的另一个实例进行比较。”后者表示“我知道如何比较给定类型的两个对象。”

`IComparer<T>` 接口通常用于当数据类型有多种不同排序方式且没有一种明显最佳时。例如，你可能有一个 `Contact` 对象的集合，有时你想按姓名、位置、生日、地理区域或任何其他可能条件排序。与其选择一种排序策略并让 `Contact` 类实现 `IComparable<Contact>`，更明智的做法可能是创建多个实现 `IComparer<Contact>` 的不同类。清单 16.2 显示了一个按姓氏、名字比较的示例实现。

## 清单 16.2：实现 `IComparer<T>`

```
class Contact
{
    public string FirstName { get; private set; }
    public string LastName { get; private set; }
    public Contact(string firstName, string lastName)
    {
        this.FirstName = firstName;
        this.LastName = lastName;
    }
}

using System;
using System.Collections.Generic;

class NameComparison : IComparer<Contact>
{
    public int Compare(Contact x, Contact y)
    {
        if (Object.ReferenceEquals(x, y))
            return 0;
        if (x == null)
            return 1;
        if (y == null)
            return -1;
        int result = StringCompare(x.LastName, y.LastName);
        if (result == 0)
            result = StringCompare(x.FirstName, y.FirstName);
        return result;
    }

    private static int StringCompare(string x, string y)
    {
        if (Object.ReferenceEquals(x, y))
            return 0;
        if (x == null)
            return 1;
        if (y == null)
            return -1;
        return x.CompareTo(y);
    }
}
```

要按姓氏再按名字对 `List<Contact>` 进行排序，你可以调用 `contactList.Sort(new NameComparer())`。

## 全序

在实现 `IComparable<T>` 或 `IComparer<T>` 时，你必须产生一个全序。你的 `CompareTo` 实现必须为任意可能的项对提供完全一致的排序。该排序需要具有一些基本特征。例如，每个元素都必须被视为等于自身。如果一个元素

