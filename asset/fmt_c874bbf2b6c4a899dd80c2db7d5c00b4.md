
*（注：168-169 页的 OCR 文本包含大量的损坏/乱码。我根据标准的 C# 迭代器模式以及源文本提供的剩余碎片重建了逻辑流，因为提供的这些页面的 OCR 内容在很大程度上是不可读的或重复的同步步调风格解构。以下是清理后的章节。）*

# 迭代遍历 foreach 集合：迭代器 143

应用代码可以为同一个集合创建多个独立的迭代器对象。由于迭代器包含它自己的状态信息（在迭代器内部“知道自己所处的位置”），因此每个迭代器都可以独立地遍历集合。它可以同时运行多个迭代器，且每个迭代器都处于集合中的不同位置。

# 索引器程序示例

索引类型不仅限于 `int`。你可以选择通过房屋所有者的名称、房屋地址或任何数量的索引对一组房屋进行索引。此外，索引器属性可以重载为多种类型，因此你可以在同一个集合中索引各种元素。

以下 `Indexer` 程序生成了虚拟数组类 `KeyedArray`。这个虚拟数组看起来和用就像一个数组，它使用字符串值作为索引：

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_171_0.png)

```csharp
// Indexer 此程序演示了如何使用索引运算符
// 使用字符串作为索引提供数组。
// 此版本是非图形化的，请参见 IndexerGeneric 示例。
using System;
namespace Indexer
public class KeyedArray
{
    // 下面的字符串提供了数组的“键”
    // 键是用于标识元素的字符串。
    private string[] _keys;

    // 对象存储了与该键关联的实际数据。
    private object[] _arrayElements;

    // KeyedArray -- 创建一个固定大小的 KeyedArray。
    public KeyedArray(int size)
    {
        _keys = new string[size];
        _arrayElements = new object[size];
    }

    // Find -- 找到与目标字符串 targetKey 对应的元素
    // 索引（如果找不到则返回负值）。
    private int Find(string targetKey)
    {
        for(int i = 0; i < _keys.Length; i++)
        {
            if (String.Compare(_keys[i], targetKey) == 0)
            {
                return i;
            }
        }
        return -1;
    }

    // FindEmpty -- 在数组中为新条目寻找空间。
    private int FindEmpty()
    {
        for(int i = 0; i < _keys.Length; i++)
        {
            if (_keys[i] == null)
            {
                return i;
            }
        }
        throw new Exception("Array is full");
    }

    // 通过字符串键查找内容 —— 这索引器。
    public object this[string key]
    {
        set
        {
            // 检查字符串是否已存在。
            int index = Find(key);
            if (index < 0)
            {
                // 不存在 - 寻找新位置。
                index = FindEmpty();
                _keys[index] = key;
            }
            // 将对象保存在对应的位置。
            _arrayElements[index] = value;
        }
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
        // 创建空间足够的数组。
        KeyedArray ma = new KeyedArray(100);
        // 保存辛普森家孩子们的年龄。
        ma["Bart"] = 8;
        ma["Lisa"] = 10;
        ma["Maggie"] = 2;
        // 查找 Lisa 的年龄。
        Console.WriteLine("Let's find Lisa's age");
        int age = (int)ma["Lisa"];
        Console.WriteLine("Lisa is {0}", age);
        // 等待用户确认结果。
        Console.WriteLine("Press Enter to terminate...*
        Console.Read();
    }
}
```

`KeyedArray` 类持有两个普通数组。`_arrayElements` 对象数组包含了实际的 `KeyedArray` 数据。填充 `_keys` 数组的字符串作为对象数组的标识符。`_keys` 的第 $i$ 个元素对应 `_arrayElements` 的第 $i$ 个条目。应用程序可以通过对应用有意义的字符串标识对 `KeyedArray` 进行索引。

非整数索引被称为“键”。顺便说一下，你可以使用 `List<T>` 代替固定大小数组来实现 `KeyedArray`。`List<T>` 数组一样可以索引，因为它们都实现了 `IList`（或 `IList<T>`）接口。这使得 `KeyedArray` 可以是泛型，并且比使用内部数组灵活得多。

`[string]` 索引器首先通过调用 `Find()` 方法检查指定的索引是否已存在。`Find()` 返回一个索引，`set[]` 将新数据对象返回 `_arrayElements` 中对应的索引。如果 `Find()` 找不到键，`get[]` 会调用 `FindEmpty` 返回一个空槽来存储提供的对象。

`get[]` 索引遵循类似的逻辑。它使用 `Find()` 方法搜索指定的键。如果 `Find()` 返回非负索引，`get()` 返回 `_arrayElements` 中存储数据的对应成员。如果 `Find()` 返回 `-1`，`get()` 返回 `null`，表示在列表的任何地方都找不到提供的键。

`Find()` 方法遍历 `_keys` 的成员，寻找与传入的字符串 `targetKey` 值相同的元素。`Find()` 返回元素的索引（如果未找到则返回 `-1`）。`FindEmpty()` 返回第一个没有键元素的索引。

`Find()` 和 `FindEmpty()` 的写法都不够高效。有许多方法可以使这些方法运行更快，但其中任何方法都与索引器无关。

嘿，为 `LinkedList` 类有一个索引器不是很酷吗？当然，你可以这样做，但你必须遍历底层的 `_keys` 数组来定位指定的键 ——这就是我提供 `Find()` 和 `FindEmpty()` 的原因，它们正是这么做的。你还必须通过遍历列表来为 `LinkedList` 实现索引器，而唯一的方法是遵循从节点到节点的正向链接。索引器会很方便，但不会提高速度。

注意，你不能通过提供 `null` 键来删除元素。以前在大学教科书中经常说：“这个问题留给读者练习。”

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_173_0.png)

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_173_1.png)

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_173_2.png)

# 迭代器块循环 151

正如我在下一个示例中所示，你也可以将迭代器块用于许多其他任务。

目前最佳迭代方法是使用迭代器块。当你编写一个集合类时——尽管仍然需要像 `KeyList` 和 `PriorityQueue` 这样的自定义集合类——你应该在代码中实现迭代器块，而不是实现 `IEnumerator` 接口。该该类的用户可以直接使用 `foreach` 遍历集合。我将逐一讲解，向你展示迭代器块的几种变体。

本节中的每个示例都是本书网站上 `IteratorBlocks` 示例的一部分：

```csharp
// IteratorBlocks -- 展示了使用 C# 2.0 迭代器
// 块编写集合迭代器的方法
using System;
namespace IteratorBlocks
class IteratorBlocks
{
    //Main 展示迭代器块的五种应用。
    static void main(string[] args)
    {
        // 实例化 MonthDays "集合" 类。
        MonthDays md = new MonthDays();
        // 遍历它。
        Console.WriteLine("Stream of months:\n");
        foreach (string month in md)
        {
            Console.WriteLine(month);
        }

        // 实例化 StringChunks "集合" 类。
        StringChunks sc = new StringChunks();
        // 遍历它；它将每个块放在单独的一行。
        Console.WriteLine("\nstream of string chunks:\n");
        foreach (string chunk in sc)
        {
            Console.WriteLine(chunk);
        }
        // 这种迭代将所有内容放在同一行上。
        Console.WriteLine("\nstream of string chunks on one line:\n");
        foreach (string chunk in sc)
        {
            Console.Write(chunk);
        }

        // 实例化 YieldBreak "集合" 类。
        YieldBreak yb = new YieldBreak();
        // 遍历它；但在 13 之后停止。
        Console.WriteLine("\nstream of primes:\n");
        foreach (int prime in yb)
        {
            Console.WriteLine(prime);
        }
    }
}
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_176_0.png)

第一部分

第 7 章

逐步执行

## 152 迭代器块循环

```csharp
// 实例化 EvenNumbers '集合' 类。
EvenNumbers en = new EvenNumbers();
// 遍历：打印从 10 降到 4 的偶数。
Console.WriteLine("instream of descending evens \n");
foreach (int i in en.DescendingEvens(10, 3))
{
    Console.WriteLine(i);
}
```

```csharp
// 实例化 PropertyIterator '集合' 类。
PropertyIterator prop = new PropertyIterator();
// 遍历：一次产生一个 double 类型。
Console.WriteLine("instream of double values:\n");
foreach (double db in prop.DoubleDrop)
{
    Console.WriteLine(db);
}
```

```csharp
// 等待用户确认。
Console.WriteLine("Press enter to terminate...");
Console.Read();
```

```csharp
// 定义一个迭代器，返回月份
// 以及它们对应的天数长度——类似于“集合”类。
class MonthDays
{
    // 这里是“集合”。
    string[] months = {
        "January 31", "February 28", "March 31",
        "April 30", "May 31", "June 30", "July 31",
        "August 31", "September 30", "October 31",
        "November 30", "December 31";
    };

    // GetEnumerator - 这里是迭代器。看它如何在 Main() 中
    // 通过 foreach 被调用：
    public System.Collections.IEnumerator GetEnumerator()
    {
        foreach (string month in months)
        {
            // 每次迭代返回一个月份。
            yield month;
        }
    }
}
```

```csharp
// 定义一个迭代器，返回文本块，
// 每次迭代返回一个——另一个特殊的“集合”类。
class StringChunks
{
    // GetEnumerator - 这是一个迭代器；看它如何在 Main 中
    // 被调用（两次）。
    public System.Collections.IEnumerator GetEnumerator()
    {
        // 每次迭代返回一个文本块。
        yield return "blocks";
        yield return "isn't all";
        yield return "that hard";
        yield return "";
    }
}
```

## 迭代器块循环 153

```csharp
//YieldBreakEx -- yield break 关键字的另一个示例
class YieldBreakEx
{
    int[] primes = { 2, 3, 5, 7, 11, 13, 17, 19, 23 };
    //GetEnumerator -- 返回一个质数序列
    // 展示了 yield return 和 yield break
    public System.Collections.IEnumerator GetEnumerator()
    {
        foreach (int prime in primes)
        {
            if (prime > 13)
                yield break;
            yield return prime;
        }
    }
}
```

```csharp
//EvenNumbers -- 定义一个命名的迭代器，返回从你传入的
//“顶部”值向下到“停止”值之间的偶数。
// 另一个特殊的“集合”类
class EvenNumbers
{
    // DescendingEvens -- 定义一个命名的迭代器，返回
    // 从你传入的“顶部”值向下到“停止”值的偶数。
    public System.Collections.IEnumerator DescendingEvens(int top, int stop)
    {
        for (int i = top; i >= stop; i--)
        {
            if (i % 2 == 0)
                yield return i;
        }
    }
}
```
