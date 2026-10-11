
```csharp
if(word.Contains("*"))
{
    Console.Write(" ");
    return true;
}
else
{
    return false;
}
```
///...

```
OUTPUT 16.3
```
Query created.
alias+= ascending* async* await* by* descending* dynamic*
equals+= from* get* global* into* join* let* nameof* nonnull*
on* order* partial* remove* select* set* value* var* where* when*
yield*
```

## 介绍查询表达式 817

在列表 16.4 中，`foreach`循环内部没有输出空格。当执行谓词`IsKeyword()`时打印空格的副作用发生在迭代查询时——而不是在创建查询时。因此，尽管`selection`是一个集合（毕竟它的类型是`IEnumerable<T>`），但在赋值时，`from`子句之后的所有内容都作为选择标准。只有当我们开始开始迭代`selection`时，这些标准才被应用。

现在考虑第二个示例（参见列表 16.5 和输出 16.4）。

### 列表 16.5：延迟执行与查询表达式（示例 2）

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
// ...
private static void CountContextualKeywords()
{
    int delegateInvocations = 0;
    string func(string text)
    {
        delegateInvocations++;
        return text;
    }
```
```csharp
IEnumerable<string> selection = from word in CSharp.Keywords
                                where word.Contains("*")
                                select func(word);
Console.WriteLine("Query created.");
foreach (string keyword in selection)
{
    // 这里没有输出空格
    Console.Write(keyword);
}
```

```
OUTPUT 16.4
```
Query created.
alias+= ascending* async* await* by* descending* dynamic*
equals+= from* get* global* into* join* let* nameof* nonnull*
on* order* partial* remove* select* set* value* var* where* when*
yield*
```

（注：列表 16.5 的 文本在源文件中略有破碎，我们根据常见的 C# 模式和可用片段重构了代码块。）

# 过滤

在列表 16.1 中，有一个子句过滤掉了保留关键字，但没有过滤上下文关键字。该子句对集合进行“垂直”过滤：如果你将集合视为一个垂直的项目列表，`where`子句会使该列表变短，从而让集合包含更少项。过滤标准通过谓词表达式——即返回`bool`的 Lambda 表达式，例如列表 16.1 中的`.Contains()`，或者`File.GetLastWriteTime(fileName) < DateTime.Now.AddMonths(-1)`。后者出现在列表 16.6 中，其输出结果出现在输出 16.5 中。

### 列表 16.6：使用 where 的查询表达式过滤

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
//
public static void FindMonthOldFiles(
    string rootDirectory, string searchPattern)
{
    IEnumerable<FileInfo> files =
        from fileName in Directory.EnumerateFiles(
            rootDirectory, searchPattern)
        where File.GetLastWriteTime(fileName) <
            DateTime.Now.AddMonths(-1)
        select new FileInfo(fileName);
    foreach (FileInfo file in files)
    {
        // 为了简化，假设当前目录是
        // rootDirectory 的子目录
        string relativePath = file.FullName.Substring(
            Directory.GetCurrentDirectory().Length);
        Console.WriteLine(
            $"{relativePath} ({file.LastWriteTime})");
    }
}
//...
```

### 输出 16.5

```
\TestData\Bill.cs (8/10/2011 9:33:55 PM)
\TestData\Contact.cs (8/19/2011 11:40:30 PM)
\TestData\Employee.cs (8/17/2011 1:33:22 AM)
\TestData\Person.cs (10/22/2011 10:00:03)
```

# 排序

要使用查询表达式对项进行排序，可以使用`orderby`子句，如列表 16.7 所示。

### 列表 16.7：使用 orderBy 子句通过查询表达式排序

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.IO;
// ...
public static void ListByFileSize(
    string rootDirectory, string searchPattern)
{
    IEnumerable<string> fileNames =
        from fileName in Directory.EnumerateFiles(
            rootDir, searchPattern)
        orderby (new FileInfo(fileName)).Length descending,
        select fileName;
    foreach (string fileName in fileNames)
    {
        Console.WriteLine(fileName);
    }
// ...
```

列表 16.7 使用`orderby`子句对`Directory.GetFiles()`返回的文件进行排序，首先按文件大小降序排列，然后按文件名升序排列。多个排序标准由逗号分隔，以便项首先按大小排序，如果大小相同，则按文件名排序。`ascending`和`descending`是指示排序方向的上下文关键字。指定排序顺序为升序或降序是可选的；如果省略方向（如在此处的`fileName`处），则默认为升序。

# let 子句

列表 16.8 包含一个与列表 16.7 中的查询非常相似的查询，不同之处在于类型参数`IEnumerable<T>`是`FileInfo`。然而，该查询存在一个问题：我们必须`orderby`子句和`select`子句中冗余地创建了两次`FileInfo`。

### 列表 16.8：投影 FileInfo 集合并按文件大小排序

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.IO;
//
public static void ListFileSize2(
    string rootDirectory, string searchPattern)
{
    IEnumerable<FileInfo> files =
        from fileName in Directory.EnumerateFiles(
            rootDirectory, searchPattern)
        orderby new FileInfo(fileName).Length, fileName
        select new FileInfo(fileName);
    foreach (FileInfo file in files)
    {
        // 为了简化，假设当前目录
        // 是 rootDirectory 的子目录
        string relativePath = file.FileName.Substring(
            Directory.GetCurrentDirectory().Length);
        Console.WriteLine(
            $"{relativePath}} {file.Length}}");
    }
}
//
```

遗憾的是，尽管结果是正确的，但列表 16.8 最终为源集合中的每个项都实例化了两次`FileInfo`，这是浪费且没有必要的。为了避免这种不必要的且可能昂贵的开销，你可以使用`let`子句，如列表 16.9 所示。

`let`子句引入了一个新的范围变量，它可以持有在整个查询表达式剩余部分使用的表达式的值。你可以根据需要添加任意`let`子句；只需将其作为额外的子句插入到第一个`from`子句之后、最后的`select`子句之前。

### 列表 16.9：查询表达式中的结果排序

```csharp
//...
IEnumerable<FileInfo> files =
    from fileName in Directory.EnumerateFiles(
        rootDirectory, searchPattern)
    let file = new FileInfo(fileName)
    order by file.Length, fileName
    select file;
//...
```

# 分组

一种常见的数据处理场景是相关项分组。在 SQL 中，这通常涉及`group by`子句。然而，LINQ 产生一个分组序列，其中项被分组成集合。例如，列表 16.10 和输出 16.6 展示了如何进行分组。

### 列表 16.10：分组

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
//
    public static void GroupKeywords()
    {
        IEnumerable<IGrouping<bool, string>> selection =
            from word in CSharp.Keywords
            group word by word.Contains('*');
        foreach (IGrouping<bool, string> wordGroup
        in selection)
        {
            Console.WriteLine(Environment.NewLine + "{0}:",
                wordGroup.Key ? "Contextual Keywords" : "Keywords");
            foreach (string keyword in wordGroup)
            {
                Console.Write(" " + keyword.Replace("*", null));
            }
        }
    }
//...
```

### 输出 16.6

Keywords:
  Contextual Keywords
  Keywords

ushort using virtual unchecked void volatile while
上下文关键字：
add aliases ascending async by descending dynamic equals from
get global group join let nameof nonnull on orderby partial remove
select set value where yield

`group`子句的结果会产生一个产生`IGrouping<TKey, TElement>`对象集合的查询——这与`GroupBy`标准查询操作符所做的相同（参见第 15 章）。后续查询中的`select`子句使用一个元组来有效地将`IGrouping<TKey, TElement>.Key`重命名为`IsContextualKeyword`，并将子集合属性重命名为`Items`。通过此更改，嵌套循环使用`wordGroup.Items`而不是直接使用`wordGroup`。元组中可以添加的另一个潜在项是子集合中项目的计数。然而，此功能已经通过 LINQ 的`wordGroup.Items.Count()`方法可用，因此直接将其添加到匿名类型中的好处尚待商榷。

## 使用 `into` 延续查询

正如你在示例 16.11 中所看到的的，你可以将现有的查询作为第二个查询的输入。但是，当你想要将一个查询的结果作为另一个查询的输入时，并没有必要编写一个完全新的查询表达式。你可以使用上下文关键字`into`通过查询延续子句来扩展任何查询。查询延续无非是创建两个查询并将第一个作为第二个的法的法的语法糖。由`into`子句引入的范围变量（示例 16.11 中的`groups`）将成为查询剩余部分的范围变量；任何之前的范围变量在逻辑上都是属于早先查询的，不能在查询延续中使用。示例 16.12 重写了示例 16.11 的代码，以使用两个查询的查询延续。

### 示例 16.12：不使用查询延续进行选择（未完）

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
//...
    private static void GroupKeywords1()
    IEnumerable<(bool IsContextualKeyword,
```

## 引入查询表达式

```csharp
IGrouping<bool, string> Items> selection =
from word in CSharp.Keywords
group word by word.Contains('*')
    into groups
    select(
        IsContextualKeyword: groups.Key,
        Items: groups
    );
// ...
}
//...
```

在现有的查询`into`结果上运行附加查询的能力不仅适用于以`group`子句结尾的查询，而是可以适用于所有的查询表达式。查询延续仅仅是编写消耗其他查询表达式结果的查询表达式的简写形式。你可以将`into`视为一个“管道操作符”，因为它将第一个查询的结果“管道”到第二个查询中。你可以通过这种方式任意地链起许多查询。

## 使用多个子句将序列的序列扁平化

通常，我们希望将一个序列的序列“扁平化”为单一序列。例如，客户序列的每个成员都可能有一个关联的订单序列，或者目录序列的每个成员都可能有一个关联的文件序列。`SelectMany`序列操作符（在第 15 章中讨论）将所有子序列连接在一起；要使用查询表达式语法实现相同的操作，可以使用多个子句，如示例 16.13 所示。

### 示例 16.13：多重选择

```csharp
var selection =
from word in CSharp.Keywords
from character in word
select character;
```

前面的查询将产生字符序列 `a, b, s, t, r, a, c, t, a, d, d, *, a, l, i, a, ....`

## 第 16 章：LINQ 到查询表达式

多个`from`子句也可以用于产生笛卡尔积——多个序列所有可能的组合的集合——如示例 16.14 所示。

## 示例 16.14：笛卡尔积

```csharp
var numbers = new[] { 1, 2, 3 };
IEnumerable<string word, int Number> product =
    from word in CSharp.Keywords
```
