
将 stringList 声明为对字符串的引用的 List。带有这种占位符、使其可与任意类型一起使用的类称为泛型类。第 18 章将讨论泛型类。第 19 章将讨论其他泛型集合类。图 19.2 提供了集合类的表格。图 9.5 显示了类 List<T> 的一些常用方法和属性。

| 方法或属性 | 描述 |
| --- | --- |
| Add | 向 List 末尾添加一个元素。 |
| AddRange | 将其集合参数的元素添加到 List 末尾。 |
| Capacity | 属性，获取或设置 List 在不调整大小的情况下可存储的元素数。 |
| Clear | 从 List 中移除所有元素。 |
| Contains | 如果 List 包含指定元素，则返回 true，否则返回 false。 |
| Count | 属性，返回 List 中存储的元素数。 |
| IndexOf | 返回指定值在 List 中首次出现的索引。 |
| Insert | 在指定索引处插入一个元素。 |
| Remove | 移除指定值的第一个匹配项。 |
| RemoveAt | 移除指定索引处的元素。 |
| RemoveRange | 从指定索引开始移除指定数量的元素。 |
| Sort | 对 List 排序。 |
| TrimExcess | 将 List 的 Capacity 设置为 List 当前包含的元素数（Count）。 |

图 9.5 | 类 List<T> 的一些方法和属性。

## 9.4.2 动态调整 List<T> 集合的大小

图 9.6 演示了动态调整 List 对象的大小。第 11 行创建一个字符串 List，然后第 14–15 行分别显示该 List 的初始 Count 和 Capacity：

- Count 属性返回 List 中当前元素的数量。
- Capacity 属性指示 List 在不扩容的情况下可容纳多少项。

创建 List 时，两者最初都为 0——不过 Capacity 取决于具体实现。

```
1   // Fig. 9.6: ListCollection.cs
2   // Generic List<T> collection demonstration.
3   using System;
4   using System.Collections.Generic;
5
6   class ListCollection
7   {
```

图 9.6 | 泛型 List<T> 集合演示。（第 1 部分，共 3 部分。）

```csharp
static void Main()
{
    // create a new List of strings
    var items = new List<string>();

    // display List's Count and Capacity before adding elements
    Console.WriteLine("Before adding to items: " +
        $"Count = {items.Count}; Capacity = {items.Capacity}");

    items.Add("red"); // append an item to the List
    items.Insert(0, "yellow"); // insert the value at index 0

    // display List's Count and Capacity after adding two elements
    Console.WriteLine("After adding two elements to items: " +
        $"Count = {items.Count}; Capacity = {items.Capacity}");

    // display the colors in the list
    Console.Write(
        "\nDisplay list contents with counter-controlled loop:");
    for (var i = 0; i < items.Count; i++)
    {
        Console.Write("{0} {items[i]}");
    }

    // display colors using foreach
    Console.Write("\nDisplay list contents with foreach statement:");
    foreach (var item in items)
    {
        Console.Write("{0} {item}");
    }

    items.Add("green"); // add "green" to the end of the List
    items.Add("yellow"); // add "yellow" to the end of the List

    // display List's Count and Capacity after adding two more elements
    Console.WriteLine("\n\nAfter adding two more elements to items: " +
        $"Count = {items.Count}; Capacity = {items.Capacity}");

    // display the List
    Console.Write("\nList with two new elements:");
    foreach (var item in items)
    {
        Console.Write("{0} {item}");
    }

    items.Remove("yellow"); // remove the first "yellow"

    // display the List
    Console.Write("\n\nRemove first instance of yellow:");
    foreach (var item in items)
    {
        Console.Write("{0} {item}");
    }
}
```

~~~csharp
61    items.RemoveAt(1); // remove item at index 1

    // display the List
    Console.WriteLine("\nRemove second list element (green):");
    foreach (var item in items)
    {
        Console.Write($"{item}");
    }

    // display List's Count and Capacity after removing two elements
    Console.WriteLine("\nAfter removing two elements from items: " +
        $"Count = {items.Count}; Capacity = {items.Capacity}");

    // check if a value is in the List
    Console.WriteLine("\n\"red\" is " +
        $"{(items.Contains("red") ? string.Empty : "not ")}in the list");

    items.Add("orange"); // add "orange" to the end of the List
    items.Add("violet"); // add "violet" to the end of the List
    items.Add("blue"); // add "blue" to the end of the List

    // display List's Count and Capacity after adding three elements
    Console.WriteLine("\nAfter adding three more elements to items: " +
        $"Count = {items.Count}; Capacity = {items.Capacity}");

    // display the List
    Console.WriteLine("List with three new elements:");
    foreach (var item in items)
    {
        Console.Write($"{item}");
    }
    Console.WriteLine();

    }
}
~~~

向 items 添加元素前：Count = 0；Capacity = 0

向 items 添加两个元素后：Count = 2；Capacity = 4

使用计数器控制的循环显示列表内容：yellow red
使用 foreach 语句显示列表内容：yellow red

再向 items 添加两个元素后：Count = 4；Capacity = 4
包含两个新元素的列表：yellow red green yellow

移除第一个 yellow 实例：red green yellow
移除第二个列表元素（green）：red yellow
从 items 中移除两个元素后：Count = 2；Capacity = 4

"red" 在列表中

再向 items 添加三个元素后：Count = 5；Capacity = 8
包含三个新元素的列表：red yellow orange violet blue

图 9.6 | 泛型 List<T> 集合演示。（第 3 部分，共 3 部分）

### 添加和插入元素

`Add` 和 `Insert` 方法向 `List` 添加元素（第 17–18 行）：

- `Add` 方法将其参数*追加*到 `List` 的末尾。
- `Insert` 方法在指定位置插入一个新元素。

Insert 的第一个参数是索引——与数组一样，集合索引从零开始。第二个参数是要在指定索引处插入的值。为了给新元素腾出空间，位于指定索引及以上的元素的索引都增加一——在此例中，"red" 最初位于索引 0，但现在位于索引 1，以便 "yellow" 可以插入到索引 0。

### Count 和 Capacity

第 21–22 行显示 `Add` 和 `Insert` 操作后 `List` 的 `Count`（2）和 `Capacity`（4）。第 17 行执行时，`List` 会增长，将其 `Capacity` 增加到 4，以便 `List` 可以容纳*四个元素*。其中一个元素立即被 "red" 占用。此时，`List` 的 `Count` 为 1。第 18 行执行时，仍有空间容纳另外三个元素，因此插入 "yellow"，`Count` 变为 2。

### 遍历 List 的内容

第 27–30 行显示 `List` 中的项。与数组元素一样，可以通过在 `List` 变量名后的方括号中放置索引来访问 `List` 元素。带索引的 `List` 表达式可用于修改该索引处的元素。第 34–37 行使用首选的 `foreach` 语句显示 `List`。

### 添加更多元素并扩展 List

第 39–51 行向 `List` 添加更多元素，然后再次显示其 `Count`、`Capacity` 和内容。

### 移除元素

`Remove` 方法删除具有特定值的第一个元素（第 53 行），如果成功则返回 `true`，否则返回 `false`。第 57–60 行显示第 53 行执行后 `List` 的内容。类似的方法 `RemoveAt` 移除指定索引处的元素（第 62 行）。通过这两种方法之一移除元素时，该索引之上所有元素的索引都减一——与 `Insert` 方法相反。第 66–69 行显示第 62 行执行后 `List` 的内容。第 72–73 行显示移除操作后 `List` 的 `Count`（2）和 `Capacity`（4）。此时，`List` 中还有空间容纳另外两个元素。

### 确定元素是否在 List 中

第 77 行使用 `Contains` 方法检查某项是否在 `List` 中。如果在 `List` 中找到该元素，`Contains` 方法返回 `true`，否则返回 `false`。该方法按顺序将其参数与 `List` 的每个元素进行比较，直到找到该项，因此在大型 `List` 上使用 `Contains` 效率低下。

### 添加更多元素并扩展 List

第 79–81 行向 `List` 再添加三个元素。在第 79–80 行执行之前，`Count` 为 2，`Capacity` 为 4，因此 `List` 中有空间容纳这些行添加的两个新元素
