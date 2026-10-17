
## 列表 5-27 SkipWhile 和 TakeWhile 运算符在谓词参数返回真时跳过或返回元素——参见输出 5-15

```cs
string sampleString =
@"# comment line 1
# comment line 2
Data line 1
Data line 2

This line is ignored
"

var q = sampleString.Split('\n')
  .SkipWhile(line => line.StartsWith("#"))
  .TakeWhile(line => !string.IsNullOrEmpty(line.Trim()));

foreach (var s in q)
  Console.WriteLine(s);
```

## 输出 5-15

Data line 1

Data line 2

## 量化运算符–All, Any 和 Contains

量化运算符 `All`、`Any` 和 `Contains` 根据序列中是否存在某些数据来返回布尔结果值。这些运算符都可以通过创建查询（使用 `Where` 子句过滤数据，并比较结果序列的元素计数以检查其是否大于零）来实现。但这些运算符针对其用途进行了优化，会在第一个可能的点返回结果，从而避免遍历整个序列（通常称为短路求值）。

### All 运算符

`All` 运算符如果序列中的所有元素都通过了提供的谓词函数，则返回布尔结果真。

### 量化运算符——ALL, ANY, AND CONTAINS 165

`All` 有一个重载，其方法签名如下：

```cs
// 如果所有元素都通过谓词
// 函数，否则返回假。
public static bool All<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate);
```

为了演示 `All` 运算符，列表 5-28 测试了三个整数数组，如果所有元素都是偶数（能被2除且无余数），则返回真。此示例的控制台输出所示输出 5-16。

#### 5-28 如果所有对象都通过谓词，All 运算符返回真——参见输出 5-16

```cs
var evens = new int[] { 2, 4, 6, 8, 10 };
var odds = new int[] { 1, 3, 5, 7, 9 };
var nums = Enumerable.Range(1, 10);

Console.WriteLine("All even? evens: {0}, odds: {1}, nums: {2}");
evens.All(i=> i%2 == 0);
odds.All(i => i%2 == 0);
nums.All(i => i%2 == 0);
```

#### 5-16

All even? evens: True, odds: False, nums: False

谓词可以根据需要变得复杂；它可以包含任意数量的逻辑与 `&&` 和或 `||`，但必须返回一个布尔值。列表 5-29 展示了如何查询确定所有联系人（来自第 2 章介绍的示例数据，“介绍 LINQ to Objects”，表 2-1）是否都超过 21 岁，并且每个联系人都有电话号码和电子邮件地址。此示例的控制台输出所示输出 5-17。

### 第 5 章 标准查询运算符

#### 列表 5-29 在示例联系人数据集中使用 All 运算符的示例——参见输出 5-17

```cs
var contacts = Contact.SampleData();
bool allOver21 = contacts.All(
    c => c.DateOfBirth.AddYears(21) < DateTime.Now);
bool allContactsHaveContactData = contacts.All(
    c => string.IsNullOrEmpty(c.Phone) == false &&
    string.IsNullOrEmpty(c.Email) == false);

Console.WriteLine("Are all contacts over 21 years old? {0}",
    allOver21);

Console.WriteLine("Do all contacts have email and phone? {0}",
    allContactsHaveContactData);
```

## 输出 5-17

Are all contacts over 21 years old? True

Do all contacts have email and phone? True

### Any 运算符

如果序列中存在任何元素，或者序列中有任何元素通过了谓词函数，`Any` 运算符返回布尔结果真。

`Any` 运算符有两个重载。第一个重载不接受参数，测试序列是否至少有一个元素，而第二个重载接受一个谓词函数，并测试至少有一个元素通过谓词逻辑。方法签名如下：

```cs
// 如果序列中至少有一个
// 元素，否则返回假 any。
public static bool Any<TSource>(
this IEnumerable<TSource> source);
```

```cs
// 如果任何元素通过了
// 谓词函数，否则返回假。
public static bool Any<TSource>(
this IEnumerable<TSource> source, 
Func<TSource, bool> predicate);
```

为了演示 `Any` 运算符，列表 5-30 测试了三个序列——一个是空的（没有元素），一个包含单个元素，第三个包含许多元素。在这些序列上调用 `Any` 操作会返回布尔结果。此示例的控制台输出所示输出 5-18。

#### 5-30 如果序列中存在任何元素，Any 运算符返回真——参见输出 5-18

```cs
var empty = Enumerable.Empty<int>();
var one = new int[] { 1 };
var many = Enumerable.Range(1,5);

Console.WriteLine("Empty: {0}, One: {1}, Many: {2}",
empty.Any(), one.Any(), many.Any());
```

## 输出 5-18

Empty: False, One: True, Many: True

`Any` 运算符是确定序列中是否存在元素最高效的方法，尽管第二个重载接受谓词函数在功能上是等价的。此示例的控制台输出所示输出 5-19。

### 168 标准查询运算符

#### 列表 5-31 如果序列中存在任何元素，Any 运算符返回真——参见输出 19

```cs
string[] animals = {"Koala", "Kangaroo", "Spider", "Wombat", "Snake", "Emu", "Shark", "Jellyfish" };

bool anyFish = animals.Any(a => a.Contains("fish"));
bool anyCats = animals.Any(a => a.Contains("cat"));

Console.WriteLine("Any fish? {0}, Any cats? {1}", anyFish, anyCats);
```

输出 5-19

Any fish? True, Any cats? False

如果序列包含与传入此运算符的测试参数等价元素，`Contains` 运算符返回布尔值真。此运算符有两个重载——一个接受测试值的单个参数，另一个接受测试值和一个用于相等性测试的 `IEqualityComparer<T>` 实例。

为了演示 `Contains` 运算符，列表 5-33 查看字符串数组元素中是否包含不同版本的 Peter 名称。测试 `b1` 将为假，因为字符串的默认比较是大小敏感的。测试 `b2` 将为真，因为它是精确的字符串匹配，而测试 `b3` 将为真，尽管使用了自定义 `customEqualityComparer<T>` 来确定字符串相等性。（创建自定义 `IEqualityComparers` 将在第 4 章中“指定你的

（“自定义键比较函数”章节以及第 6 章中的“使用 LINQ 集合运算符时的自定义相等比较器”）。此示例的控制台输出如输出 5-21 所示。

#### 列表 5-33 Contains运算符如果测试元素在序列中，则返回 true——参见输出 5-21

```
string[] names = new string[] { "peter", "paul", "mary" };

bool b1 = names.Contains("PETER");
bool b2 = names.Contains("peter");

// 可以使用自定义比较器或内置的比较器
bool b3 = names.Contains(
    "PETER", StringComparer.InvariantCultureIgnoreCase);

Console.WriteLine("PETER: {0}, peter: {1}, PETER: {2}",
b1, b2, b3);
```

# 输出 5-21

PETER: False, peter: True, PETER: True

某些实现 `IEnumerable<T>` 且在 `Contains` 扩展方法范围内的集合类型实现了它们名为 `Contains(List<T>)` 的实例方法。在大多数情况下，这不会引起任何问题，但如果你显式地调用扩展 `Contains`，请指定泛型类型。列表 5-34 展示了在使用 `List<T>` 类型集合时如何显式控制调用哪个方法（实例方法或扩展方法）。此示例的控制台输出如输出 5-22 所示。

#### 列表 5-34 当集合拥有名为 `Contains` 的实例方法时，如何显式指定你想调用哪个 `Contains`——参见输出 5-22

```
// List<T> 已经有一个名为 "Contains" 的实例方法
// 该实例方法没有支持
// EqualityComparer 的重载，因此可以使用 Contains
// 扩展方法进行此项调用。
```

# 总结 171

```
List<string> list =
    new List<string> { "peter", "paul", "mary" };

// 将使用 List<T>.Contains 方法
bool b4 = list.Contains("PETER");

// 将强制使用 Contains 扩展方法
bool b5 = list.Contains<string>("PETER");

// 或者更好的是，直接调用扩展方法
bool b6 = Enumerable.Contains(list, "PETER");

// 将使用 Contains 扩展方法，因为
// List<T>.Contains 没有接受
// IEqualityComparer 的参数重载
bool b7 = list.Contains(
    "PETER", StringComparer.InvariantCultureIgnoreCase);

Console.WriteLine(
    "Instance: {0}, Extension: {1}, With Comparator: {2}",
    b4, b5, b6);
```

## 输出 5-22

Instance: False, Extension: False, With Comparator: True

# 摘要

本章介绍了在 .NET Framework 4 中可用的许多剩余标准查询运算符。下一章将涵盖最后几个专门对数据源应用基于集合set的运算符。

# 第 6 章

# 处理集合数据

本章目标：

- 定义使用 LINQ 处理集合数据的两种选项。
- 介绍 `HashSet` 类型以及它如何与 LINQ 关联。
- 介绍与处理集合数据有关的 LINQ 标准查询运算符。

使用 LINQ 在数据序列上应用基于集合的功能有两种方法。本章探索了这两种选项的优点，并解释了何时以及为何使用一种方法而不是另一种方法。

## 引言

集合操作允许各种函数比较集合（以及在某些情况下是同一个集合）中的元素，以确定集合中的重叠元素和唯一元素。

.NET Framework 1、2 和 3 缺少用于集合操作的框架库。`HashSet` 在 .NET Framework 3.5 中引入，这种集合类型解决了开发者经常面对的大多数集合问题。LINQ 通过特定运算符扩展了集合函数功能，其中某些与 `HashSet` 的功能重叠。理解这两种策略的优点以及何时选择其中一种是关重要的。本节详细查看了这两个主要选择：

- LINQ 标准查询运算符
- 来自 `System.Collections.Generic` 命名空间的 `HashSet<T>` 类

如何处理基于集合的任务取决于问题的具体情况，但通常情况下，每种方法的优点可以用以下方式描述：

当使用 `HashSet` 及其运算符时：

- 集合中不允许重复项。
- 希望修改原始集合。这些运算符允许对原始集合进行更改。

当使用 LINQ 运算符时：

- 集合中允许重复项。
- 当希望返回一个新的 `IEnumerable<T>` 而不是修改原始集合时。

## LINQ 集合运算符

LINQ to Objects 有用于处理集合内元素集合的标准查询运算符。这些运算符允许使用各种方法将两个集合（包含相同类型的元素）合并为单个集合。

所有集合运算符都实现了延迟执行模式，简单来说，它们在逐个迭代元素之前不会对下一个元素进行评估。本节将详细介绍每个运算符，包括每个运算符的方法签名。

### Concat 运算符

`Concat` 合并两个集合的内容。它通过遍历第一个集合并产生每个元素，然后遍历第二个集合并产生每个元素来操作。如果返回重复元素所需的行为，请考虑使用 `Union` 运算符。当调用此运算符时，如果任何集合为空，将抛出 `ArgumentNullException`。

`Concat` 只有一个重载，方法签名如下：

```
// 合并两个集合的内容。
// 返回来自 IEnumerable<TSource> 的所有元素
IEnumerable<TSource> Concat<TSource>(
    this IEnumerable<TSource> first,
    IEnumerable<TSource> second);
```

# 输出 5-21

PETER: False, peter: True, PETER: True

某些实现 `IEnumerable<T>` 且在 `Contains` 扩展方法范围内的集合类型实现了它们名为 `Contains(List<T>)` 的实例方法。在大多数情况下，这不会引起任何问题，但如果你显式地调用扩展 `Contains`，请指定泛型类型。列表 5-34 展示了在使用 `List<T>` 类型集合时如何显式控制调用哪个方法（实例方法或扩展方法）。此示例的控制台输出如输出 5-22 所示。

#### 列表 5-34 当集合拥有名为 `Contains` 的实例方法时，如何显式指定你想调用哪个 `Contains`——参见输出 5-22

```
// List<T> 已经有一个名为 "Contains" 的实例方法
// 该实例方法没有支持
// EqualityComparer 的重载，因此可以使用 Contains
// 扩展方法进行此项调用。
```

# 总结 171

```
List<string> list =
    new List<string> { "peter", "paul", "mary" };

// 将使用 List<T>.Contains 方法
bool b4 = list.Contains("PETER");

// 将强制使用 Contains 扩展方法
bool b5 = list.Contains<string>("PETER");

// 或者更好的是，直接调用扩展方法
bool b6 = Enumerable.Contains(list, "PETER");

// 将使用 Contains 扩展方法，因为
// List<T>.Contains 没有接受
// IEqualityComparer 的参数重载
bool b7 = list.Contains(
    "PETER", StringComparer.InvariantCultureIgnoreCase);

Console.WriteLine(
    "Instance: {0}, Extension: {1}, With Comparator: {2}",
    b4, b5, b6);
```

## 输出 5-22

Instance: False, Extension: False, With Comparator: True

# 摘要

本章介绍了在 .NET Framework 4 中可用的许多剩余标准查询运算符。下一章将涵盖最后几个专门对数据源应用基于集合的运算符。

# 第 6 章

# 处理集合数据

本章目标：

- 定义使用 LINQ 处理集合数据的两种选项。
- 介绍 `HashSet` 类型以及它如何与 LINQ 关联。
- 介绍与处理集合数据有关的 LINQ 标准查询运算符。

使用 LINQ 在数据序列上应用基于集合的功能有两种方法。本章探索了这两种选项的优点，并解释了何时以及为何使用一种方法而不是另一种方法。

## 引言

集合操作允许各种函数比较集合（以及在某些情况下是同一个集合）中的元素，以确定集合中的重叠元素和唯一元素。

.NET Framework 1、2 和 3 缺少用于集合操作的框架库。`HashSet` 在 .NET Framework 3.5 中引入，这种集合类型解决了开发者经常面对的大多数集合问题。LINQ 通过特定运算符扩展了集合函数功能，其中某些与 `HashSet` 的功能重叠。理解这两种策略的优点以及何时选择其中一种是重要的。本节详细查看了这两个主要选择：

- LINQ 标准查询运算符
