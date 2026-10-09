

在本例中，选择 FileInfo 类型是因为它具有所需输出的两个相关字段：文件名和最后写入时间。如果你需要 FileInfo 对象中未包含的其他信息，可能就没有这样方便的数据类型了。元组（或在 C# 7.0 之前的匿名类型）提供了一种便捷且简洁的方式，让你能够投影出恰好所需的数据，而无需查找或创建显式类型。列表 16.3 提供了与列表 16.2 相似的输出，但通过元组语法而非 FileInfo 实现。

## **列表 16.3：查询表达式中的元组**

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.IO;

// ...

static void List2(string rootDirectory, string searchPattern)
{
    var fileNames = Directory.EnumerateFiles(
        rootDirectory, searchPattern);
    var fileResults =
        from fileName in fileNames
        select
        (
            Name: fileName,
            LastWriteTime: File.GetLastWriteTime(fileName)
        );

    foreach (var fileResult in fileResults)
    {
        Console.WriteLine(
            $"{fileResult.Name} ({fileResult.LastWriteTime})");
    }
}

// ...
```

在此示例中，查询仅投影出文件名及其最后文件写入时间。像列表 16.3 中这样的投影，在操作小对象（如 FileInfo）时差别不大。然而，当数据量大且获取成本高昂（例如通过互联网从另一台计算机获取）时，“横向”投影（即筛选集合中每个项目相关数据量的功能）就极其强大。使用元组（或 C# 7.0 之前的匿名类型），可以避免在查询执行时检索所有数据，而是能够仅将所需数据存储到集合中并从中检索。

例如，想象一个大型数据库，其中包含具有 30 列或更多列的表。如果没有元组，开发人员要么必须使用包含不必要信息的对象，要么必须定义小的专用类，这些类仅用于存储所需的具体数据。而元组允许编译器定义类型——这些类型仅包含其即时场景所需的数据。其他场景可以拥有仅包含该场景所需属性的不同投影。

## 初学者主题

### 查询表达式的延迟执行

使用查询表达式符号编写的查询表现出延迟执行特性，正如第 15 章中编写的查询一样。再次考虑列表 16.1 中将查询对象赋值给变量 `selection`。创建查询并将其赋值给变量并不会执行查询；相反，它们只是构建一个代表查询的对象。在创建查询对象时，并不会调用 `word.Contains(" * ")` 方法。相反，查询表达式保存了选择标准，以便在遍历由 `selection` 变量标识的集合时使用。

为了说明这一点，请参考列表 16.4 及其对应的输出（输出 16.3）。

## 列表 16.4：延迟执行和查询表达式（示例 1）

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

// ...

private static void ShowContextualKeywords2()
{
    IEnumerable<string> selection = from word in Keywords
                                    where IsKeyword(word)
                                    select word;

    Console.WriteLine("Query created.");

    foreach (string keyword in selection)
    {
        // No space output here
        Console.Write(keyword);
    }

    // The side effect of console output is included
    // in the predicate to demonstrate deferred execution;
    // predicates with side effects are a poor practice in
    // production code
    private static bool IsKeyword(string word)
    {
        if (word.Contains(' '))
        {
            Console.Write(" ");
            return true;
        }
        else
        {
            return false;
        }
    }
    // ...
}
```

## 输出 16.3

Query created.
add\* alias\* ascending\* async\* await\* by\* descending\* dynamic\* equals\* from\* get\* global\* group\* into\* join\* let\* nameof\* on\* orderby\* partial\* remove\* select\* set\* value\* var\* where\* yield\*

在列表 16.4 中，foreach 循环内没有输出空格。当执行谓词 IsKeyword() 时打印空格的副作用发生在查询被遍历时——而不是查询创建时。因此，尽管 selection 是一个集合（毕竟它的类型是 IEnumerable<T>），但在赋值时，from 子句之后的所有内容都构成了选择标准。直到我们开始遍历 selection 时，这些标准才会被应用。

现在考虑第二个示例（参见列表 16.5 和输出 16.4）。

## 列表 16.5：延迟执行和查询表达式（示例 2）

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

// ...

private static void CountContextualKeywords()
{
    int delegateInvocations = 0;
    Func<string, string> func =
        text =>
        {
            delegateInvocations++;
            return text;
        };

    IEnumerable<string> selection =
        from keyword in Keywords
        where keyword.Contains('*')
        select func(keyword);

    Console.WriteLine(
        $"1. delegateInvocations={delegateInvocations}");

    // Executing count should invoke func once for
    // each item selected
    Console.WriteLine(
        $"2. Contextual keyword count={selection.Count()}");

    Console.WriteLine(
        $"3. delegateInvocations={delegateInvocations}");

    // Executing count should invoke func once for
    // each item selected
    Console.WriteLine(
        $"4. Contextual keyword count={selection.Count()}");

    Console.WriteLine(
        $"5. delegateInvocations={delegateInvocations}");

    // Cache the value so future counts will not trigger
    // another invocation of the query
    List<string> selectionCache = selection.ToList();

    Console.WriteLine(
        $"6. delegateInvocations={delegateInvocations}");

    // Retrieve the count from the cached collection
    Console.WriteLine(
        $"7. selectionCache count={selectionCache.Count()}");

    Console.WriteLine(
        $"8. delegateInvocations={delegateInvocations}");
}
```

## 输出 16.4

1. delegateInvocations=0
2. Contextual keyword count=27
3. delegateInvocations=27
4. Contextual keyword count=27
5. delegateInvocations=54
6. delegateInvocations=81
7. selectionCache count=27
8. delegateInvocations=81

列表 16.5 没有定义单独的方法，而是使用了一个语句 lambda 来统计方法被调用的次数。

输出中有三点值得关注。首先，请注意在 `selection` 被赋值后，`DelegateInvocations` 仍保持为零。在赋值给 `selection` 时，并未对 `Keywords` 进行遍历。如果 `Keywords` 是一个属性，属性调用将会运行——换句话说，`from` 子句在赋值时执行。然而，无论是投影、筛选还是 `from` 子句之后的任何内容，直到代码遍历 `selection` 中的值之前都不会执行。这就好像在赋值时，将 `selection` 称为“查询”更为合适。

然而，一旦我们调用 `Count()`，像 `selection` 或 `items` 这样指示容器或集合的术语就是合适的，因为我们开始统计集合中的项目。换句话说，变量 `selection` 具有双重用途：保存查询信息并充当从中检索数据的容器。

第二个值得注意的重要特征是，两次调用 `Count()` 会导致 `func` 再次对每个选定项目调用一次。鉴于 `selection` 既表现为查询又表现为集合，请求计数需要再次通过遍历 `selection` 引用的 `IEnumerable<string>` 集合并统计项目来执行查询。C# 编译器不知道是否有人修改了数组中的字符串，导致计数结果不同，因此为了确保答案正确且最新，每次都需要重新进行计数。同样，对 `selection` 的 `foreach` 循环也会触发对每个项目再次调用 `func`。通过 `System.Linq.Enumerable` 提供的其他所有扩展方法也是如此。

