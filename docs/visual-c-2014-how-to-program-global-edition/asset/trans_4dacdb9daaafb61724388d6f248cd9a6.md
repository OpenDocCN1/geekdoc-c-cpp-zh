

## SortedDictionary 的 Values 属性

如果你不需要键，SortedDictionary 还提供了一个只读的 Values 属性，它可以获取存储在 SortedDictionary 中所有值的的 `ICollection<T>`。你可以使用此属性来遍历 SortedDictionary 中存储的值，而无需考虑它们对应的键。

## 21.5 泛型 List 集合

第 9.4 节引入了泛型 `List<T>`，它定义了一个基于数组的实现。在这里，我们讨论 `LinkedList<T>`，它定义了一个可以向前和向后导航的双向链表。`LinkedList<T>` 包含泛型类 `LinkedList<T>` 的节点。每个节点包含一个属性 `Value` 以及两个只读属性 `Previous` 和 `Next`。`Value` 属性与 `LinkedList<T>` 的单个类型参数匹配，因为它包含了存储在节点中的数据。`Previous` 提供链表中前一个节点的引用（如果该节点是第一个，则为 `null`）。同样，`Next` 提供链表中后一个结的引用（如果该节点是最后一个，则为 `null`）。我们在图 21.5 中演示了几个链表操作。

```csharp
// 图 21.5: LinkedTest.cs
// 使用 LinkedList（链表）。
using System;
using System.Collections.Generic;

class LinkedTest
{
    private static readonly string[] colors =
        "black", "yellow", "green", "blue", "violet", "silver";
    private static readonly string[] colors2 =
        "gold", "white", "brown", "blue", "gray";

    // 设置并操作 LinkedList 对象
    static void Main()
    {
        var list1 = new LinkedList<string>();
        // 向第一个链表添加元素
        foreach (var color in colors)
        {
            list1.AddLast(color);
        }

        // 通过构造函数向第二个链表添加元素
        var list2 = new LinkedList<string>(colors2);
        Concatenate(list1, list2); // 将 list2 并到 list1 上
        PrintList(list1);
        Console.WriteLine("\n将 list1 中的字符串转换为大写\n");
        ToUpperStrings(list1); // 转换为大写字符串
```

```
图 21.5 | 使用 LinkedList（3 部分中的第 1 部分）。

## 21.5 泛型 LinkedList 集合

| 行 | 代码 |
| :--- | :--- |
| 32 | PrintList(list1); // 显示 list1 元素 |
| 33 | |
| 34 | | |
| 35 | Console.WriteLine("\n删除 BLACK 和 BROWN 之间的字符串\n"); |
| 36 | RemoveItemsBetween(list1, "BLACK", "BROWN"); |
| 37 | | |
| 38 | PrintList(list1); // 显示 list1 元素 |
| 39 | PrintReverseList(list1); // 逆序显示列表 |
| 40 | } |
| 41 | // 打印列表内容 |
| 42 | private static void PrintList<T>(LinkedList<T> list) |
| 43 | { |
| 44 | Console.WriteLine("Linked list: "); |
| 45 | |
| 46 | foreach (var value in list) |
| 47 | { |
| 48 | Console.Write($"{value}"); |
| 49 | |

| 50 | } |
| 51 | Console.WriteLine(); |
| 52 | } |
| 53 | |
| 54 | // 将第二个列表连接到第一个列表的末尾 |
| 55 | private static void Concatenate<T>( |
| 56 | LinkedList<T> list1, LinkedList<T> list2 |
| 57 | { |
| 58 | // 通过复制元素值连接链表 |
| 59 | // 从第二个列表按顺序执行 |
| 60 | foreach (var value in list2) |
| 61 | { |
| 62 | list1.AddLast(value); // 添加新节点 |
| 63 | } |
| 64 | } |
| 65 | // 定位字符串并转换为大写 |
| 66 | private static void ToUppercaseStrings(LinkedList<T> list) |
| 67 | { |
| 68 | // 使用节点遍历列表 |
| 69 | LinkedListNode<string> currentNode = list.First; |
| 70 | while (currentNode != null) |
| 71 | { |
| 72 | string color = currentNode.Value; // 获取节点中的值 |
| 73 | currentNode.Value = color.ToUpper(); // 转换为大写 |
| 74 | currentNode = currentNode.Next; // 获取下一个节点 |
| 75 | } |
| 76 | } |
| 77 | // 删除两个项目之间的项 |
| 78 | private static void RemoveItemsBetween<T>( |
| 79 | LinkedList<T> list, T startItem, T endItem) |
| 80 | } |

图 21.5 | 使用 LinkedList。（3 部分中的第 2 部分）。

## 21 泛型集合：使用 LINQ/PLINQ 进行函数式编程

```csharp
// 获取起始和结束项对应的节点
LinkedListNode<T> currentNode = list.Find(startItem);
LinkedListNode<T> endNode = list.Find(endItem);

// 删除两个项目之间的项
private static void RemoveItemsBetween<T>(
    LinkedList<T> list, T startItem, T endItem)
{
    // 省略具体实现
}

// 打印列表内容
private static void PrintList<T>(LinkedList<T> list)
{
    Console.WriteLine("Linked list: ");
    foreach (var value in list)
    {
        Console.Write($"{value}");
    }
    Console.WriteLine();
}

// 将第二个列表连接到第一个列表的末尾
private static void Concatenate<T>(
    LinkedList<T> list1, LinkedList<T> list2)
{
    // 通过复制元素值连接链表
    // 从第二个列表按顺序执行
    foreach (var value in list2)
    {
        list1.AddLast(value); // 添加新节点
    }
}

// 定位字符串并转换为大写
private static void ToUppercaseStrings(LinkedList<string> list)
{
    // 使用节点遍历列表
    LinkedListNode<string> currentNode = list.First;
    while (currentNode != null)
    {
        string color = currentNode.Value; // 获取节点中的值
        currentNode.Value = color.ToUpper(); // 转换为大写
        currentNode = currentNode.Next; // 获取下一个节点
    }
}

// 逆序显示列表
private static void PrintReverseList<T>(LinkedList<T> list)
{
    // 省略具体实现
}
```

