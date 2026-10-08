

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

