

# Linq，语言集成查询 (C# 3.0) 199

## 示例 241 Linq orderby 子句
使用示例 234 中的 xs 和 ys，这里的第一个 orderby 示例使 select 按降序顺序处理 x。第二个 orderby 示例使 select 按（主要按）x 的降序顺序和（次要按）字符串 y 长度的降序顺序来处理二元组 (x, y)。

```csharp
Show(from x in xs // 25 9
    orderby x descending
    select x);
Show(xs.OrderByDescending(x => x).Select(x => x*));
```

```csharp
Show(from x in xs // { x=5, y=C } { x=5, y=BB } ... { x=2, y=BA }
    from y in ys
    orderby x descending, y.Length
    select new { x, y });
Show(xs.SelectMany(x => ys, (x, y) => new { x, y }
    .OrderByDescending(xy => xy.x)
    .ThenBy(xy => xy.y.Length)
    .Select(xy => xy.x));
```

## 示例 242 Linq 中的左外连接
内连接（示例 240）会忽略左侧在右侧没有匹配 y 的项。相比之下，左连接也包含项 x，可以通过 join 结合 DefaultEmpty（第 28.5 节）来计算。

```csharp
Show(from x in xs // { x=2, z=C } { x=3, z=BB } { x=3, z=BA } { x=5, z=null }
    join y in ys on x-1 equals y into zs
    from z in zs.DefaultEmpty()
    select new { x, z });
Show(xs.GroupJoin(ys, x => x-1, y => y.Length, (x, zs) => new { x, zs }
    .SelectMany(zs => zs.DefaultEmpty(), (x, z) => new { x.x, z, z }));
```

## 示例 243 连续性，到 Into 子句
与 234 类似，查询的前两行创建一个包含组的流，其中第一组有 2 和两个成员 (4, 25)，而第二组有 0 和一个成员 (9)。查询继续到 g 将范围变量 g 中的每个组绑定到 g 是 g.Key。组的成员可以通过枚举 g 来获取，g 本身是一个非空序列。

```csharp
Show(from x in xs // 20
    group x*x by x%3
    into g
    select g.Key);
Show(xs.GroupBy(x => x*x, x => x*x).Select(g => g.Key));
```

## 28.3 Linq 和 SQL 之间的区别

Linq 查询 select ... 与 SQL 查询 select from ... 相当相似，但不能使用 `*`，且某些在表述为 SQL 查询一部分的操作必须在 Linq 中通过调用结果上的方法来表示：

- 代替 SQL 的 `SELECT COUNT(*) FROM ...`，在 Linq 中使用 `(from select ...).Count()`。同样，代替其他 SQL 聚合函数 AVG、MAX、MIN 和 SUM，Linq 使用第 28.6 节描述的扩展方法 `Average()`、`Max()`、`Min()` 和 `Sum()`。
- 代替 SQL 的 `DISTINCT(...) FROM ...`，在 Linq 中使用 `(from select ...).Distinct()`。
- 代替 SQL 的 `UNION (SELECT ...) UNION (SELECT ...)`，在 Linq 中使用 `(from ...).Union(from select ...)`。
同样，代替 SQL 的 EXCEPT 和 intersect 运算符，Linq 使用扩展方法 `Except` 和 `Intersect`。
- 代替 SQL 的 `HAVING` 运算符，`group ... by ... int g where ...`。

## 28.4 支持 Linq 的辅助接口 (C# 3.0)

Enables 支持 Linq 查询是因为 `IEnumerable<T>` 接口通过其扩展方法（方法 28.5 节）实现了查询模式（第 27.2 节）。查询表达式中的 Gp<K,T> 和 O<T> 部分由两个额外的接口实现：`IGrouping<K,T>` 和 `IOrderedEnumerable<T>`。

`System.Linq` 命名空间下的 `IGrouping<K,T>` 扩展 `IEnumerable<T>` 并用于表示一组项。`GroupBy` 等扩展方法产生 `IGrouping<K,T>` 对象的的可枚举集合（第 28.5 节）。`IGrouping<K,T>` 支持对其项进行枚举，因为它派自 `IEnumerable<T>`，此外还可以返回组的键：

- 只读属性 `Key` 返回组的键。

`System.Linq` 命名空间下的 `ILookup<K,T>` 扩展 `IEnumerable<IGrouping<K,T>>` 并表示项组的集合。该接口派自 `IGrouping<K,T>` 并支持其定义的所有方法。此外，`ILookup<K,T>` 可以：

- 只读索引器 `[k]` 返回键 k 的组。
- 只读属性 `Count` 返回组的数量。

`IOrderedEnumerable<T>` 扩展 `IEnumerable<T>` 并表示已排序的项。该接口派自 `IEnumerable<T>` 并支持所有定义的方法。进一步的排序（通过 `ThenBy` 和 `ThenDescending`）遵循了已应用的排序顺序。

## 示例 245 带过滤的查询：SQL HAVING
与 243 类似，组被绑定到范围变量 g。在这里，对组进行了过滤以丢弃。

```csharp
Show(from x in xs // 2
    group x by
    into g
    where g.Count() > 1
    select g.Key);
```

## 示例 246 连续性，到 Into 子句
与 234 类似，查询的前两行创建一个包含组的流，其中第一组有 2 和两个成员 (4, 25)，第二组有 0 和一个成员 (9)。查询继续到 g 将范围变量 g 中的每个组绑定到 g 是 g.Key。组的成员可以通过枚举 g 来获取，g 本身是一个非空序列。

```csharp
Show(from x in xs // 20
    group x*x by x%3
    into g
    select g.Key);
```

## 示例 247 组合组
此示例展示了如何将多个组组合为一个结果。

```csharp
Show(from x in xs
    group x by x%3 into g1
    from y in ys
    group y by y%3 into g2
    select new { g1, g2 });
```

## 示例 248 组连接
此示例展示了如何根据公共键连接两个组。

```csharp
Show(from x in xs
    group x by x%3 into g1
    from y in ys
    group y by y%3 into g2
    join k1 in g1.Key from k2 in g2.Key on k1 == k2
    select new { g1, g2 });
```

## 示例 249 平化组
此示例展示了如何将组扁平化为序列。

```csharp
Show(from x in xs
    group x by x%3 into g
    from item in g
    select item);
```

## 示例 250 投影组
此示例展示了如何将每个组投影为一个对象。

```csharp
Show(from x in xs
    group x by x%3 into g
    select new { Key = g.Key, Count = g.Count() });
```
