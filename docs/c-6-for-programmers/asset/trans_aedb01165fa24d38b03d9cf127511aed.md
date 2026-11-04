
按其空白字符分割字符串。在正则表达式 `\s+` 中，`\s` 表示空白字符，`+` 表示其左侧表达式的一个或多个——因此单词由一个或多个空白字符分隔，这些空白字符会被丢弃。这创建了一个 "words" 数组，我们将其存储在局部变量 words 中。

### SortedDictionary 方法 ContainsKey 和 Add

第 31–45 行遍历数组 words。每个单词都使用字符串方法 ToLower 转换为小写，然后存储在变量 key 中（第 33 行）。接下来，第 36 行调用 SortedDictionary 方法 ContainsKey 来确定该单词是否在字典中。如果是，则该单词之前已在句子中出现。如果 SortedDictionary 不包含该单词的条目，则第 43 行使用 SortedDictionary 方法 Add 在字典中创建一个新条目，以小写单词作为键，1 作为值。

> **常见编程错误 19.2**
> 使用 Add 方法向哈希表中添加已存在的键会导致 `ArgumentException`。

### SortedDictionary 索引器

如果该单词已是哈希表中的键，则第 38 行使用 SortedDictionary 的索引器获取并设置字典中该键的关联值（单词计数）。使用不存在于哈希表中的键的设置访问器会创建一个新条目，就像你使用 Add 方法一样，因此第 43 行可以写成

```csharp
dictionary[key] = 1;
```

> **常见编程错误 19.3**
> 使用不存在于集合中的键调用 SortedDictionary 索引器的 get 访问器会导致 `KeyNotFoundException`。

### 方法 DisplayDictionary

第 47 行将字典返回给 Main 方法，然后该方法将其传递给方法 DisplayDictionary（第 51–65 行），该方法显示所有键值对。此方法使用只读属性 Keys（第 59 行）获取包含所有键的 `ICollection<T>`。由于接口 `ICollection<T>` 扩展了 `IEnumerable<T>`，我们可以在第 59–62 行的 `foreach` 语句中使用此集合来遍历键。此循环使用迭代变量和 SortedDictionary 索引器的 get 访问器访问并输出每个键及其对应的值。每个键和值都以左对齐的方式在宽度为 12 的字段中显示。由于 SortedDictionary 将其键值对存储在二叉搜索树中，因此键值对会按键的排序顺序显示。第 64 行使用 SortedDictionary 属性 Count 获取字典中键值对的数量。

### 遍历 SortedDictionary 的 KeyValuePairs

第 59–62 行也可以使用 `foreach` 语句与 SortedDictionary 对象本身，而不是使用 Keys 属性。如果使用 `foreach` 语句与 SortedDictionary 对象，则迭代变量的类型将为 `KeyValuePair<K,V>`。SortedDictionary 的枚举器使用 `KeyValuePair<K,V>` 结构体值类型来存储键值对。`KeyValuePair<K,V>` 提供属性 Key 和 Value 用于检索当前元素的键和值。

### SortedDictionary 的 Values 属性

如果不需要键，类 SortedDictionary 还提供一个只读 Values 属性，该属性获取存储在 SortedDictionary 中的所有值的 `ICollection<T>`。你可以使用此属性遍历 SortedDictionary 中存储的值，而不考虑其对应的键。

## 19.5 泛型 LinkedList 集合

第 9.4 节介绍了泛型 `List<T>` 集合，该集合定义了基于数组的列表实现。在这里，我们讨论类 `LinkedList<T>`，它定义了一个双向链表，应用程序可以向前和向后导航。`LinkedList<T>` 包含泛型类 `LinkedListNode<T>` 的节点。每个节点包含属性 Value 和只读属性 Previous 和 Next。Value 属性的类型与 `LinkedList<T>` 的单个类型参数匹配，因为它包含存储在节点中的数据。Previous 获取链表中前一个节点的引用（如果节点是列表的第一个节点，则为 null）。类似地，Next 获取链表中后续节点的引用（如果节点是列表的最后一个节点，则为 null）。我们在图 19.5 中演示了一些链表操作。

```csharp
// Fig. 19.5: LinkedListTest.cs
// Using LinkedLists.
using System;
using System.Collections.Generic;

class LinkedListTest
{
   private static readonly string[] colors =
      { "black", "yellow", "green", "blue", "violet", "silver" };
   private static readonly string[] colors2 =
      { "gold", "white", "brown", "blue", "gray" };

   // set up and manipulate LinkedList objects
   static void Main()
   {
      var list1 = new LinkedList<string>();

      // add elements to first linked list
      foreach (var color in colors)
      {
         list1.AddLast(color);
      }

      // add elements to second linked list via constructor
      var list2 = new LinkedList<string>(colors2);

      Concatenate(list1, list2); // concatenate list2 onto list1
      PrintList(list1); // display list1 elements

      Console.WriteLine("\nConverting strings in list1 to uppercase\n");
      ToUppercaseStrings(list1); // convert to uppercase string

32        PrintList(list1); // display list1 elements
33
34        Console.WriteLine("\nDeleting strings between BLACK and BROWN\n");
35        RemoveItemsBetween(list1, "BLACK", "BROWN");
36
37        PrintList(list1); // display list1 elements
38        PrintReversedList(list1); // display list in reverse order
39    }
40
41    // display list contents
42    private static void PrintList<T>(LinkedList<T> list)
43    {
44        Console.WriteLine("Linked list: ");
45
46        foreach (var value in list)
47        {
48            Console.Write($"{value} ");
49        }
50
51        Console.WriteLine();
52    }
53
54    // concatenate the second list on the end of the first list
55    private static void Concatenate<T>(
56        LinkedList<T> list1, LinkedList<T> list2)
57    {
58        // concatenate lists by copying element values
59        // in order from the second list to the first list
60        foreach (var value in list2)
61        {
62            list1.AddLast(value); // add new node
63        }
64    }
65
66    // locate string objects and convert to uppercase
67    private static void ToUppercaseStrings(LinkedList<string> list)
68    {
69        // iterate over the list by using the nodes
70        LinkedListNode<string> currentNode = list.First;
71
72        while (currentNode != null)
73        {
74            string color = currentNode.Value; // get value in node
75            currentNode.Value = color.ToUpper(); // convert to uppercase
76            currentNode = currentNode.Next; // get next node
77        }
78    }
79
80    // delete list items between two given items
81    private static void RemoveItemsBetween<T>(
82        LinkedList<T> list, T startItem, T endItem)
83    {
        // get the nodes corresponding to the start and end item
        LinkedListNode<T> currentNode = list.Find(startItem);
        LinkedListNode<T> endNode = list.Find(endItem);

        // remove items after the start item
        // until we find the last item or the end of the linked list
        while ((currentNode.Next != null) && (currentNode.Next != endNode))
        {
            list.Remove(currentNode.Next); // remove next node
        }
    }

    // display reversed list
    private static void PrintReversedList<T>(LinkedList<T> list)
    {
        Console.WriteLine("Reversed List:");

        // iterate over the list by using the nodes
        LinkedListNode<T> currentNode = list.Last;

        while (currentNode != null)
        {
            Console.Write($"{currentNode.Value} ");
            currentNode = currentNode.Previous; // get previous node
        }

        Console.WriteLine();
    }
}
```

**图 19.5** | 使用 LinkedLists。（第 1 部分，共 3 部分。）
**图 19.5** | 使用 LinkedLists。（第 2 部分，共 3 部分。）
**图 19.5** | 使用 LinkedLists。（第 3 部分，共 3 部分。）

第 16–25 行创建名为 list1 和 list2 的字符串 `LinkedList`，并分别用数组 colors 和 colors2 的内容填充它们。`LinkedList` 是一个泛型类，它有一个类型参数，在此示例中我们指定类型参数 `string`（第 16 行和第 25 行）。

### LinkedList 方法 AddLast 和 AddFirst

我们演示了两种填充列表的方法。第 19–22 行使用 `foreach` 语句和方法 AddLast 来填充 list1。AddLast 方法创建一个新的 `LinkedListNode`（带有
