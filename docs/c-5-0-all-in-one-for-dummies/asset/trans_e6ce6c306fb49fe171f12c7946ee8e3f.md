

```csharp
int index = Find(key);
if (index < 0)
{
    // It isn't -- find a new spot.
    index = FindEmpty();
    _keys[index] = key;
}

// Save the object in the corresponding spot.
_arrayElements[index] = value;

get
{
    int index = Find(key);
    if (index < 0)
    {
        return null;
    }
    return _arrayElements[index];
}
}
}

public class Program
{
    public static void Main(string[] args)
    {
        // Create an array with enough room.
        KeyedArray ma = new KeyedArray(100);

        // Save the ages of the Simpson kids.
        ma["Bart"] = 8;
        ma["Lisa"] = 10;
        ma["Maggie"] = 2;

        // Look up the age of Lisa.
        Console.WriteLine("Let's find Lisa's age");
        int age = (int)ma["Lisa"];
        Console.WriteLine("Lisa's age is {0}", age);

        // Wait for user to acknowledge the results.
        Console.WriteLine("Press Enter to terminate...");
        Console.Read();
    }
}
}
```

类 KeyedArray 包含两个普通数组。_arrayElements 对象数组包含实际的 KeyedArray 数据。驻留在 _keys 数组中的字符串充当对象数组的标识符。_keys 的第 i 个元素对应于 _arrayElements 的第 i 个条目。应用程序随后可以通过对应用程序有意义的字符串标识符来索引 KeyedArray。

![](img/80ff26f06fc9ab951e1cd4257b867366_170_0.png)

非整数索引被称为键。顺便说一下，你可以用底层的 List<T> 而不是固定大小的数组来实现 KeyedArray。List<T> 可以像数组一样被索引，因为两者都实现了 IList（或 IList<T>）接口。这使得 KeyedArray 可以是泛型的，并且比使用内部数组灵活得多。

set[string] 索引器首先通过调用 Find() 方法检查指定的索引是否已存在。如果 Find() 返回一个索引，set[] 将新数据对象存储到 _arrayElements 中对应的索引。如果 Find() 找不到该键，set[] 会调用 FindEmpty() 以返回一个空槽来存储提供的对象。

索引的 get[] 部分遵循类似的逻辑。它首先使用 Find() 方法搜索指定的键。如果 Find() 返回一个非负索引，get[] 返回存储数据的 _arrayElements 的对应成员。如果 Find() 返回 -1，get[] 返回 null，表示它在列表中找不到提供的键。

Find() 方法遍历 _keys 的成员，查找与传入的字符串 targetKey 值相同的元素。Find() 返回找到元素的索引（如果未找到则返回 -1）。FindEmpty() 返回第一个没有键元素的元素的索引。

Find() 和 FindEmpty() 都不是以高效的方式编写的。有很多方法可以使这些方法更快，其中没有任何一种与索引器有关。

![](img/80ff26f06fc9ab951e1cd4257b867366_171_0.png)

请注意，你不能通过提供 null 键来移除一个元素。正如大学教材里常说的，“这个问题留给读者作为练习。”

Main() 方法以一种简单的方式演示了 Indexer 类：

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        // Create an array with enough room.
        KeyedArray ma = new KeyedArray(100);

        // Save the ages of the Simpson kids.
        ma["Bart"] = 8;
        ma["Lisa"] = 10;
        ma["Maggie"] = 2;

        // Look up the age of Lisa.
        Console.WriteLine("Let's find Lisa's age");
        int age = (int)ma["Lisa"];
        Console.WriteLine("Lisa is {0}", age);

        // Wait for user to acknowledge the results.
        Console.WriteLine("Press Enter to terminate...");
        Console.Read();
    }
}
```

该程序创建了一个长度为 100 的 KeyedArray 对象 ma（即有 100 个空闲元素）。它继续按每个孩子的名字索引存储《辛普森一家》电视节目中孩子们的年龄。最后，程序使用表达式 ma [ "Lisa" ] 检索 Lisa 的年龄并显示结果。表达式 ma [ "Lisa" ] 读作“ma 下标-Lisa。”

请注意，程序必须对从 ma [ ] 返回的值进行强制转换，因为 KeyedArray 被编写为保存任何类型的对象。如果索引器被编写为仅处理 int 值——或者如果 KeyedArray 是泛型的——则不需要强制转换。（有关泛型的更多信息，请参阅本迷你书的第 8 章。）

程序的输出简单而优雅：

```
Let's find Lisa's age
Lisa is 10
Press Enter to terminate...
```

顺带一提，IList 接口描述了一个提供类似数组的整数索引器的类，其形式为 object this[int]。C# 还有一个 IList<T> 接口，你可以用它用你选择的 type T 替换 object。这将消除前一个示例中对强制转换的需求。

有关 Indexer 程序的泛型版本，请参阅本书网站上的 IndexerGeneric 示例。

![](img/80ff26f06fc9ab951e1cd4257b867366_172_0.png)

## 在迭代器块周围循环

在 C# 的早期版本中，我们在本章“以数组方式访问集合：索引”一节中讨论的链表，是遍历集合的主要做法，就像在 C++ 和 C 中之前所做的那样。虽然这种解决方案确实有效，但事实证明 C# 2.0 已简化了此过程，使得

- 你不必调用 GetEnumerator()（并转换结果）。
- 你不必调用 MoveNext()。
- 你不必调用 Current 并转换其返回值。
- 你只需使用 foreach 来迭代集合。（C# 会在幕后为你完成剩下的工作——它甚至会编写枚举器类。）

公平地说，foreach 也适用于 .NET 中的 LinkedList 类。这来自于提供 GetEnumerator() 方法。但我仍然必须自己编写 LinkedListIterator 类。新颖之处在于，如果你选择的话，你可以在自己编写的集合类中跳过这部分。

而不是在你编写的集合类中实现所有这些接口方法，你可以提供一个迭代器块——并且你不必编写自己的迭代器类来支持集合。你也可以将迭代器块用于许多其他任务，正如我在下一个示例中向你展示的那样。

现在迭代的最佳方法使用迭代器块。当你编写一个集合类——并且对于自定义集合类（如 `KeyedList` 和 `PriorityQueue`）的需求仍然存在——你在其代码中实现迭代器块，而不是实现 `IEnumerator` 接口。然后该类的用户只需使用 `foreach` 迭代集合即可。我将一步步带你了解它，以展示迭代器块的几种变体。

本节中的每个示例都是本书网站上 `IteratorBlocks` 示例的一部分：

![](img/80ff26f06fc9ab951e1cd4257b867366_173_0.png)

```csharp
// IteratorBlocks -- Demonstrates using the C# 2.0 iterator
//     block approach to writing collection iterators
using System;
namespace IteratorBlocks
{
    class IteratorBlocks
    {
        //Main -- Demonstrate five different applications of
        // iterator blocks.
        static void Main(string[] args)
        {
            // Instantiate a MonthDays "collection" class.
            MonthDays md = new MonthDays();
            // Iterate it.
            Console.WriteLine("Stream of months:\n");
            foreach (string month in md)
            {
                Console.WriteLine(month);
            }

            // Instantiate a StringChunks "collection" class.
            StringChunks sc = new StringChunks();
            // Iterate it: prints pieces of text.
            // This iteration puts each chunk on its own line.
            Console.WriteLine("\nStream of string chunks:\n");
            foreach (string chunk in sc)
            {
                Console.WriteLine(chunk);
            }

            // And this iteration puts it all on one line.
            Console.WriteLine("\nStream of string chunks on one line:\n");
            foreach (string chunk in sc)
            {
                Console.Write(chunk);
            }
            Console.WriteLine();

            // Instantiate a YieldBreakEx "collection" class.
            YieldBreakEx yb = new YieldBreakEx();
            // Iterate it, but stop after 13.
            Console.WriteLine("\nStream of primes:\n");
```
