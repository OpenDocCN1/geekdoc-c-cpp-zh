

## 表 6-2 LINQ 集合操作符与 HashTable 类型方法的比较

| HashSet<T> 操作符 | LINQ 等效操作符 | 描述 |
|---|---|---|
| IsSupersetOf | 未提供。若要使用 LINQ 来实现相同结果，按照以下方式，如果交集计数等于第二个集合中唯一元素的数量，则返回布尔值 true：
```csharp
var bCount = b.Distinct().Count();
var intersectCount = b.Intersect(a).Distinct().Count();
return intersectCount == bCount;
``` | 如果第二个集合中的所有元素都存在于给定集合中，则返回布尔值 true。如果集合共享相同的元素也会返回布尔值 true。 |
| IsProperSupersetOf | 未提供。若要使用 LINQ 实现相同结果，按照以下方式，如果交集计数小于集合中的元素数量且交集计数等于集合中唯一元素的数量，则返回布尔值 true：
```csharp
var aCount = a.Distinct().Count();
var bCount = b.Distinct().Count();
var intersectCount = b.Intersect(a).Distinct().Count();
return intersectCount < aCount && intersectCount == bCount;
``` | 如果第二个集合中的所有元素都存在于给定集合中，则返回布尔值 true。如果集合共享完全相同的元素，则返回布尔值 false。该集合必须是真正的超集，比第二个集合至少多一个元素。 |
| SetEquals | 未提供。若要用 LINQ 实现相同结果，按照以下方式比较唯一且有序的集合：a.Distinct().OrderBy(x => x).SequenceEqual(b.Distinct().OrderBy(y => y)); | 如果两个集合共享相同的唯一元素值，则返回布尔值 true。 |

## 列表 6-9 HashSet 中操作符的 LINQ 近似实现

```csharp
public static IEnumerable<T> SymmetricExcept<T>(
    this IEnumerable<T> first,
    IEnumerable<T> second = null)
{
    if (first == null)
    {
        throw new ArgumentNullException("first");
    }

    if (second == null)
    {
        throw new ArgumentNullException("second");
    }

    return first.Except(second)
        .Concat(
            second.Except(first));
}

public static bool Overlaps<T>(
    IEnumerable<T> first,
    IEnumerable<T> second)
{
    if (first == null)
    {
        throw new ArgumentNullException("first");
    }

    if (second == null)
    {
        throw new ArgumentNullException("second");
    }

    return second.Intersect(first).Distinct().Any();
}
```

## HASHSET<T> 类

```csharp
public static bool IsSupersetOf<T>(
    this IEnumerable<T> first,
    IEnumerable<T> second)
{
    if (first == null)
        throw new ArgumentNullException("first");

    if (second == null)
        throw new ArgumentNullException("second");

    var secondCount = second.Distinct().Count();

    var intersectCount = second
        .Intersect(first)
        .Distinct()
        .Count();

    return intersectCount == secondCount;
}
public static bool IsProperSupersetOf<T>(
    this IEnumerable<T> first,
    IEnumerable<T> second)
{
    if (first == null)
        throw new ArgumentNullException("first");

    if (second == null)
        throw new ArgumentNullException("second");

    var firstCount = first.Distinct().Count();
    var secondCount = second.Distinct().Count();

    var intersectCount = 
        second
        .Intersect(first)
        .Distinct()
        .Count();

    return (intersectCount < firstCount) &&
        (intersectCount == secondCount);
}
```

```csharp
public static bool IsSubsetOf<T>(
    this IEnumerable<T> first,
    IEnumerable<T> second)
{
    // 调用超集操作符并反转参数
    return IsSubsetOf(second, first);
}
```

```csharp
public static bool IsProperSubsetOf<T>(
    this IEnumerable<T> first,
    IEnumerable<T> second)
{
    // 调用超集操作符并反转参数
    return IsSupersetOf(second, first);
}
```

```csharp
public static bool SetEquals<T>(
    this IEnumerable<T> first,
    IEnumerable<T> second)
{
    return first.Distinct().OrderBy(x => x)
           .SequenceEqual(second.Distinct().OrderBy(y => y));
}
```

## 总结

使用 LINQ 处理集合数据并不比选择正确的标准查询操作符困难。也可以使用现有的 HashSet<T> 集合类型，而决定哪种集合方法适合你的问题归结为以下因素：

在以下情况下使用 HashSet 及其操作符：

- 集合中不允许存在重复项。
- 希望修改原始集合。这些操作符会对原始集合进行更改。

在以下情况下使用 LINQ 操作符：

- 集合中允许存在重复项。
- 当希望返回一个新的 `IEnumerable<T>` 而不是修改原始集合时。

## 将 LINQ 扩展到对象

本章目标：

- 定义不同类型的操作符以及它们的独特性。
- 定义用于每种操作符的通用模式。
- 理解错误处理的最佳实践。

LINQ to Objects 设计用于扩展扩展。本章将讨论如何编写新的操作符，并像使用标准操作符一样使用它们。

## 编写新操作符

虽然标准查询操作符已经很全面，但通常需要构建更多操作符来满足编程问题。虽然编写新操作符初看起来难度很大，但标准操作符的实现代码很少超过几行。

LINQ to Objects 操作符根据其返回类型和操作分为四类。基本类别为

- 单元素操作符——返回单个元素（例如 First, Last, ElementAt）。
- 序列操作符——返回序列（Where, Select）。
- 聚合操作符——返回聚合结果值（Count, Min, Max

## 编写单元素操作符

单元素操作符的作用为任何实现 IEnumerable<T> 的类型添加扩展方法，并从集合中返回单个元素。标准查询操作符 First、Last 和 ElementAt 是这种操作的示例。

理解 Microsoft 如何构建标准操作符是理解自定义操作符的第一步。为了探索构建操作符的方法，在构建更复杂的操作符之前，让我们先构建自己的 Last 操作版本。

## 构建自己的 Last 操作

为了学习如何构建返回单个元素的操作符，让我们首先查看标准查询操作符 Last 是如何实现的。Last 操作符的最短编译实现位于列表 7-1。

**列表 7-1** 最短编译 Last 操作符实现

```csharp
public static T Last<T>(
    IEnumerable<T> source)
{
    using (IEnumerator<T> enumerator = source.GetEnumerator())
    {
        if (enumerator.MoveNext())
        {
            T current;
            do
            {
                current = enumerator.Current;
            }
            while (enumerator.MoveNext());
        }
    }
}
```

