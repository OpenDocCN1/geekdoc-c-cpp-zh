

## 高级主题

### IQueryable<T> 的可查询扩展

与 IEnumerable<T> 几乎相同的接口是 IQueryable<T>。由于 IQueryable<T> 派生自 IEnumerable<T>，因此它拥有 IEnumerable<T> 的所有成员，但仅包含直接声明的那些成员（例如 GetEnumerator()）。扩展方法不会被继承，因此 IQueryable<T> 不具备任何 Enumerable 扩展方法。不过，它有一个类似的扩展类 System.Linq.Queryable，该类为 IQueryable<T> 添加了几乎所有 Enumerable 为 IEnumerable<T> 添加的方法。因此，它提供了非常相似的编程接口。

IQueryable<T> 的独特之处在于它支持自定义 LINQ 提供程序。LINQ 提供程序将表达式细分为其组成部分。拆分后，表达式可以被翻译成另一种语言、序列化以进行远程执行、注入异步执行模式，等等。本质上，LINQ 提供程序允许将拦截机制引入标准集合 API，借助这种看似无限的功能，可以向查询和集合注入相关行为。

例如，LINQ 提供程序允许将查询表达式从 C# 翻译为 SQL，然后在远程数据库上执行。这样一来，C# 程序员可以继续使用其主要的面向对象语言，并把到 SQL 的翻译留给底层 LINQ 提供程序。通过这类表达式，编程语言能够跨越面向对象世界与关系数据库之间的阻抗失配。

就 IQueryable<T> 而言，对延迟执行的警惕更为关键。例如，设想一个从数据库返回数据的 LINQ 提供程序。lambda 表达式不会无视选择条件直接检索数据库中的数据，而是会提供 IQueryable<T> 的一个实现，该实现可能包含上下文信息（如连接字符串），但不包含数据本身。数据检索直到调用 GetEnumerator() 甚至 MoveNext() 时才会发生。然而，GetEnumerator() 调用通常是隐式的，例如在使用 foreach 遍历集合或调用 Count<T>()、Cast<T>() 等 Enumerable 方法时。显然，此类情况要求开发人员警惕延迟执行可能涉及的代价高昂操作的微妙且重复的调用。例如，如果调用 GetEnumerator() 涉及通过网络对数据库进行分布式调用，明智的做法是避免无意中通过 Count() 或 foreach 重复迭代调用。

## 小结

在介绍了匿名类型、隐式变量和集合初始化器之后，本章描述了 foreach 循环的内部工作原理，并解释了其执行所需实现的接口。此外，开发人员经常筛选集合以减少项数，并对集合进行投影以改变项的形式。为此，本章详细讨论了如何使用标准查询运算符（即 System.Linq.Enumerable 类上的常见集合 API）来执行集合操作。

在介绍标准查询运算符时，我们详细阐述了延迟执行的过程，并强调开发人员应注意避免通过枚举集合内容的微妙调用而无意地重新执行表达式。延迟执行以及由此产生的标准查询运算符的隐式执行是代码效率的重要影响因素，尤其是当查询执行代价高昂时。程序员应将查询对象视为查询对象本身，而不是结果，并且应预期查询会完整执行，即使它已经执行过一次。查询对象并不知道结果会与上次执行时的结果相同。

清单 14.26 出现在高级主题部分，是因为连续调用多个标准查询运算符的复杂性。尽管类似的执行需求可能很常见，但并不需要直接依赖标准查询运算符。C# 3.0 包含查询表达式，这是一种类似 SQL 的语法，用于以通常更易于编码和阅读的方式操作集合，我们将在下一章展示。

在本章中，我们介绍查询表达式，并使用它们来表达上一章中的许多查询。

## 介绍查询表达式

开发人员最常执行的两个操作是筛选集合以消除不需要的项，以及投影集合以使项呈现不同的形式。例如，给定一个文件集合，我们可以筛选它，创建一个仅包含“.cs”扩展名文件的新集合，或者仅包含大于 1 百万字节文件的新集合。我们还可以投影文件集合，创建一个新集合，其中包含文件所在目录的路径以及相应的目录大小。查询表达式为这两种常见操作提供了直接的语法。清单 15.1 展示了一个筛选字符串集合的查询表达式；输出 15.1 显示了结果。

### 清单 15.1：简单的查询表达式

```
using System;
using System.Collections.Generic;
using System.Linq;

// ...

static string[] Keywords = {
    "abstract", "add*", "alias*", "as", "ascending*",
    "async*", "await*", "base", "bool", "break",
    "by*", "byte", "case", "catch", "char", "checked",
    "class", "const", "continue", "decimal", "default",
    "delegate", "descending*", "do", "double",
    "dynamic*", "else", "enum", "event", "equals*",
    "explicit", "extern", "false", "finally", "fixed",
    "from*", "float", "for", "foreach", "get*", "global*",
    "group*", "goto", "if", "implicit", "in", "int",
    "into*", "interface", "internal", "is", "lock", "long",
    "join*", "let*", "nameof*", "namespace", "new", "null",
    "object", "on*", "operator", "orderby*", "out",
    "override", "params", "partial*", "private", "protected",
    "public", "readonly", "ref", "remove*", "return", "sbyte",
    "sealed", "select*", "set*", "short", "sizeof",
    "stackalloc", "static", "string", "struct", "switch",
    "this", "throw", "true", "try", "typeof", "uint", "ulong",
    "unsafe", "ushort", "using", "value*", "var*", "virtual",
    "unchecked", "void", "volatile", "where*", "while", "yield*"};

private static void ShowContextualKeywords1()
```

```
IEnumerable<string> selection =
    from word in Keywords
    where !word.Contains('*')
    select word;

foreach (string keyword in selection)
{
    Console.Write(keyword + " ");
}
```

```
// ...
```

### 输出 15.1

```
abstract as base bool break byte case catch char checked class const continue decimal default delegate do double else enum event explicit extern false finally fixed float for foreach goto if implicit in int interface internal is lock long namespace new null object operator out override params private protected public readonly ref return sbyte sealed short sizeof stackalloc static string struct switch this throw true try typeof uint ulong unchecked unsafe ushort using virtual void volatile while
```

在这个查询表达式中，selection 被赋值为 C# 保留关键字的集合。此示例中的查询表达式包含一个 where 子句，用于筛选出非上下文关键字。

查询表达式总是以“from 子句”开头，以“select 子句”或“group 子句”结尾，分别由 from、select 或 group 上下文关键字标识。from 子句中的标识符 word 被称为范围变量；它表示集合中的每一项，就像 foreach 循环中的循环变量表示集合中的每一项一样。

熟悉 SQL 的开发人员会注意到，查询表达式的语法与 SQL 类似。这一设计是刻意的——其目的是让已经了解 SQL 的程序员能够轻松学习 LINQ。然而，两者存在一些明显的差异。大多数具有 SQL 经验的开发人员注意到的第一个区别是，这里显示的 C# 查询表达式中的子句顺序为：from、然后 where、最后 select。等效的 SQL 查询则将 SELECT 子句放在最前面，然后是 FROM 子句，最后是 WHERE 子句。

这种顺序变化的一个原因是能够使用 IntelliSense，这是 IDE 的一项功能，编辑器通过它生成有用的用户界面元素，例如描述给定类型成员的下拉列表。

