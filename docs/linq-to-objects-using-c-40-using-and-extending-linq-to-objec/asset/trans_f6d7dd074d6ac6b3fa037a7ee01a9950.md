

```cs
return current;
}

throw new InvalidOperationException("No elements");
}
```

## 是否使用 FOREACH 还是 GETENUMATOR 循环语法

在上一个示例中，我选择根据 `IEnumerable` 接口模式手动创建并使用枚举器。在这个示例中，使用 `foreach` 循环同样有效，并且可能让代码更易读。与 `foreach` 样式的循环相比，使用纯枚举器模式可以带来一些性能上的提升（虽然并不多，但确实有）。以下是使用 `foreach` 语法的实现：

```cs
public static T Last<T>(
    this IEnumerable<T> source)
{
    bool hasElements = false;
    T lastElement = default(T);

    foreach (T item in source)
    {
        hasElements = true;
        lastElement = item;
    }

    // 如果没有元素
    if (!hasElements) throw new
    InvalidOperationException("No elements");

    // 返回最后一个元素
    return lastElement;
}
```

运算符经常用于循环中，关注性能应该是一个目标。其他开发者会假设这些运算符已经过过优化，我们不应该让他们失望。

列表 7-1 中的代码符合编译器要求且功能完备。它简单地接收一个 `IEnumerable<T>` 集合作为源，迭代到最后一个元素，并返回该元素作为结果。该实现捕获的错误条件是源集合中没有元素的情况。抛出 `InvalidOperationException` 是微软运算符实现使用的标准模式，自定义运算符也应该遵循此模式以保持一致性（在之前的代码中省略 `InvalidOperationException` 将导致编译错误，因为并不是所有代码都返回值，所以它并不是可选的）。

另一个需要处理的错误条件是源集合为 `null`（不是空，而是未初始化）。在这种情况下，微软使用的模式是抛出 `ArgumentNullException`，并在任何运算符的开头对 `source` 参数进行此类条件测试，如下代码所示：

```cs
public static T Last<T>(this IEnumerable<T> source)
{
    if (source == null)
        throw new ArgumentNullException("source");
    // ... 与列表 7-1 相同的代码 ...
}
```

该实现功能完备，并遵循了微软在运算符中采用的所有错误条件模式。一旦满足了错误条件，就可以探索性能的提升。

当前的实现会遍历整个源集合以获取最后一个元素，假设源集合的大小为 100,000。如果集合的元素数量很大，这可能被视为性能问题。对于许多集合类型，最后一个元素可以通过单个语句获取。许多集合实现了 `IEnumerable<T>`。`IList<T>` 集合允许通过元素索引位置访问，即从第一个元素开始的零计数。如果集合实现了 `IList<T>`，则自定义运算符应该先尝试该处理逻辑，然后再使用较慢的 `IEnumerable<T>` 枚举算法方法。列表 7-2 显示的代码演示了如何在可能的情况下使用索引位置（否则使用所选的枚举模式）。

## 编写单元素运算符

列表 7-2 带有推荐错误处理和性能优化的 Last 运算符实现

```cs
public static T Last<T>(
    this IEnumerable<T> source)
{
    if (source == null)
        throw new ArgumentNullException("source");

    IList<T> list = source as IList<T>;
    if (list != null)
    {
        int count = list.Count;
        if (count > 0)
            return list[count - 1];
    }
    else
    {
        using (IEnumerator<T> enumerator = source.GetEnumerator())
        {
            if (enumerator.MoveNext())
            {
                T current;
                do
                    current = enumerator.Current;
                } while (enumerator.MoveNext());
                return current;
            }
        }
    }
    throw new InvalidOperationException("No elements");
}
```

该实现首先尝试将源集合转换为 `IList<T>` 接口；如果成功，则使用接口在单个语句中解析最后一个元素。如果集合没有实现 `IList<T>`，则采用使用 `IEnumerable<T>` 接口的 `do-while` 枚举模式。它遵循相同的错误处理模式，该实现与微软在其迭代器实现中使用的模式等效。

## LINQ TO OBJECTS 提供程序是否有内置性能优化？

微软编程编写作家 Alexandra Rusina 针对此主题增加了一个 FAQ 条目，可以在此处查看：http://blogs.msdn.com/csharpfaq/archive/2009/01/26/does-the-linq-to-objects-provider-have-built-in-performance-optimization.aspx。

博客文章中有更多详细信息，但表 7-1 涵盖了要点。

表 7-1 LINQ to Objects 内置性能优化

| LINQ 方法 | 优化 |
| :--- | :--- |
| Cast | 如果数据源针对给定的 T 实现了 `IEnumerable<T>`，则直接返回数据序列而不进行转换。 |
| Contains | 如果数据源实现了 `ICollection` 或 `ICollection<T>` 接口，则使用接口的对应方法。 |
| Count | |
| ElementAt | 如果数据源实现了 `IList` 或 `IList<T>` 接口，则使用接口的 `Count` 方法和索引操作。 |
| ElementAtDefault | |
| First | |
| FirstOrDefault | |
| Last | |
| LastOrDefault | |
| Single | |
| SingleOrDefault | |

在没有源元素时抛出 `InvalidOperationException` 可能不是理想的行为，`FirstOrDefault` 和 `LastOrDefault` 运算符在序列为空时会返回默认值。许多运算符执行基础功能，但不是在序列为空时抛出异常，而是返回默认值。对于我们的 `Last` 实现，我们会添加一个名为 `LastOrDefault` 的运算符，其对运算符代码的唯一更改是：

```cs
public static T LastOrDefault<T>(
    // ... 与列表 7-1 相同的代码，除了 ...
    // 
    return default(T);
```

## default 关键字返回什么？

`default` 关键字解决了初始赋值什么值的问题，对于引用类型返回 `null`，对于数值类型返回零。对于结构体返回零。

## 构建随机运算符

为了演示如何构建一个随机返回元素的运算符，让我们观察满足以下要求的运算符：

- 接收 `IEnumerable<T>` 序列并随机返回元素。
- 通过可选接收 seed 来控制随机数生成器。
- 如果源为 `null`，抛出 `ArgumentNullException`。
- 如果源序列为空，抛出 `InvalidOperationException`。

正如实现 `Last` 时所示，尽管你扩展了 `IEnumerable<T>` 接口，但任何序列都实现了 `IList<T>` 和 `ICollection<T>` 接口，这些可以用来提高性能。任何实现了 `IList` 的集合允许通过索引位置访问（例如，`list[2]` 将返回第三个元素），实现 `ICollection` 的集合暴露了 `Count` 属性以立即获取元素数量。应该使用这些性能增强。

列表 7-3 显示的代码使用了 .NET Framework 内置的随机数生成器在边界范围内查找索引位置并返回该元素。它首先尝试获取元素（因为这样更快），如果该集合不支持该接口，则该运算符使用较慢的枚举模式。

演示了在方法声明中使用可选参数。这在第 8 章“C# 4.0 特性”中会有详细介绍，但这里是为了演示 seed 的值是可选的。如果在调用此方法时省略了 seed 的值，其值为 0。

# 列表 7-3 示例 RandomElement 运算符从源序列中随机返回元素并接收可选的随机数生成器 seed 值

```cs
public static T RandomElement<T>(
    IEnumerable<T> source,
    int seed = 0 /* 可选参数，C# 4.0 新增 */)
{
    // 检查空源条件
    if (source == null)
        throw new ArgumentNullException("source");
}
```

