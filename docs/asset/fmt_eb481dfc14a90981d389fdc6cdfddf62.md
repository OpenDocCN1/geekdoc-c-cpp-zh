
## 输出 16.1

`abstract` `as` `base` `bool` `break` `byte` `case` `catch` `char` `checked` `class` `const` `continue` `decimal` `default` `delegate` `do` `double` `else` `enum` `event` `explicit` `extern` `false` `finally` `fixed` `float` `for` `foreach` `goto` `if` `implicit` `in` `int` `interface` `internal` `is` `lock` `long` `namespace` `new` `null` `object` `operator` `out` `override` `params` `private` `protected` `public` `readonly` `ref` `return` `sbyte` `sealed` `short` `sizeof` `stackalloc` `static` `string` `struct` `switch` `this` `throw` `true` `try` `typeof` `uint` `ulong` `unchecked` `unsafe` `ushort` `using` `virtual` `void` `volatile` `while`

在此查询表达式中，`selection` 被赋值为 C# 保留关键字的集合。此示例中的查询表达式包含一个 `where` 子句，用于过滤掉非上下文关键字。

查询表达式始终以 `from` 子句开始，并以 `select` 子句或 `group` 子句结束，分别由上下文关键字 `from`、`select` 或 `group` 标识。`from` 子句中的标识符 `word` 被称为`范围变量`；它代表集合中的每个项，正如 `foreach` 循环中的循环变量代表集合中的每个项一样。

熟悉 SQL 的开发人员会注意到，查询表达式的语法与 SQL 相似。这种设计是刻意为之——目的是让已经熟悉 SQL 的程序员更容易学习 LINQ。然而，存在一些明显的差异。大多数有 SQL 经验的开发人员首先会注意到的是，此处展示的 C# 查询表达式中子句的顺序为：先是 `from`，然后是 `where`，最后是 `select`。等效的 SQL 查询将 `SELECT` 子句放在首位，然后是 `FROM` 子句，最后是 `WHERE` 子句。

改变这一顺序的一个原因是为了启用 IntelliSense，这是 IDE 的一项功能，编辑器通过它生成有用的用户界面元素，例如描述给定对象成员的列表。由于 `from` 出现在首位并标识字符串数组 `Keywords` 作为数据源，代码编辑器可以推断出范围变量 `word` 的类型为 `string`。当你在编辑器中输入代码并到达 `word` 后面的点时，编辑器将仅显示 `string` 的成员。

如果 `from` 子句出现在 `select` 之后，如 SQL 中那样，当你在查询中输入时，编辑器不知道 `word` 的数据类型，因此无法显示 `word` 成员列表。例如，在示例 16.1 中，将无法预测 `Contains()` 是 `word` 的一个可能成员。

C# 查询表达式的顺序也更紧密地符合逻辑上执行操作的顺序。在评估查询时，你首先标识集合（由 `from` 子句描述），然后筛选出不需要的项（通过 `where` 子句），最后描述所需结果（通过 `select` 子句）。

最后，C# 查询表达式的顺序确保了“where”（范围）变量的作用域规则与局部变量的作用域规则大致一致。例如，（范围）变量必须由某个子句（通常是 `from` 子句）声明后才能使用，这就像局部变量在使用前必须始终被声明一样。

### 投影

查询表达式的结果是类型为 `IEnumerable<T>` 或 `IQueryable<T>` 的集合。实际类型 `T` 是从 `select` 或 `group by` 子句推断出来的。例如，在示例 16.1 中，编译器知道 `Keywords` 的类型为 `string[]`，它可以转换为 `IEnumerable<string>`，并推断出 `word` 因此类型为 `string`。查询以 `select word` 结尾，这意味着查询表达式的结果必须是字符串集合，因此查询表达式的类型为 `IEnumerable<string>`。

- 1. 实际上，查询表达式的结果几乎总是 `IEnumerable<T>` 或其派生类型。虽然创建返回其他类型的查询方法实现是合法的，但有些不合理；语言中*没有要求*查询表达式的结果必须可转换为 `IEnumerable<T>`。

在这种情况下，查询的“输入”和“输出”都是字符串集合。然而，如果 *select* 子句中的表达式类型完全不同，输出类型可能与输入类型有很大不同。请考虑示例 16.2 中的查询表达式及其在输出 16.2 中对应的输出。

#### 示例 16.2：使用查询表达式进行投影

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.IO;
// ...
static void List1(string rootDirectory, string searchPattern)
{
    IEnumerable<string> fileNames = Directory.GetFiles(
        rootDirectory, searchPattern);
    IEnumerable<FileInfo> fileInfos =
        from fileName in fileNames
        select new FileInfo(fileName);
    foreach (FileInfo fileInfo in fileInfos)
    {
        Console.WriteLine(
            "{0} {1}", fileInfo.Name, fileInfo.LastWriteTime);
    }
}
```

**输出 16.2**

```
Account.cs (11/22/2011 11:56:11 AM)
Bill.cs (8/10/2011 9:33:55 PM)
Contact.cs (8/19/2011 11:40:30 PM)
Customer.cs (11/17/2011 2:02:52 AM)
Employee.cs (8/17/2011 1:33:22 AM)
Person.cs (10/22/2011 10:00:03 PM)
```

此查询表达式产生的结果是 `IEnumerable<FileInfo>`，而不是 `Directory.GetFiles()` 返回的 `IEnumerable<string>` 数据类型。查询表达式的 select 子句可能会投影出与 from 子句表达式收集的数据类型不同的数据类型。

![](img/ef6a8a417630b222bfb3f3b949facff0_697_0.png)

在本例中，选择 FileInfo 类型是因为它具有所需输出的两个相关字段：文件名和最后写入时间。如果你需要 FileInfo 对象中未包含的其他信息，可能就没有这样方便的数据类型了。元组（或在 C# 7.0 之前的匿名类型）提供了一种便捷且简洁的方式，让你能够投影出恰好所需的数据，而无需查找或创建显式类型。列表 16.3 提供了与列表 16.2 相似的输出，但通过元组语法而非 FileInfo 实现。

## 列表 16.3：查询表达式中的元组

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

### 初学者主题

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

```
Query created.
add* alias* ascending* async* await* by* descending* dynamic* equals* from* get* global* group* into* join* let* nameof* on* orderby* partial* remove* select* set* value* var* where* yield*
```

在列表 16.4 中，`foreach` 循环内没有输出空格。当执行谓词 `IsKeyword()` 时打印空格的副作用发生在查询被遍历时——而不是查询创建时。因此，尽管 `selection` 是一个集合（毕竟它的类型是 `IEnumerable<T>`），但在赋值时，`from` 子句之后的所有内容都构成了选择标准。直到我们开始遍历 `selection` 时，这些标准才会被应用。

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
