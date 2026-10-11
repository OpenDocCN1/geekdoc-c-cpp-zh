
# 217 Linq, 语言集成查询 (C# 3.0) 205

- `T ElementAtDefault(int i)` 返回从 0 开始计数的索引 `i` 处的项。如果 `i<0` 或 `i` 大于或等于枚举中的项目数，则返回 `default(T)`。

- `IEnumerable<T> Except(IEnumerable<T> ys)` 返回一个可枚举，该枚举生成不等于 `ys` 中任何项的项，通过默认的等性比较器进行比较。在比较表示法中：`(x | xs, where y in ys)`。还重载为接受一个显式的 `EqualityComparer<T>` 作为最后一个参数。

- `IEnumerable<T> Distinct(T x)` 返回一个可枚举，该枚举恰好生成给定枚举中的每个项，通过默认的等性比较器区分项。还重载为接受一个显式的 `EqualityComparer<T>` 作为最后一个参数。

- `IEnumerable<T> DefaultEmpty()` 如果给定的枚举为空，则返回一个生成与给定枚举相同项的可枚举；否则，它生成一个包含单个项 `default(T)` 的单例枚举。

- `IEnumerable<T> DefaultEmpty(T x)` 如果给定的枚举不为空，则返回一个生成与给定枚举相同项的可枚举；否则，它生成一个包含单个项 `x` 的单例枚举。

`DefaultEmpty` 方法可以与 `GroupJoin` 方法结合使用产生左外连接（示例 242）。

- `int Count()` 返回项目的数量（示例 244）。

- `int Count(Func<T,bool> p)` 作用于每个项 `x`，并返回 `p(x)` 为真的项目数量。

- `IEnumerable<R> Join<U,K,R>(IEnumerable<T> xs, Func<T,K> fx, Func<U,K> fy, Func<T,U,R> g)` 返回一个可枚举，生成项 `r`，每个项都是作为值 `g(x,y)` 获取，其中 `x` 取自给定的枚举 `xs`，`y` 是映射到与 `x` 相同键的项集合。在推导式表示法中：`<g(x,y) | y-ys, where fx(x) = fy(y))`。见示例 240。还重载为接受一个显式的 `EqualityComparer<T>` 作为最后一个参数。

- `IEnumerable<T> Intersect(IEnumerable<T> ys)` 返回一个可枚举，生成给定枚举中在 `ys` 中存在相等项的项，通过默认的等性比较器进行比较。在比较表示法中：`<x | x-xs, where x is in ys>` 还重载为接受一个显式的 `EqualityComparer<T>` 作为最后一个参数。

- `IEnumerable<T> Join<U,K,R>(IEnumerable<T> xs, Func<T,K> fx, Func<U,K> fy, Func<T,U,R> g)` 返回一个可枚举，生成 `g(x,y)` 的值，其中 `x` 取自给定的枚举 `xs`，`y` 取自 `ys`，且满足 `fx(x).Equals(fy(y))`。在推导式表示法中：`<g(x,y) | x-xs, y-ys, where fx(x) = fy(y))`。见示例 240。还重载为接受一个显式的 `EqualityComparer<T>` 作为最后一个参数。

- `T Last()` 如果给定的枚举不为空，则返回最后一个项。如果枚举为空，则抛出 `InvalidOperationException`。

- `T Last(Func<T,bool> p)` 返回给定的枚举中最后一个 `p(x)` 为真的项 `x`（如果存在）。如果枚举为空，则抛出 `InvalidOperationException`。

- `T LastDefault(Func<T,bool> p)` 返回给定的枚举中最后一个 `p(x)` 为真的项 `x`（如果存在）；否则返回 `default(T)`。

- `int LongCount()` 返回给定枚举中的项目数。

- `int LongCount(Func<T,bool> p)` 作用于每个项 `x`，并返回 `p(x)` 为真的项目数量。

- `IEnumerable<IGrouping<T,K>> GroupBy()` 返回一个可枚举，其中项 `x` 根据其 `h(x)` 的值进行分组。结果中的每个组是一个对 `(x, xs)`，其成员是具有相同 `h(x)` 计算出的键 `k` 的 `x`。在比较表示法中：`IGrouping<T,K>` 在第 28.A 节描述。接口 `((k, x | xs, where h(x)=k)) | k--((h(x)) | x))`；函数 `distinct` 返回重复项。

- `IEnumerable<IGrouping<T,K,E>> GroupBy(Func<T,K>, Func<T,E> f)` 返回一个可枚举，其中项 `x` 根据其 `h(x)` 的值分组并并通过 `f(x)` 转换。结果中的每个组是一个对 `(k, vs)`，其成员是具有相同 `h(x)` 计算出的键 `k` 的 `x` 的 `f(x)` 值。在推导式表示法中：`< (k, (f(x)) | x-xs, where h(x) = k)> | k distinct((h(x)) | x-xs))`。见示例 235。

- `IEnumerable<R> GroupBy<K,R>(Func<T,K> h, Func<T,IEnumerable<R>> g)` 返回一个可枚举，生成项 `r`，每个项都是作为值 `g(k, vs)` 获取，其成员是具有相同 `h(x)` 计算出的键 `k` 的项。在推导式表示法中：`<g(k, (x | x-xs, where h(x) = k)) | k distinct((h(x)) | x-xs))>`

- `IEnumerable<R> GroupBy<K,R>(Func<T,K> h, Func<T> f, Func<T,IEnumerable<R>> g)` 返回一个可枚举，生成项 `r`，每个项都是通过对组 `(ks)` 应用 `g` 得到的值 `g(k, vs)`，其成员是具有相同 `h(x)` 计算出的键 `k` 的项 `x` 的 `f(x)` 值。在推导式表示法中：`<g(k, (f(x) | x-xs, where h(x) = k)) | k distinct((h(x)) | x-xs))>`

每个 `GroupBy` 也有一个接受显式 `EqualityComparer<K>` 作为参数的重载。

- `IEnumerable<IGrouping<T,K,E>> GroupBy(Func<T,K>, Func<T,E> f)` 返回一个可枚举，其中项 `x` 根据其 `h(x)` 的值分组并并通过 `f(x)` 转换。结果中的每个组是一个对 `(k, vs)`，其成员是具有相同 `h(x)` 计算出的键 `k` 的 `x` 的 `f(x)` 值。在推导式表示法中：`< (k, (f(x)) | x-xs, where h(x) = k)> | k distinct((h(x)) | x-xs))`。见示例 235。

# 217 Linq, 语言集成查询 (C# 3.0) 205

- `T Max()` 如果给定的枚举不为空，则返回最大项。如果枚举为空，则抛出 `InvalidOperationException`。

- `T Max(Func<T,bool> p)` 返回给定的枚举中最大 `p(x)` 为真的项 `x`（如果存在）。如果没有这样的项，则抛出 `InvalidOperationException`。

- `T MaxDefault()` 如果给定的枚举不为空，则返回最大项；否则返回 `default(T)`。

- `T MaxDefault(Func<T,bool> p)` 返回给定的枚举中最大 `p(x)` 为真的项 `x`（如果存在）；否则返回 `default(T)`。

- `T Min()` 如果给定的枚举不为空，则返回最小项。如果枚举为空，则抛出 `InvalidOperationException`。

- `T Min(Func<T,bool> p)` 返回给定的枚举中最小 `p(x)` 为真的项 `x`（如果存在）。如果没有这样的项，则抛出 `InvalidOperationException`。

- `T MinDefault()` 如果给定的枚举不为空，则返回最小项；否则返回 `default(T)`。

- `T MinDefault(Func<T,bool> p)` 返回给定的枚举中最小 `p(x)` 为真的项 `x`（如果存在）；否则返回 `default(T)`。

- `IEnumerable<T> Reverse()` 返回一个可枚举，按反序生成枚举的项。

- `IEnumerable<R> Select(Func<T, R> f)` 返回一个可枚举，其项为 `f(x1), f(x2), ...` 或在推导式表示法中：`f(x) | x <- xs`。在函数式语言中通常称为 `map`。见示例 235 和238。

- `IEnumerable<R> Select(Func<T, int, R> f)` 返回一个可枚举，其项为 `f(x1, 0), f(x2, 1), ...` 或在推导式表示法中：`f(x, i) | x, i <- zip2(xs, 0) ...` 其中 `zip2` 创建两个枚举的对，而 `0` 是项为 `0, 1` 等的枚举。

- `IEnumerable<R> SelectMany(Func<T, Iumerable<R>> d)` 创建中间枚举 `d(x1) = y1, y2, ...,` 以及 `d(x2) = y21, y22, ...,` 等，然后将其展平并转换成单个可枚举 `f(x1,y1), f(x1,y2), ...` 在推导式表示法中返回：`f(x, y) | x <- xs, y <- d(x)`。在函数式语言中通常称为 `flatMap`。见示例 237。

- `IEnumerable<R> SelectMany(Func<T, int, IEnumerable<R>>)` 创建中间枚举 `d(x1,0) = y11, y12, ...,` 以及 `d(x2,1) = y21, y22, ...,` 等，然后将其展平

# 206 Linq，语言集成查询 (C# 3.0)

合并为单个的可枚举序列 `y11,y12,...,y22` 并返回。在查询表达式表示法中：

```
y | (x,i) <- zip2(x,0..)(Func<T,int,IEnumerable<U>> d, Func<T,U,R> f) 中间 d(x,0) = y11，且 d(x,1) = y22，以此此类推，并展平并将这些转换为单个的可枚举序列 f(x1,y11), f(x1,y12), ..., f(x2,y22)，最后返回。在查询表达式表示法中：
```

```
f(x,y) | (x,i) <- zip2(x,0..).y = d(x,i).
```

- `IEnumerable<R> SelectMany<T,U>(Func<T,int,IEnumerable<U>> d, Func<T,U,R> f)` 中间 `d(x,0) = y11`，且 `d(x,1) = y22`，以此此类推，并展平并将这些转换为单个的可枚举序列 `f(x1,y11), f(x1,y12), ..., f(x2,y22)`，最后返回。在查询表达式表示法中：

- `bool SequenceEqual(IEnumerable<T> ys)` 如果给定的可枚举序列（通过默认相等比较器）的每个项与 `ys` 在相同位置的项相等，且两个可枚举序列的项目数量相同，则返回 `true`；否则返回 `false`。重载以接受显式的 `EqualityComparer<T>` 作为最后一个参数。

- `Single<T>` 返回给定可枚举序列的唯一项。如果可枚举序列为空或包含多一个项，则抛出 `InvalidOperationException`。

- `Single(Func<T,bool> p)` 将 `p` 应用于给定可枚举序列的所有项，并返回第一个使 `p(x)` 为真的给定项 `x`。如果没有这样的项 `x`，或者存在多个项 `x`，则抛出 `InvalidOperationException`。

- `SingleOrDefault(T)` 如果给定可枚举序列不为空，则返回唯一项；否则返回 `default(T)`。如果可枚举序列包含多一个项，则抛出 `InvalidOperationException`。

- `SingleOrDefault(Func<T,bool> p)` 将 `p` 应用于给定可枚举序列的所有项，并返回第一个使 `p(x)` 为真的给定项 `x`；否则返回 `default(T)`。如果可枚举序列中有多个 `x` 使得 `p(x)` 为真，则抛出 `InvalidOperationException`。

- `IEnumerable<T> Skip(int n)` 返回一个生成除前 `n` 个之外的项目的可枚举序列。当 `n<0` 时，生成所有项；当 `n` 大于或等于项目总数时，不生成任何项。

- `IEnumerable<T> SkipWhile(Func<T,bool> p)` 返回一个生成给定可枚举序列尾的可枚举序列，从第一个 `p(x)` 为假的项开始。如果可枚举序列中所有项的 `p(x)` 都为真，则不生成任何项。

- `IEnumerable<T> SkipWhile(Func<T,int,bool> p)` 返回一个生成给定可枚举序列尾的可枚举序列，从第一个 `p(x, i)` 为假的项开始。其中 `x` 是从零开始的 `i`。

- `N Sum(Func<T,N> f)` 将 `f` 应用于可枚举序列的每个项 `x`，并返回值 `f(x)` 的和。仅当 `N` 是数值类型或可空类型时（节 28.6）。

- `IEnumerable<T> Take(int n)` 返回一个生成给定可枚举序列前 `n` 个项的可枚举序列。当 `n<0` ，，不生成任何项；当 `n` 大于或等于项目总数时，生成所有项。

- `IEnumerable<T> TakeWhile(Func<T,bool> p)` 返回一个生成给定可枚举序列最大前缀的可枚举序列，由所有 `p(x)` 为真的项组成。

- `IEnumerable<T> TakeWhile(Func<T,int,bool> p)` 返回一个生成给定可枚举序列最大前缀的可枚举序列，由所有 `p(x, i)` 为真的项组成，其中 `x`位于从零开始的位置 `i`。

- `T[]` 返回一个包含给定可枚举序列项的新数组。

- `Dictionary<K,T> ToDictionary(Func<T,K>, Func<T,T> h)` 返回一个类型为 `DictionaryKey` 的新字典，包含给定可枚举序列中每个项 `x` 的条目 `(h(x), x)`。如果存在两个项 `xi` 和 `xj` 使得 `h(xi)` 等于 `h(xj)`，则抛出 `ArgumentException`。在查询表达式表示法中，新字典的键值对为 `((h(x), x) | xs)`。

- `Dictionary<K,E> ToDictionary(Func<T,K>, Func<T,E> h, Func<T,E> f)` 返回一个类型为 `DictionaryKey` 的新字典，包含给定可枚举序列中每个项 `x` 的条目 `(h(x), f(x))`。如果存在两个项 `xi` 和 `xj` 使得 `h(xi)` 等于 `h(xj)`，则抛出 `ArgumentException`。在查询表达式表示法中，新字典的键值对为 `((h(x), f(x)) | xs)`。

- `List<T>` 返回一个包含给定可枚举序列项的新 `List<T>`。

- `IEnumerable<T> ToLookup(Func<T,K>, Func<T,V> h)` 返回一个新的查找结构，包含 `h` 的每个值 `k` 的条目 `(k, vs)`，其中 `vs` 是可枚举序列中对应值 `k` 的所有 `x f(x)` 的可枚举序列，每个组可以通过索引访问。在查询表达式表示法中，键值对为 `((k, vs) | xs)`。

- `IEnumerable<T> ToLookup(Func<T,K>, Func<T,V> h, Func<T,V> f)` 返回一个新的查找结构，包含 `h` 的每个值 `k` 的条目 `(k, vs)`，其中 `vs` 是可枚举序列中对应值 `k` 的所有 `x f(x)` 的可枚举序列，每个组可以通过索引访问。

- `IEnumerable<T> Union(IEnumerable<T> first, IEnumerable<T> second)` 返回包含两个可枚举序列并集的可枚举序列，不包含重复的项。

- `bool SequenceEqual(IEnumerable<T> ys)` 如果给定的可枚举序列的每个项（通过默认相等比较器）与 `ys` 在相同位置的项相等，且两个可枚举序列的项目数量相同，则返回 `true`；否则返回 `false`。重载以接受显式的 `EqualityComparer<T>` 作为最后一个参数。

- `Single<T>` 返回给定可枚举序列的唯一项。如果可枚举序列为空或包含多一个项，则抛出 `InvalidOperationException`。

- `Single(Func<T,bool> p)` 将 `p` 应用于给定可枚举序列的所有项，并返回第一个使 `p(x)` 为真的给定项 `x`。如果没有这样的项 `x`，或者存在多个项 `x`，则抛出 `InvalidOperationException`。

- `SingleOrDefault(T)` 如果给定可枚举序列不为空，则返回唯一项；否则返回 `default(T)`。如果可枚举序列包含多一个项，则抛出 `InvalidOperationException`。

- `SingleOrDefault(Func<T,bool> p)` 将 `p` 应用于给定可枚举序列的所有项，并返回第一个使 `p(x)` 为真的给定项 `x`；否则返回 `default(T)`。如果可枚举序列中有多个 `x` 使得 `p(x)` 为真，则抛出 `InvalidOperationException`。

- `IEnumerable<T> Skip(int n)` 返回一个生成除前 `n` 个之外的项目的可枚举序列。当 `n<0` 时，生成所有项；当 `n` 大于或等于项目总数时，不生成任何项。

- `IEnumerable<T> SkipWhile(Func<T,bool> p)` 返回一个生成给定可枚举序列尾的可枚举序列，从第一个 `p(x)` 为假的项开始。如果可枚举序列中所有项的 `p(x)` 都为真，则不生成任何项。

- `IEnumerable<T> SkipWhile(Func<T,int,bool> p)` 返回一个生成给定可枚举序列尾的可枚举序列，从第一个 `p(x, i)` 为假的项开始。其中 `x` 是从零开始的 `i`。

- `N Sum(Func<T,N> f)` 将 `f` 应用于可枚举序列的每个项 `x`，并返回值 `f(x)` 的和。仅当 `N` 是数值类型或可空类型时（节 28.6）。
