

```cs
// 结果选择函数
// (将最终和细化为方差)
// 平均值 = sum / count
// 方差 = (sum_sqr - sum * mean) / (n - 1)
result =>
(result[2] - (result[1] * (result[1] / result[0]))
/ (result[0] - 1)
);
```

如表 9.2 所示，优化顺序算法获得的性能收益是巨大的——比仅依赖并行优化效果更为显著。

现在已经编写了 `Variance` 运算符，`StandardDeviation` 运算符只需如列表 9-11 所示基于结果构建。此示例还演示了通用的模式，即定义一个接受值选择器器函数的重载——这遵循了提供的聚合标准查询运算符所设模式，并是推荐的做法。

## 列表 9-11 StandardDeviation 运算符的顺序实现

```csharp
public static double StandardDeviation(
    this IEnumerable<int> source)
{
    return Math.Sqrt(source.Variance());
}

public static double StandardDeviation<T>(
    this IEnumerable<T> source,
    Func<T, int> selector)
{
    return StandardDeviation(
    Enumerable.Select(source, selector));
}
```

## 创建并测试并行运算符

这是对使用 `Aggregate` 标准查询运算符构建的顺序代码进行直接适配，使用 `Parallel LINQ Aggregate` 标准查询运算符来推导出并行运算符。Parallel LINQ 运算符是 `ParallelQuery<T>` 类型的扩展方法，而不是 `IEnumerable<T>` 类型。

`Aggregate` 标准查询运算符有一个其顺序对应项不具备的额外参数。你之前读到过，在并行查询执行期间，数据会被分区并由不同的执行线程处理。这使得每个线程的结果必须与其他线程的结果合并，以确保聚合在数学上是成立的。除了 `Update Accumulator` 累加函数（针对每个元素）外，我们还需要提供此 `Combine Accumulator` 累加函数（针对每个结果）。

列表 9-12 显示了没有错误防护或处理的标准查询运算符（我们稍后会介绍）。如果你将其与列表 9-10 中优化的顺序运算符进行比较，你可以看到细微的变化。我们继续使用单次通过聚合函数，但对其进行了更新以适用于并发环境。更改如下：

- 此扩展方法将 `IEnumerable<T>` 替换为 `ParallelQuery<T>`。任何对 `source.AsParallel` 执行的查询都将路由到此扩展方法重载，而不是顺序重载。
- 种子数组使用工厂函数创建；这允许每个分区（通过调用此函数）创建并孤立地操作自身的种子，避免聚合过程中过程中线程之间的任何竞争。
- `Combine Accumulator` 累加函数只需通过索引对左侧和右侧数组进行加法（相同位置元素的求和）。

![](img/a165e601c4b83dd836f659a99a3c067c_316_0.png)

## 列表 9-12 并行的 Variance 和 StandardDeviation 扩展方法

```csharp
public static double Variance(
    this ParallelQuery<int> source)
{
    /* 基于 Igor Ostrovsky 的博客文章 - -
     * http://blogs.msdn.com/pfxteam/archive/2008/06/05/8576194.aspx
     * 该文章演示了如何在 Aggregate 函数中使用工厂函数来提高效率
*/
return source.Aggregate(
    // 种子 - 使用工厂函数构建的三个 double 类型的数组
    // 并初始化为 0
    () => new double[3] { 0.0, 0.0, 0.0 },

    // 项目聚合函数，为每个元素运行
    (subtotal, item) =>
    {
        subtotal[0]++; // 计数
        subtotal[1] += item; // 求和

        // 平方和
        subtotal[2] += (double)item * (double)item;
        return subtotal;
    },

    // 合并函数，
    // 在每个“线程”完成后运行
    (total, thisThread) =>
    {
        total[0] += thisThread[0];
        total[1] += thisThread[1];
        total[2] += thisThread[2];
        return total;
    },

    // 选择器函数
    // 将最终和细化为方差
    // 平均值 = sum / count
    // 方差 = (sum_sqr - sum * mean) / (n - 1)
    (result) =>
    {
        result[2] - (result[1] * (result[1] / result[0]))
        / (result[0] - 1)
    }
);

public static double StandardDeviation(
    this ParallelQuery<int> source)
{
    return Math.Sqrt(source.Variance());
}

public static double StandardDeviation<T>(
    this ParallelQuery<T> source,
    Func<T, int> selector)
{
    return StandardDeviation(
        ParallelEnumerable.Select(source, selector));
}
```

表 9-3 记录了对顺序和并行算法进行的简单性能分析。表 9-3 通过从 HookedOnLINQ.com 下载示例代码记录了 StandardDeviation 运算符的简单性能分析。

## 表 9-3 StandardDeviation 运算符的性能

| 算法 | Array[int] | IEnumerable<int> |
| :--- | :--- | :--- |
| 顺序 – StandardDeviation (列表 10 和 11) | 2,669ms | 3,146ms |
| 并行 – StandardDeviation (列表 12) | 1,469ms | 3,222ms |

## 添加错误处理

编写完我们的运算符后，需要引入对输入和特定错误情况的处理。需要考虑、测试并相应地处理以下输入条件：

- 源参数为 null——为该参数抛出 `ArgumentNullException`。
- 源参数为空——返回 0。
- 源参数只包含一个元素——返回 0。

选择为空数组和包含单个元素的数组返回 0 是针对此运算符和我特定规范的。通常情况下会抛出 `InvalidOperationException`，但对于方差的统计量，我决定在这种情况下避免抛出异常。Microsoft Excel 在计算单元素样本标准差时返回 #DIV/0! 错误，我认为这很陌生，尽管这可能更正确。

空源错误可以通过对 `Variance` 扩展方法进行初始检查轻松处理，正如我们在第 7 节“扩展 LINQ to Objects”中详细看到的那样。通过添加以下代码完成错误检查：

```csharp
if (source == null)
    throw new ArgumentNullException("source");
```

虽然在初始方差计算之前进行空源检查是可以接受的（因为不可避免），但对源中零或单个元素的检查需要一些思考。在聚合函数之前添加检查（如下例所示）可能会对不是索引集合（而是 `IEnumerable<T>`）源数组进行整个枚举：

```csharp
if (source.Any() == false)
    throw new InvalidOperationException("No elements");
```

当我们构建并行运算符时，是为了提高性能，因此对数据源的循环应尽可能少（理想情况下为一次）。我们使用 `Aggregate` 运算符的算法提供了一个理想的解决方案。最终选择器函数可以访问聚合循环中确定的累计计数。我们可以在该处使用三元运算符检查零或单个元素，并在该情况下返回零值。我们避免了额外的循环并满足了
