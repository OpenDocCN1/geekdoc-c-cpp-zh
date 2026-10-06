

# Linq, 语言集成查询 (C# 3.0) 203

- int Count() 返回项目的数量（示例 244）。
- int Count(Func<T,bool> p) 作用于每个项 x，并返回使 p(x) 为真的项目数量。
- IEnumerable<T> DefaultEmpty() 如果给定的枚举不为空，则返回一个生成与给定枚举相同项的可枚举；否则，它生成一个包含单个项 default(T) 的单例枚举。
- IEnumerable<T> DefaultEmpty(T x) 如果给定的枚举为空，则返回一个生成与给定枚举相同项的可枚举；否则，它生成一个包含单个项 x 的单例枚举。

DefaultEmpty 方法可以与 GroupJoin 方法结合使用产生左外连接（示例 242）。

- IEnumerable<T> Distinct(T x) 返回一个可枚举，该枚举恰好生成给定枚举中的每个项，通过默认的等性比较器区分项。还重载为接受一个显式的 EqualityComparer<T> 作为最后一个参数。
- T Element(int i) 返回从 0 开始计数的索引 i 处的项。如果 i<0 或 i 大于或等于枚举中的项目数，则抛出 OutOfRangeException。
- T ElementAtDefault(int i) 返回从 0 开始计数的索引 i 处的项。如果 i<0 或 i 大于或等于枚举中的项目数，则返回 default(T)。
- IEnumerable<T> Except(IEnumerable<T> ys) 返回一个可枚举，该枚举生成不等于 ys 中任何项的项，通过默认的等性比较器进行比较。在比较表示法中：(x | xs, where y in ys)。还重载为接受一个显式的 EqualityComparer<T> 作为最后一个参数。
- T First() 如果给定的枚举不为空，则返回第一个项。如果枚举为空，则抛出 InvalidOperationException。
- T First(Func<T,bool> p) 返回给定的枚举中第一个 p(x) 为真的项 x（如果存在）。如果没有这样的项，则抛出 InvalidOperationException。
- T FirstDefault() 如果给定的枚举不为空，则返回第一个项；否则返回 default(T)。
- T FirstDefault(Func<T,bool> p) 返回给定的枚举中第一个 p(x) 为真的项 x（如果存在）；否则返回 default(T)。
- IEnumerable<IGrouping<T,K>> GroupBy() 返回一个可枚举，其中项 x 根据其 h(x) 的值进行分组。结果中的每个组是一个对 (x, xs)，其成员是具有相同 h(x) 计算出的键 k 的 x。在比较表示法中：IGrouping<T,K> 在第 28.A 节描述。接口 ((k, x | xs, where h(x)=k)) | k--((h(x)) | x));函数 distinct 返回重复项。
- IEnumerable<IGrouping<T,K,E>> GroupBy(Func<T,K>, Func<T,E> f) 返回一个可枚举，其中项 x 根据其 h(x) 的值分组并并通过 f(x) 转换。结果中的每个组是一个对 (k, vs)，其成员是具有相同 h(x) 计算出的键 k 的 x 的 f(x) 值。在推导式表示法中：<(k, (f(x)) | x-xs, where h(x) = k)> | k distinct((h(x)) | x-xs))。见示例 235。
- IEnumerable<R> GroupBy<K,R>(Func<T,K> h, Func<T,IEnumerable<R>> g) 返回一个可枚举，生成项 r，每个项都是作为值 g(k, vs) 获取，其成员是具有相同 h(x) 计算出的键 k 的项。在推导式表示法中：<g(k, (x | x-xs, where h(x) = k)) | k distinct((h(x)) | x-xs))>
- IEnumerable<R> GroupBy<K,R>(Func<T,K> h, Func<T> f, Func<T,IEnumerable<R>> g) 返回一个可枚举，生成项 r，每个项都是通过对组 (ks) 应用 g 得到的值 g(k, vs)，其成员是具有相同 h(x) 计算出的键 k 的项 x 的 f(x) 值。在推导式表示法中：<g(k, (f(x) | x-xs, where h(x) = k)) | k distinct((h(x)) | x-xs))>

每个 GroupBy 也有一个接受显式 EqualityComparer<K> 作为参数的重载。

- IEnumerable<R> Join<U,K,R>(IEnumerable<T> xs, Func<T,K> fx, Func<U,K> fy, Func<T,U,R> g) 返回一个可枚举，生成项 r，每个项都是作为值 g(x,y) 获取，其中 x 取自给定的枚举 xs，y 是映射到与 x 相同键的项集合。在推导式表示法中：<g(x,y) | y-ys, where fx(x) = fy(y))。见示例 240。还重载为接受一个显式的 EqualityComparer<T> 作为最后一个参数。
- IEnumerable<T> Intersect(IEnumerable<T> ys) 返回一个可枚举，生成给定枚举中在 ys 中存在相等项的项，通过默认的等性比较器进行比较。在比较表示法中：<x | x-xs, where x is in ys> 还重载为接受一个显式的 EqualityComparer<T> 作为最后一个参数。
- IEnumerable<T> Join<U,K,R>(IEnumerable<T> xs, Func<T,K> fx, Func<U,K> fy, Func<T,U,R> g) 返回一个可枚举，生成 g(x,y) 的值，其中 x 取自给定的枚举 xs，y 取自 ys，且满足 fx(x).Equals(fy(y))。在推导式表示法中：<g(x,y) | x-xs, y-ys, where fx(x) = fy(y))。见示例 240。还重载为接受一个显式的 EqualityComparer<T> 作为最后一个参数。
- T Last() 如果给定的枚举不为空，则返回最后一个项。如果枚举为空，则抛出 InvalidOperationException。
- T Last(Func<T,bool> p) 返回给定的枚举中最后一个 p(x) 为真的项 x（如果存在）。如果枚举为空，则抛出 InvalidOperationException。
- T LastDefault(Func<T,bool> p) 返回给定的枚举中最后一个 p(x) 为真的项 x（如果存在）；否则返回 default(T)。
- int LongCount() 返回给定枚举中的项目数。
- int LongCount(Func<T,bool> p) 作用于每个项 x，并返回 p(x) 为真的项目数量。

# 204 Linq, 语言集成查询 (C# 3.0)

- T First() 如果给定的枚举不为空，则返回第一个项。如果枚举为空，则抛出 InvalidOperationException。
- T First(Func<T,bool> p) 返回给定的枚举中第一个 p(x) 为真的项 x（如果存在）。如果没有这样的项，则抛出 InvalidOperationException。
- T FirstDefault() 如果给定的枚举不为空，则返回第一个项；否则返回 default(T)。
- T FirstDefault(Func<T,bool> p) 返回给定的枚举中第一个-

- T Element(int i) 返回从 0 开始计数的索引 i 处的项。如果 i<0 或 i 大于或等于枚举中的项目数，则抛出 OutOfRangeException。
- T ElementAtDefault(int i) 返回从 0 开始计数的索引 i 处的项。如果 i<0 或 i 大于或等于枚举中的项目数，则返回 default(T)。
- IEnumerable<T> Except(IEnumerable<T> ys) 返回一个可枚举，该枚举生成不等于 ys 中任何项的项，通过默认的等性比较器进行比较。在比较表示法中：(x | xs, where y in ys)。还重载为接受一个显式的 EqualityComparer<T> 作为最后一个参数。
- IEnumerable<T> Distinct(T x) 返回一个可枚举，该枚举恰好生成给定枚举中的每个项，通过默认的等性比较器区分项。还重载为接受一个显式的 EqualityComparer<T> 作为最后一个参数。
- IEnumerable<T> DefaultEmpty() 如果给定的枚举为空，则返回一个生成与给定枚举相同项的可枚举；否则，它生成一个包含单个项 default(T) 的单例枚举。
- IEnumerable<T> DefaultEmpty(T x) 如果给定的枚举不为空，则返回一个生成与给定枚举相同项的可枚举；否则，它生成一个包含单个项 x 的单例枚举。

DefaultEmpty 方法可以与 GroupJoin 方法结合使用产生左外连接（示例 242）。
- int Count() 返回项目的数量（示例 244）。
- int Count(Func<T,bool> p) 作用于每个项 x，并返回 p(x) 为真的项目数量。
- IEnumerable<R> Join<U,K,R>(IEnumerable<T> xs, Func<T,K> fx, Func<U,K> fy, Func<T,U,R> g) 返回一个可枚举，生成项 r，每个项都是作为值 g(x,y) 获取，其中 x 取自给定的枚举 xs，y 是映射到与 x 相同键的项集合。在推导式表示法中：<g(x,y) | y-ys, where fx(x) = fy(y))。见示例 240。还重载为接受一个显式的 EqualityComparer<T> 作为最后一个参数。
- IEnumerable<T> Intersect(IEnumerable<T> ys) 返回一个可枚举，生成给定枚举中在 ys 中存在相等项的项，通过默认的等性比较器进行比较。在比较表示法中：<x | x-xs, where x is in ys> 还重载为接受一个显式的 EqualityComparer<T> 作为最后一个参数。
- IEnumerable<T> Join<U,K,R>(IEnumerable<T> xs, Func<T,K> fx, Func<U,K> fy, Func<T,U,R> g) 返回一个可枚举，生成 g(x,y) 的值，其中 x 取自给定的枚举 xs，y 取自 ys，且满足 fx(x).Equals(fy(y))。在推导式表示法中：<g(x,y) | x-xs, y-ys, where fx(x) = fy(y))。见示例 240。还重载为接受一个显式的 EqualityComparer<T> 作为最后一个参数。
- T Last() 如果给定的枚举不为空，则返回最后一个项。如果枚举为空，则抛出 InvalidOperationException。
- T Last(Func<T,bool> p) 返回给定的枚举中最后一个 p(x) 为真的项 x（如果存在）。如果枚举为空，则抛出 InvalidOperationException。
- T LastDefault(Func<T,bool> p) 返回给定的枚举中最后一个 p(x) 为真的项 x（如果存在）；否则返回 default(T)。
- int LongCount() 返回给定枚举中的项目数。
- int LongCount(Func<T,bool> p) 作用于每个项 x，并返回 p(x) 为真的项目数量。
- IEnumerable<IGrouping<T,K>> GroupBy() 返回一个可枚举，其中项 x 根据其 h(x) 的值进行分组。结果中的每个组是一个对 (x, xs)，其成员是具有相同 h(x) 计算出的键 k 的 x。在比较表示法中：IGrouping<T,K> 在第 28.A 节描述。接口 ((k, x | xs, where h(x)=k)) | k--((h(x)) | x));函数 distinct 返回重复项。
- IEnumerable<IGrouping<T,K,E>> GroupBy(Func<T,K>, Func<T,E> f) 返回一个可枚举，其中项 x 根据其 h(x) 的值分组并并通过 f(x) 转换。结果中的每个组是一个对 (k, vs)，其成员是具有相同 h(x) 计算出的键 k 的 x 的 f(x) 值。在推导式表示法中：<(k, (f(x)) | x-xs, where h(x) = k)> | k distinct((h(x)) | x-xs))。见示例 235。
- IEnumerable<R> GroupBy<K,R>(Func<T,K> h, Func<T,IEnumerable<R>> g) 返回一个可枚举，生成项 r，每个项都是作为值 g(k, vs) 获取，其成员是具有相同 h(x) 计算出的键 k 的项。在推导式表示法中：<g(k, (x | x-xs, where h(x) = k)) | k distinct((h(x)) | x-xs))>
- IEnumerable<R> GroupBy<K,R>(Func<T,K> h, Func<T> f, Func<T,IEnumerable<R>> g) 返回一个可枚举，生成项 r，每个项都是通过对组 (ks) 应用 g 得到的值 g(k, vs)，其成员是具有相同 h(x) 计算出的键 k 的项 x 的 f(x) 值。在推导式表示法中：<g(k, (f(x) | x-xs, where h(x) = k)) | k distinct((h(x)) | x-xs))>

每个 GroupBy 也有一个接受显式 EqualityComparer<K> 作为参数的重载。
- IEnumerable<IGrouping<T,K,E>> GroupBy(Func<T,K>, Func<T,E> f) 返回一个可枚举，其中项 x 根据其 h(x) 的值分组并并通过 f(x) 转换。结果中的每个组是一个对 (k, vs)，其成员是具有相同 h(x) 计算出的键 k 的 x 的 f(x) 值。在推导式表示法中：<(k, (f(x)) | x-xs, where h(x) = k)> | k distinct((h(x)) | x-xs))。见示例 235。 (对不起对不起翻译翻译翻译翻译翻译翻译翻译翻译翻译翻译翻译翻译翻译))

# 217 Linq, 语言集成查询 (C# 3.0) 205

# 217 Linq, 语言集成查询 (C# 3.0) 205

- T Max() 如果给定的枚举不为空，则返回最大项。如果枚举为空，则抛出 InvalidOperationException。
- T Max(Func<T,bool> p) 返回给定的枚举中最大 p(x) 为真的项 x（如果存在）。如果没有这样的项，则抛出 InvalidOperationException。
- T MaxDefault() 如果给定的枚举不为空，则返回最大项；否则返回 default(T)。
- T MaxDefault(Func<T,bool> p) 返回给定的枚举中最大 p(x) 为真的项 x（如果存在）；否则返回 default(T)。
- T Min() 如果给定的枚举不为空，则返回最小项。如果枚举为空，则抛出 InvalidOperationException。
- T Min(Func<T,bool> p) 返回给定的枚举中最小 p(x) 为真的项 x（如果存在）。如果没有这样的项，则抛出 InvalidOperationException。
- T MinDefault() 如果给定的枚举不为空，则返回最小项；否则返回 default(T)。
- T MinDefault(Func<T,bool> p) 返回给定的枚举中最小 p(x) 为真的项 x（如果存在）；否则返回 default(T)。
- IEnumerable<T> Reverse() 返回一个可枚举，按反序生成枚举的项。
- IEnumerable<R> Select(Func<T, R> f) 返回一个可枚举，其项为 f(x1), f(x2), ... 或在推导式表示法中：f(x) | x <- xs。在函数式语言中通常称为 map。见示例 235 和238。
- IEnumerable<R> Select(Func<T, int, R> f) 返回一个可枚举，其项为 f(x1, 0), f(x2, 1), ... 或在推导式表示法中：f(x, i) | x, i <- zip2(xs, 0) ... 其中 zip2 创建两个枚举的对，而 0 是项为 0, 1 等的枚举。
- IEnumerable<R> SelectMany(Func<T, Iumerable<R>> d) 创建中间枚举 d(x1) = y1, y2, ..., 以及 d(x2) = y21, y22, ..., 等，然后将其展平并转换成单个可枚举 f(x1,y1), f(x1,y2), ... 在推导式表示法中返回：f(x, y) | x <- xs, y <- d(x)。在函数式语言中通常称为 flatMap。见示例 237。
- IEnumerable<R> SelectMany(Func<T, int, IEnumerable<R>>) 创建中间枚举 d(x1,0) = y11, y12, ..., 以及 d(x2,1) = y21, y22, ..., 等，然后将其展平

