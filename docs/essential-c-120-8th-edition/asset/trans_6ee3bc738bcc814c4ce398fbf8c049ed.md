

# 16 使用查询表达式的 LINQ

第 15 节末尾展示了一个使用标准查询运算符 `GroupJoin()`、`SelectMany()` 和 `Distinct()` 的查询。结果是一个跨越多行的语句，比通常仅使用 C# 早期版本特性的语句要复杂得多且难以理解。处理丰富数据集的现代程序通常需要此类复杂的查询；因此，如果语言能够让这些查询更易于阅读，将大有益处。像 SQL 这样的领域特定查询语言使得查询变得更易于阅读和理解，但它们缺乏 C# 语言的完整威力。这就是为什么 C# 语言设计者添加了查询表达式语法¹。通过查询表达式，许多标准查询运算符表达式被转换为更具读性的代码，就像 SQL 一样。

| 2. 查询表达式是方法调用 | 使用查询表达式的 LINQ | 1. 引入查询表达式 | 投影 |
|---|---|---|---|
| | | 排序 | 分组 |

在本章中，我们引入了查询表达式，并使用它们来表示第 15 节中的许多查询。

- 1. 从 C# 3.0 开始。

# 引入查询表达式

开发者最频繁执行的操作是过滤集合以消除不需要的项，以及投影集合以使项以不同的形式存在。例如，给定一个文件集合，我们可以过滤它以创建一个仅包含 .cs 扩展名文件的新集合，或者仅包含大于 100 万字节文件的新集合。我们还可以对文件集合进行投影，创建一个新的集合，该集合同时包含目录路径和相应的目录大小。查询表达式为这两种常用操作提供了直观的语法。列表 16.1 显示了一个过滤字符串集合的查询表达式；输出 16.1 显示了结果。

列表 16.1：简单的查询表达式

```
public static static readonly ReadOnlyCollection<string> Keywords = new(
    string[] {
        "abstract", "add", "alias", "as", "ascending",
        "async", "await", "base", "bool", "break",
        "byte", "case", "catch", "char", "checked",
        "class", "const", "continue", "decimal", "default",
        "delegate", "descending", "do", "double", "dynamic",
        "else", "enum", "equals", "event", "explicit",
        "extern", "finally", "fixed", "float", "for",
        "foreach", "from", "get", "global", "goto", "group",
        "if", "il", "in", "interface", "internal",
        "into", "join", "let", "lock", "long",
        "nameof", "namespace", "new", "nonnull", "null",
        "object", "on", "operator", "orderby", "out",
        "override", "params", "partial", "private",
        "protected", "public", "readonly", "ref", "remove",
        "return", "sbyte", "sealed", "select", "set", "short",
        "sizeof", "stackalloc", "static", "string", "struct",
        "switch", "this", "throw", "true", "try", "typeof",
        "uint", "unchecked", "unsafe", "ushort",
        "using", "value", "var", "virtual", "void", "volatile",
        "when", "where", "while", "yield"
    }
);
```

```cs
// ...
using System;
using System.Collections.Generic;
using System.Linq;
// ...
private static void ShowContextualKeywords() {
    IEnumerable<string> selection =
    from word in CSharp.keywords
    where word.Contains('*')
    select word;
```

```cs
foreach (string keyword in selection) {
    Console.Write(keyword + " ");
}
```

# 输出 16.1

abstract as base pool break byte case catch checked class const continue default do double else event explicit extern finally fixed float for foreach from get global goto group if il in interface internal into join let lock long nameof namespace new nonnull object on operator orderby out override params partial private protected public readonly ref remove return sbyte sealed select set short sizeof stackalloc static string switch this throw true try typeof uint unchecked unsafe ushort using var virtual void volatile when where while yield

