

group 子句产生的结果查询会生成一组 IGrouping<TKey, TElement> 对象——正如 GroupBy() 标准查询运算符所做的那样（参见第 14 章）。后续查询中的 select 子句使用匿名类型来有效地将 IGrouping<TKey, TElement>.Key 重命名为 IsContextualKeyword，并为子集合属性命名为 Items。通过此更改，嵌套的 foreach 循环使用 wordGroup.Items 而不是直接使用 wordGroup，如清单 15.10 所示。另一个可以添加到匿名类型的潜在属性是子集合中项目的计数。此功能已可通过 wordGroup.Items.Count() 获得，因此将其直接添加到匿名类型的益处值得怀疑。

## 使用 into 的查询延续

正如我们在清单 15.11 中看到的，你可以使用现有查询作为第二个查询的输入。然而，当你想将一个查询的结果用作另一个查询的输入时，并不需要编写一个全新的查询表达式。你可以使用上下文关键字 into 通过查询延续子句扩展任何查询。查询延续不过是创建两个查询并将第一个用作第二个输入的语法糖。into 子句引入的范围变量（清单 15.11 中的 groups）成为查询剩余部分的范围变量；任何之前的范围变量在逻辑上属于较早的查询，不能在查询延续中使用。清单 15.12 显示了如何重写清单 15.11 的代码以使用查询延续而不是两个查询。

## LISTING 15.12: Selecting without the Query Continuation

```
using System;
using System.Collections.Generic;
using System.Linq;

// ...

private static void GroupKeywords1()
{
    var selection =
        from word in Keywords
        group word by word.Contains('*')
        into groups
        select new
        {
```

## LISTING 15.14: Cartesian Product

```
var numbers = new[] { 1, 2, 3 };
var product =
    from word in Keywords
    from number in numbers
    select new {word, number};
```

这将产生一对序列 (abstract, 1), (abstract, 2), (abstract, 3), (as, 1), (as, 2), ...。

## BEGINNER TOPIC

## Distinct Members

通常，希望仅从集合中返回不同的（即唯一的）项，丢弃任何重复项。查询表达式没有用于不同成员的显式语法，但该功能可通过在第 14 章中引入的查询运算符 Distinct() 获得。要将查询运算符应用于查询表达式，表达式必须用括号括起来，以便编译器不会认为对 Distinct() 的调用是 select 子句的一部分。清单 15.15 给出了一个示例；输出 15.8 显示了结果。

## LISTING 15.15: Obtaining Distinct Members from a Query Expression

```
using System;
using System.Collections.Generic;
using System.Linq;

// ...

public static void ListMemberNames()
{
    IEnumerable<string> enumerableMethodNames = (
        from method in typeof(Enumerable).GetMembers(
            System.Reflection.BindingFlags.Static |
            System.Reflection.BindingFlags.Public)
        orderby method.Name
        select method.Name).Distinct();
    foreach(string method in enumerableMethodNames)
    {
        Console.Write($"{ method }, ");
    }
}

// ...
```

## OUTPUT 15.8

```
Aggregate, All, Any, AsEnumerable, Average, Cast, Concat, Contains,
Count, DefaultIfEmpty, Distinct, ElementAt, ElementAtOrDefault,
Empty, Except, First, FirstOrDefault, GroupBy, GroupJoin,
Intersect, Join, Last, LastOrDefault, LongCount, Max, Min, OfType,
OrderBy, OrderByDescending, Range, Repeat, Reverse, Select,
SelectMany, SequenceEqual, Single, SingleOrDefault, Skip,
SkipWhile, Sum, Take, TakeWhile, ThenBy, ThenByDescending, ToArray,
ToDictionary, ToList, ToLookup, Union, Where, Zip,
```

在此示例中，typeof(Enumerable).GetMembers() 返回 System.Linq.Enumerable 上所有成员（方法、属性等）的列表。然而，其中许多成员是重载的，有时不止一次。与其多次显示相同的成员，Distinct() 是从查询表达式调用的。这消除了列表中的重复名称。（我们将在第 17 章中介绍 typeof() 和反射的细节[其中提供了 GetMembers() 等方法]。）

## 查询表达式只是方法调用

有点令人惊讶的是，向 C# 3.0 添加查询表达式不需要对 CLR 或 CIL 语言进行任何更改。相反，C# 编译器只是将查询表达式翻译成一系列方法调用。例如，考虑清单 15.1 中的查询表达式，其一部分出现在清单 15.16 中。

## LISTING 15.16: Simple Query Expression

```
private static void ShowContextualKeywords1()
{
    IEnumerable<string> selection =
        from word in Keywords
        where word.Contains('*')
        select word;
    // ...
}
// ...
```

编译后，清单 15.16 中的表达式被转换为 System.Linq.Enumerable 上的 IEnumerable<T> 扩展方法调用，如清单 15.17 所示。

## LISTING 15.17: Query Expression Translated to Standard Query Operator Syntax

```
private static void ShowContextualKeywords3()
{
    IEnumerable<string> selection =
        Keywords.Where(word => word.Contains('*'));
    // ...
}
// ...
```

正如第 14 章所讨论的，lambda 表达式随后由编译器本身翻译以发出具有 lambda 主体的<|message|>方法，并且对其的使用变为对该方法的委托分配。

每个查询表达式都可以（并且必须）被翻译成方法调用，但并非每个方法调用序列都有对应的查询表达式。例如，扩展方法 TakeWhile<T>(Func<T, bool> predicate) 没有查询表达式等价物，该方法只要谓词返回 true 就会重复返回集合中的项。

对于那些既有方法调用形式又有查询表达式形式的查询，哪种更好？这是一个判断问题；某些查询更适合查询表达式，而其他查询作为方法调用更易读。

## Guidelines

- DO use query expression syntax to make queries easier to read, particularly if they involve complex from, let, join, or group clauses.
- CONSIDER using the standard query operators (method call form) if the query involves operations that do not have a query expression syntax, such as Count(), TakeWhile(), or Distinct().

## SUMMARY

本章介绍了一种新的语法——即查询表达式。熟悉 SQL 的读者会立即看到查询表达式与 SQL 之间的相似之处。然而，查询表达式也引入了 SQL 不可用的附加功能，例如将分组到一组新的分层对象中。查询表达式的所有功能都已可通过标准查询运算符获得，但查询表达式通常为表达此类查询提供更简单的语法。无论是通过标准查询运算符还是查询表达式语法，最终结果都是开发人员对集合 API 编程方式的显著改进——这种改进最终为面向对象语言如何与关系数据库交互提供了范式转变。

在下一章中，我们将继续讨论集合，通过研究 .NET Framework 的一些集合类型并探索如何定义自定义集合。

## 16
Building Custom Collections

第 14 章涵盖了标准查询运算符——即为 IEnumerable<T> 提供的扩展方法，为所有集合提供通用方法。然而，这些运算符并不能使所有集合都同样适合所有任务；仍然需要不同类型的集合。有些集合更适合按键搜索，而其他集合更适合按位置访问项目。有些集合像队列一样工作：先进先出。其他集合更像栈：先进后出。其他集合根本没有顺序。

.NET Framework 提供了大量适用于集合所需场景的集合类型。本章提供

![](img/25683ccec0773ba5b8794b11f2b12877_681_0.png)

