

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

量化运算符 All、Any 和 Contains 根据序列中是否存在某些数据来返回布尔结果值。这些运算符都可以通过创建查询（使用 `Where` 子句过滤数据，并比较结果序列的元素计数以检查其是否大于零）来实现。但这些运算符针对其用途进行了优化，会在第一个可能的点返回结果，从而避免遍历整个序列（通常称为短路求值）。

## All 运算符

All 运算符如果序列中的所有元素都通过了提供的谓词函数，则返回布尔结果真。

## 量化运算符——ALL, ANY, AND CONTAINS 165

All 有一个重载，其方法签名如下：

```cs
// 如果所有元素都通过谓词
// 函数，否则返回假。
public static bool All<TSource>(
    this IEnumerable<TSource> source,
    Func<TSource, bool> predicate);
```

为了演示 All 运算符，列表 5-28 测试了三个整数数组，如果所有元素都是偶数（能被2除且无余数），则返回真。此示例的控制台输出所示输出 5-16。

**5-28 如果所有对象都通过谓词，All 运算符返回真——参见输出 5-16

```cs
var evens = new int[] { 2, 4, 6, 8, 10 };
var odds = new int[] { 1, 3, 5, 7, 9 };
var nums = Enumerable.Range(1, 10);

Console.WriteLine("All even? evens: {0}, odds: {1}, nums: {2}");
evens.All(i=> i%2 == 0);
odds.All(i => i%2 == 0);
nums.All(i => i%2 == 0);
```

**5-16**

All even? evens: True, odds: False, nums: False

谓词可以根据需要变得复杂；它可以包含任意数量的逻辑与 (&&) 和或 (||)，但必须返回一个布尔值。列表 5-29 展示了如何查询确定所有联系人（来自第 2 章介绍的示例数据，“介绍 LINQ to Objects”，表 2-1）是否都超过 21 岁，并且每个联系人都有电话号码和电子邮件地址。此示例的控制台输出所示输出 5-17。

## 第 5 章 标准查询运算符

**列表 5-29** 在示例联系人数据集中使用 All 运算符的示例——参见输出 5-17

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

## Any 运算符

如果序列中存在任何元素，或者序列中有任何元素通过了谓词函数，Any 运算符返回布尔结果真。
Any 运算符有两个重载。第一个重载不接受参数，测试序列是否至少有一个元素，而第二个重载接受一个谓词函数，并测试至少有一个元素通过谓词逻辑。方法签名如下：

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

为了演示 Any 运算符，列表 5-30 测试了三个序列——一个是空的（没有元素），一个包含单个元素，第三个包含许多元素。在这些序列上调用 Any 操作会返回布尔结果。此示例的控制台输出所示输出 5-18。

## 5-30 如果序列中存在任何元素，Any 运算符返回真——参见输出 5-18

```cs
var empty = Enumerable.Empty<int>();
var one = new int[] { 1 };
var many = Enumerable.Range(1,5);

Console.WriteLine("Empty: {0}, One: {1}, Many: {2}",
empty.Any(), one.Any(), many.Any());
```

## 输出 5-18

Empty: False, One: True, Many: True

Any 运算符是确定序列中是否存在元素最高效的方法，尽管第二个重载接受谓词函数在功能上是等价的。此示例的控制台输出所示输出 5-19。

## 168 标准查询运算符

列表 5-31 如果序列中存在任何元素，Any 运算符返回真——参见输出 19

```cs
string[] animals = {"Koala", "Kangaroo", "Spider", "Wombat", "Snake", "Emu", "Shark", "Jellyfish" };

bool anyFish = animals.Any(a => a.Contains("fish"));
bool anyCats = animals.Any(a => a.Contains("cat"));

Console.WriteLine("Any fish? {0}, Any cats? {1}", anyFish, anyCats);
```

输出 5-19

Any fish? True, Any cats? False

如果序列包含与传入此运算符的测试参数等价元素，Contains 运算符返回布尔值真。此运算符有两个重载——一个接受测试值的单个参数，另一个接受测试值和一个用于相等性测试的 `IEqualityComparer<T>` 实例。

为了演示 Contains 运算符，列表 5-33 查看字符串数组元素中是否包含不同版本的 Peter 名称。测试 b1 将为假，因为字符串的默认比较是大小敏感的。测试 b2 将为真，因为它是精确的字符串匹配，而测试 b3 将为真，尽管使用了自定义 `customEqualityComparer<T>` 来确定字符串相等性。（创建自定义 `IEqualityComparers` 将在第 4 章中“指定你的

