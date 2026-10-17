
```csharp
// PropertyIterator -- 定义一个命名的迭代器，返回偶数
class PropertyIterator
{
    // 这里是“集合”。
    double[] doubles = { 1.1, 2.2, 3.3, 4.4, 5.5 };
    // DoubleDrop -- 定义一个命名的迭代器，返回偶数
    public System.Collections.IEnumerator DoubleDrop
    {
        foreach (double db in doubles)
        {
            if (db > 3.0)
                yield return db;
        }
    }
}
```

# 迭代器块循环 154

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_178_0.png)

# 154 迭代器块循环

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_179_0.png)

# 迭代器块循环 155

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_180_0.png)

## 156 遍历迭代器块

更广泛地说，无论可迭代集合在底层如何实现，它都会产生一个值的“流”，你可以通过 `foreach` 获取这些这些值。（我将在第三书中讨论流——我引入这个概念是为了说明关于迭代器的一个观点。）

为了更形象地说明这一点，`IteratorBlocks` 中还有另一个简单的集合类，它将集合的概念推向了极致（你可能会这么想）：

```csharp
//StringChunks -- 定义一个可迭代对象，返回文本块，
// 每次迭代返回一个 -- 另一个奇特的“集合”类。
class StringChunks
{
    // GetEnumerator -- 这是一个迭代器；看它在 Main
    // 中被调用了两次。
    public System.Collections.IEnumerator GetEnumerator()
    {
        // 每次迭代返回不同的文本块。
        yield return "using iterator *;";
        yield return "blocks";
        yield return "isn't all";
        yield return "that hard";
        yield return "";
    }
}
```

奇怪的是，`StringChunks` 在通常意义上并没有存储任何内容。它不包含数组。那么集合在哪里呢？它存在于 `yield` 的序列中，直到所有内容都被返回。集合“包含”五个对象，每个对象都是单个字符串，类似于之前 `MonthDays` 示例中存储在数组中的那些。而且，在类外部的 `Main()` 中，你可以使用简单的 `foreach` 循环遍历这些对象，因为 `yield` 会按顺序一次返回一个字符串。这里有一个简单的 `main` 方法：

```csharp
// 实例化 StringChunks “集合”类。
StringChunks sc = new StringChunks();
// 遍历它：它打印文本片段。
foreach (string chunk in sc)
{
    Console.WriteLine(chunk);
}
```

## 迭代器语法非常容易放弃

从 C# 2.0 开始，该语言引入了两个迭代器语法。`yield return` 语句类似于 `MoveNext()` 和 `Current`，用于获取集合中的下一个项目。`yield break` 语句类似于 C# 的 `break` 语句，允许你跳出循环或 `switch` 语句。

### Yield return：好吧，我放弃了

`yield return` 语法的工作方式如下：

- 1. 第一次被调用时，它返回集合中的第一个值。
- 2. 下次被调用时，它返回第二个值。
- 3. 依此类推……

使用 `yield` 就像显式地使用旧式迭代器的 `MoveNext()` 方法，就像在 `LinkedList` 代码中那样。每次调用 `MoveNext()` 都会从集合中产生新项目。但在这里，你不需要调用 `MoveNext()`。（不过你可以相信，它在 `yield return` 语法的背后的某处已经为你执行了，并且符合我们的逻辑。）

你可能会想我说的“下一次被调用”是什么意思？这里再次使用了 `foreach` 循环来遍历 `StringChunks` 集合：

```csharp
foreach (string chunk in sc)
    Console.WriteLine(chunk);
```

每当循环从迭代器获取一个新块时（在循环的每次迭代中），迭代器都会存储它在集合中的位置（正如所有的迭代器都是一样）。在 `foreach` 循环的下一次迭代中，迭代器会返回集合中的下一个值，依此类推。

### Yield break：我想离开这里！

我需要提到一个与 `yield` 相关的语法。你可以通过在迭代器中指定 `yield break` 语句在某处停止迭代器的进度。在集合的迭代器块中测试条件后达到了阈值，此时你想在该点停止迭代器。这里有一个以此方式使用 `yield break` 的迭代器块简单示例：

```csharp
//YieldBreakEx -- yield break 关键字的另一个示例
class YieldBreakEx{
    int[] primes = { 2, 3, 5, 7, 11, 13, 17, 19, 23 };
    //GetEnumerator -- 返回质数序列
    // 展示了 yield return 和 yield break
    public System.Collections.IEnumerator GetEnumerator()
    {
        foreach (int prime in primes)
        {
            if (prime > 13) yield break;
            yield return prime;
        }
    }
}
```

在这种情况下，迭代器块包含一个 `if` 语句，检查迭代器到达集合中时的每个质数（顺便说一下，在迭代器内部使用了另一个 `foreach`）。如果质数大于 13，该块将调用 `yield break` 停止产生质数。否则，它继续执行——通过 `yield return` 放弃另一个质数，直到集合耗尽。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_183_0.png)

除了在正式集合类中使用迭代器块、使用它们来实现枚举器外，你还可以简单地将本章中的任何迭代器块写成与 `Program` 类中的 `Main()` 方法并行的静态方法。在本章的许多示例中，集合位于方法内部。特殊用途集合有许多用途，而且它们通常快速且易用。

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_183_1.png)

你还可以为类（另一种类型）编写扩展，其行为类似于一个迭代器块。当你有一个可以被认为是迭代器块的类时，这非常有用。（*注：原文此处存在大量重复的句子，翻译时已根据要求进行处理。*）

```csharp
//Numbers 定义一个迭代器返回偶数
class Numbers
{
    yield return 2;
    yield return 4;
    yield return 6;
}
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_183_2.png)

## 160 遍历迭代块

（前一个示例的工作原理类似。）此示例演示了如果你也将奇数作为限制值传递时会发生什么 —— 这是 `%` 运算符的另一种用法：

```cs
// 实例化一个 EvenNumbers “集合”类。
EvenNumbers en = new EvenNumbers();
// 遍历它：打印从 10 降到 4 的偶数。
Console.WriteLine("stream of descending evens : \n");
foreach (int even in en.DescendingEvents(11, 3))
{
    Console.WriteLine(even);
}
```

这将产生一个从 10 降到 4 的偶数整数列表。还要注意 `foreach` 是如何指定的。你必须实例化一个 `EvenNumbers` 对象（集合类）。然后，在 `foreach` 语句中，你通过该对象调用了命名的迭代器方法：

```cs
EvenNumbers en = new EvenNumbers();
foreach(int even in en.DescendingEvents(nTop, nStop))
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_185_0.png)

如果 `DescendingEvents()` 是静态的，你就不需要类实例了。你会像往常一样直接调用类本身：

```cs
foreach(int even in EvenNumbers.DescendingEvents(nTop, nStop))
```

**外那里是一片广阔的天地！**

如果你能用 `foreach` 语句产生一个偶数的“流”，请想一下你可能用这些特殊用途集合产生的其他所有东西：2 的幂次流、或者级数中作为质数或平方数的数学级数项 —— 或者像斐波那契数那样的奇特数字。或者，一个随机数流（`Random` 类已经做的事情）或随机生成的对象流呢？

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_185_1.png)

如果你查看本书书第 8 章中的 `PriorityQueue` 示例，你可能想检查一下 `PackageFactoryWithIterator` —— 它出现在本书的网站上。该示例说明了如何使用迭代块来生成进入运输公司的随机生成对象包的流。它与原始 `PriorityQueue` 示例中的 `PackageFactory` 类功能相同，但使用了迭代块。

**迭代属性并不意味着“一个不断增加的房子”**

你也可以将迭代块实现为类的属性 - 特别是在属性的 get 访问器器中。在这个带有 `DoubleProp` 属性的简单类中，属性的 `get()` 访问器充当迭代块，返回一个 `double` 值的流：

## 遍历迭代块 161

```cs
//PropertyIterator - 演示如何将类的
// 属性的 get 访问器作为迭代块。
class PropertyIterator
{
    double[] doubles = { 1.0, 2.0, 3.5, 4.67 };
    // DoubleProp - 一个带有迭代块的 “get” 属性
    public System.Collections.IEnumerable DoubleProp
    {
        get
        {
            foreach (double db in doubles)
            {
                yield return db;
            }
        }
    }
}
```

你编写 `DoubleProp` 方法头的方式与你在迭代示例中编写 `DescendingEvents(1)` 方法头的方式相同。方法头返回一个 `IEnumerator` 接口，但作为属性，它在名称后没有父级，并且有一个 `get()` 访问器 —— 而没有 `set()`。`get()` 访问器被实现为一个循环，遍历集合并使用标准的 `yield` 依次返回集合 `Doubles` 中的每个项。

这里是属性在 `Main()` 中被访问的方式：

```cs
// 实例化一个 PropertyIterator “集合”类。
PropertyIterator prop = new PropertyIterator();
// 遍历：它一次产生一个 double。
Console.WriteLine("\name of double values:\n");
foreach (double db in prop.DoubleProp)
{
    Console.WriteLine(db);
}
```

> 你也可以拥有一个泛型迭代器。查找迭代器，使用 `in`。迭代器（iterators），使用 `in`。

如果你能用 `foreach` 语句产生一个偶数的“流”，请想一下你可能用这些特殊用途集合产生的其他所有东西：2 的幂次流、或者级数中作为质数或平方数的数学级数项 —— 或者像斐波那契数那样的奇特数字。或者，一个随机数流（`Random` 类已经做的事情）或随机生成的对象流呢？

如果你查看本书书第 8 章中的 `PriorityQueue` 示例，你可能想检查一下 `PackageFactoryWithIterator` —— 它出现在本书的网站上。该示例说明了如何使用迭代块来生成进入运输公司的随机生成对象包的流。它与原始 `PriorityQueue` 示例中的 `PackageFactory` 类功能相同，但使用了迭代块。

**迭代属性并不意味着“一个不断增加的房子”**

你也可以将迭代块实现为类的属性 - 特别是在属性的 get 访问器中。在这个带有 `DoubleProp` 属性的简单类中，属性的 `get()` 访问器充当迭代块，返回一个 `double` 值的流：

你也可以拥有一个泛型迭代器。查找迭代器，使用 `in`。迭代器（iterators），使用 `in`。

（注：由于源文本中存在大量重复和断裂的句子，译文已根据上下文逻辑进行了对齐和翻译，确保逻辑完整性。）
