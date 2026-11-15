

之所以这样做，是为了启用 IntelliSense，即预测所选对象成员的能力。例如，因为 from 出现在第一位并将字符串数组 Keywords 标识为数据源，代码编辑器知道 word 是 string 类型。这启用了 IntelliSense——对 word 进行成员访问（点运算）将仅显示 string 的成员。如果 from 子句出现在 select 之后，那么 from 子句之前的任何点运算都不会知道 word 的数据类型是什么，因此也就无法显示 word 的成员列表。例如，在清单 15.1 中，将无法预测 Contains() 是 word 的可能成员。word 被称为范围变量；它表示集合中的每个项目。

## 投影

查询表达式的输出是 IEnumerable<T> 或 IQueryable<T> 集合。¹ T 的数据类型从 select 或 groupby 子句中推断。例如，在清单 15.1 中，string 的数据类型是从 select word 推断出来的，因为 word 是 string，word 的数据类型是 from 子句中 IEnumerable<T> 集合的类型参数。由于 Keywords 是字符串数组，它实现了 IEnumerable<string>，因此 word 是 string。

查询特定类型集合的表达式所产生的类型绝不局限于该原始类型的序列。相反，select 子句允许将数据投影到完全不同的类型。请考虑清单 15.2 中的查询表达式及其在输出 15.2 中的相应输出。

```
LISTING 15.2: Projection Using Query Expressions
using System;
using System.Collections.Generic;
using System.Linq;
using System.IO;

// ...

static void List1(string rootDirectory, string searchPattern)
{
    IEnumerable<FileInfo> files =
        from fileName in Directory.GetFiles(
            rootDirectory, searchPattern)
        select new FileInfo(fileName);

    foreach (FileInfo file in files)
    {
        Console.WriteLine("{0} ({1})",
            file.Name, file.LastWriteTime);
    }
}

// ...
```

1. 查询表达式的输出实际上总是 IEnumerable<T>，但理论上不一定。没有什么能阻止任何人实现返回其他内容的查询运算符。这样做有些乖张，但语言中没有要求查询运算符必须返回 IEnumerable<T>。

## 输出 15.2:

```
Account.cs(10/1/2007 11:56:11 AM)
Bill.cs(6/10/2007 9:33:55 PM)
Contact.cs(6/14/2007 11:40:30 PM)
Customer.cs(11/17/2007 2:02:52 AM)
Employee.cs(8/17/2007 1:33:22 AM)
Person.cs(10/22/2007 10:00:03 PM)
```

请注意，此查询表达式返回的是 IEnumerable<FileInfo>，而不是 System.IO.Directory.GetFiles() 返回的 IEnumerable<string> 数据类型。查询表达式的 select 子句可能会投影出与 from 子句表达式（Directory.GetFiles()）所收集的不同的数据类型。

事实上，这种投影正是 C# 3.0 将匿名类型纳入语言的关键驱动因素。通过匿名类型，可以在不定义显式类型的情况下选择出所需的确切数据。例如，清单 15.3 提供了与清单 15.2 类似的输出，但使用的是匿名类型而不是 FileInfo。

## 清单 15.3：查询表达式中的匿名类型

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.IO;

// ...

static void List2(string rootDirectory, string searchPattern)
{
    var files =
        from fileName in Directory.GetFiles(
            rootDirectory, searchPattern)
        select new
        {
            Name = fileName,
            LastWriteTime = file.GetLastWriteTime(fileName)
        };

    foreach (var file in files)
    {
        Console.WriteLine("{0}({1})",
            file.Name, file.LastWriteTime);
    }
}

// ...
```

在此示例中，查询仅投影出文件名及其最后写入时间。在处理 FileInfo 之类的小对象时，像清单 15.3 这样的投影差别不大。但是，当数据量很大且检索数据（也许是通过 Internet 从不同计算机检索）代价高昂时，过滤掉集合中每个项目关联数据量的水平投影非常强大。与在查询执行时检索所有数据相比，使用匿名类型可以将仅所需的数据存储和检索到集合中。例如，想象一个包含 30 个或更多列的表的大型数据库。如果没有匿名类型，开发人员将不得不使用包含不必要信息的对象，或定义仅用于存储所需特定数据的小型专用类。相反，匿名类型支持由编译器定义类型——这些类型仅包含其直接场景所需的数据。其他场景可以有仅包含该场景所需属性的不同投影。

## 初学者主题

## 查询表达式中的延迟执行

延迟执行的主题在前一章中也出现过。相同的原则也适用于查询表达式。请再次考虑清单 15.1 中 selection 的赋值。赋值本身并不执行查询表达式。换句话说，在 selection 的赋值期间，不会调用 word.Contains("**")。相反，查询表达式会保存选择条件，以便在遍历 selection 变量标识的集合时使用。

为了说明这一点，请考虑清单 15.4 及其相应的输出（输出 15.3）。

## 清单 15.4：延迟执行和查询表达式（示例 1）

```
using System;
using System.Collections.Generic;
using System.Linq;

// ...

private static void ShowContextualKeywords2()
{
    IEnumerable<string> selection = from word in Keywords
                                    where IsKeyword(word)
                                    select word;

    foreach (string keyword in selection)
    {
        Console.Write(keyword);
    }
}

// Side effect (console output) included in predicate to show
// deferred execution not as a best practice.
private static bool IsKeyword(string word)
{
    if (word.Contains("**"))
    {
        Console.Write("");
        return true;
    }
    else
    {
        return false;
    }
}

// ...
```

## 输出 15.3:

```
add* alias* ascending* by* descending* dynamic* equals* from* get*
global* group* into* join* let* on* orderby* partial* remove* select*
set* value* var* where* yield*
```

请注意，在清单 15.4 中，foreach 循环内不会输出空格。上下文关键字之间的空格是在 IsKeyword() 函数中输出的，这表明 IsKeyword() 函数是在代码遍历 selection 时才被调用，而不是在 selection 赋值时调用。

关键在于，尽管 selection 是一个集合（毕竟它是 IEnumerable<T> 类型），但在赋值时，from 子句之后的所有内容都构成选择条件。只有在开始遍历 selection 时，才会应用这些条件。

请考虑第二个示例（请参见清单 15.5 和输出 15.4）。

## 清单 15.5：延迟执行和查询表达式（示例 2）

```
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
        where keyword.Contains("*")
        select func(keyword);

    Console.WriteLine(
        "1. delegateInvocations={0}", delegateInvocations);

    // Executing count should invoke func once for
    // each item selected.
    Console.WriteLine(
        "2. Contextual keyword count={0}", selection.Count());

    Console.WriteLine(
        "3. delegateInvocations={0}", delegateInvocations);

    // Executing count should invoke func once for
```

