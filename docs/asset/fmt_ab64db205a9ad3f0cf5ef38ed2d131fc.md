
在这里，`builder` 是任何计算表达式构建器，这是一个实现了某些定义成员的特殊对象，编译器会解析计算表达式中的构造。表 25-12 总结了这些构造，提供了 F# 语言的一个子集以及如 `let` 和 `use!` 等增强功能，你可以在计算表达式中使用它们。

**表 25-12：计算表达式中的构造**

| 构造 | 底层表示 |
| --- | --- |
| () | `b.Zero()` |
| `let pat = expr in cexpr` | `b.Let(expr, (fun pat -> [expr]))` |
| `let! pat = expr in cexpr` | `b.Bind(expr, (fun pat -> [expr]))` |
| `use pat = expr in cexpr` | `b.Using(expr, (fun pat -> [expr]))` |
| `use! pat = expr in cexpr` | `b.Bind(expr, (fun x -> b.Using(x, (fun pat -> [expr]))))` |
| `do expr in cexpr` | `b.Let(expr, (fun () -> [expr]))` |
| `do! expr in cexpr` | `b.Bind(expr, (fun () -> [expr]))` |
| `if expr then cexpr` | `if expr [expr] else b.Zero()` |
| `if expr then cexpr else cexpr` | `if expr [expr] else [cexpr2]` |

## 序列

所有的 F# 集合（如列表和数组）都实现了 `System.Collections.IEnumerable<T>` 接口。在 F# 代码中，你经常看到此接口类型写作 `seq<T>`，它是该接口类型的类型缩写。与 .NET 代码一样，序列（sequences）是惰性数据结构。它们是按需枚举的，在请求它们之前，序列值不会被计算。

重要的一点是，使用序列，你可以通过对各种 `Seq.*` 静态成员操作将 F# 列表和数组变为惰性的。正如你将看到的，这些操作与表 25-11 中 `List` 模块定义的聚合操作之间有很多相似之处，事实上，这对于所有 F# 集合也是如此。然而，`Seq` 模块还支持以多种方式计算最小值、平均值、排序和平均，以及遍历以选取元素。

**表 25-14:** Seq 模块中的可选聚合操作符

| 函数 | 类型 | 描述 |
| :--- | :--- | :--- |
| `Seq.append` | `seq<'T> -> seq<'T> -> seq<'T>` | 附加两个序列，保持结果为惰性。 |
| `Seq.average` | `seq<'T> -> 'T` | 计算序列中元素的平均值。 |
| `Seq.cast` | `IIIEnumerable -> seq<'T>` | 将无类型集合封装为类型化序列。 |
| `Seq.choose` | `('T -> 'U) -> seq<'T> -> seq<'U>` | 返回一个新序列，其元素在应用于给定谓词时返回 Some。 |
| `Seq.collect` | `('T -> seq<'U>) -> seq<'T> -> seq<'U>` | 将函数应用于每个元素，并返回一个连接了结果的新序列。 |
| `Seq.concat` | `seq<'T> -> seq<'T>` | 将序列的序列连接为单个序列。 |
| `Seq.distinct` | `'T -> seq<'T>` | 返回所有不同的元素。 |
| `Seq.empty` | `seq<'T>` | 返回空序列。 |
| `Seq.exists` | `('T -> bool) -> seq<'T> -> bool` | 测试是否有元素满足给定的谓词。 |
| `Seq.filter` | `('T -> bool) -> seq<'T> -> seq<'T>` | 过滤所有满足给定谓词的元素。 |
| `Seq.find` | `('T -> bool) -> seq<'T> -> 'T` | 找到满足给定谓词的第一个元素。 |
| `Seq.fold` | `('State -> 'T -> 'State) -> 'State -> seq<'T> -> 'State` | 将给定函数应用于序列中的每个元素，在每次调用时传递结果。 |
| `Seq.forall` | `('T -> bool) -> seq<'T> -> bool` | 测试序列中的所有元素是否满足给定的谓词。 |
| `Seq.head` | `Seq<'T> -> 'T` | 返回序列的头部。 |
| `Seq.isEmpty` | `Seq<'T> -> bool` | 测试序列是否为空。 |
| `Seq.iter` | `('T -> unit) -> seq<'T> -> unit` | 将给定函数应用于序列的每个元素。 |
| `Seq.length` | `Seq<'T> -> int` | 返回序列的长度。 |
| `Seq.map` | `('T -> 'U) -> seq<'T> -> seq<'U>` | 将给定函数映射到每个元素并返回一个新序列。 |
| `Seq.max` | `Seq<'T> -> 'T` | 计算序列中最大的元素。 |
| `Seq.min` | `Seq<'T> -> 'T` | 计算序列中最小的元素。 |
| `Seq.nth` | `Int -> Seq<'T> -> 'T` | 计算序列中的第 n 个元素。 |
| `Seq.ofarray` | `'T [] -> seq<'T>` | 将数组转换为序列。 |
| `Seq.oflist` | `'T list -> seq<'T>` | 将列表转换为序列。 |
| `Seq.pick` | `('T -> 'U) -> seq<'T> -> 'U` | 返回给定函数返回 Some 的第一个元素。 |
| `Seq.reduce` | `('T -> 'T -> 'T) -> seq<'T> -> 'T` | 将函数应用于前两个元素并返回剩余的结果。 |
| `Seq.singleton` | `'T -> seq<'T>` | 构建包含单个元素的序列。 |
| `Seq.skip` | `Int -> seq<'T> -> seq<'T>` | 跳过指定数量的元素并产生序列的序列。 |
| `Seq.sort` | `Seq<'T> -> seq<'T>` | 对序列排序（枚举所有元素）。 |
| `Seq.sum` | `Seq<'T> -> 'T` | 返回序列的和。 |
| `Seq.take` | `Int -> seq<'T> -> seq<'T>` | 返回前 N 个元素。 |
| `Seq.toArray` | `Seq<'T> -> 'T[]` | 将序列转换为数组。 |
| `Seq.toList` | `Seq<'T> -> 'T list` | 将序列转换为列表。 |
| `Seq.truncate` | `Int -> seq<'T> -> seq<'T>` | 将序列截断为最多 N 个元素。 |
| `Seq.tryFind` | `('T -> bool) -> seq<'T> -> 'T option` | 同 `Seq.find`，但如果没有找到满足谓词的元素则返回 None。 |
| `Seq.tryPick` | `('T -> 'U option) -> seq<'T> -> 'U option` | 同 `Seq.pick`，但如果找不到元素则返回 None。 |
| `Seq.windowed` | `Int -> seq<'T> -> seq<'T[]>` | 返回指定大小的滑动窗口，以新数组表示。 |
| `Seq.zip` | `Seq<'T> -> seq<'U> -> 'T * 'U` | 将两个序列（假设长度相同）组合为元组序列。 |
| `Seq.zip3` | `Seq<'T> -> seq<'U> -> seq<'V> -> 'T * 'U * 'V` | 将三个序列（假设长度相同）组合为三元组序列。 |

## 范围表达式

除了表 25-24 中的各种成员外，还可以通过其他方式构造序列。例如，可以使用范围表达式构造数值序列，这是在本章后面看到的更通用的序列表达式：

```
seq ( 0 .. 100 )
```

构造了一个 0 到 100 之间的整数序列，按需提供。如果你需要其他类型的元素，可以在范围表达式的第一个和最后一个元素添加类型后缀，以产生 float32 值的序列：

```
seq ( 0.0f .. 100.0f )
```

还可以使用 skip 值来指定增量。例如，以下代码将给你 0 到 100 之间的所有偶数。

```
seq ( 0 .. 2 .. 100 )
```

## 序列表达式

序列表达式是计算表达式的一种，使用 `seq` 计算构造器构建，产生序列。它们是一种多用途的抽象，在编译器语法方面有特殊处理。你可以将它们用于许多不同的目的——例如，创建计算元素的流，或增量地提供大型集合。考虑以下函数 `AllFiles`，它返回给定文件夹及其所有子文件夹中的文件名：

```fsharp
open System.IO

let rec AllFiles folder =
  seq ( for file in Directory.GetFiles folder do
    yield file
    for subfolder in Directory.GetDirectories folder do
      yield! AllFiles subfolder )
```

这包含两个部分。首先，它使用单个 System.IO 调用获取给定文件夹中的所有文件并逐个提供它们的名称。记住序列是惰性数据结构，元素只有在请求时才被计算。

一旦提供了指定文件夹中的所有文件，函数的第二部分获取所有文件夹并递归调用枚举文件。注意使用 `yield!` 将结果序列展平为正在产生的序列。

在 `seq` 计算内部可以使用的表达式语言方面，通用计算能力不支持以下结构：

- `let!`
- `use!`
- `return`（你必须使用 `yield` 从序列表达式返回值）

所有其他都是可用的，你可以使用它们来构建序列计算。此外，正如你之前看到的，你还可以使用 `yield!` 将值序列展平，并作为你正在构建的原始序列的一部分返回它们。

## 异步流

异步工作流允许你编写执行非阻塞的代码。这通常是非常理想的——例如，在需要在后台执行某些密集计算的同时保持 UI 活跃的情况下。在这里，你的应用程序设计不是单线程的，以避免计算成为应用程序的瓶颈。

计算的一个重要特性是它更偏向 CPU 还是更偏向 I/O——换句话说，它大部分时间是在计算（100% 运行 CPU），还是在等待本质较慢的 I/O 操作完成。

考虑以下伪代码，其中 `processUrl` 涉及 CPU 和 I/O 密集活动。（为了讨论这些目的，它下载通过 URL 可用的文本文件内容并统计其中的单词数。）假设此函数的两次调用是独立的。

```fsharp
let result1 = processUrl(...)
let result2 = processUrl(...)
```

按照目前的写法，这段在单线程上执行异步的代码将花费宝贵的时间等待 I/O 操作完成（例如，访问包含请求资源的服务器的延迟），而它在此期间可以转而执行某些 CPU 操作。这看起来可能没什么。但如果你有大量类似的调用，开销可能会迅速累积，你通过使应用程序更并行而能获得的“速度”提升可能是非常巨大的。

你需要创建线程的能力，并且在线程内部指定异步执行的点，允许线程睡眠直到异步操作返回，并让另一个线程在在此期间做一些更有用的事情。

F# 异步工作流（asynchronous workflows）让你能够实现这一操作。你在前面的节节中用于操作 `Microsoft.Sharp.Control.Async` 类值的工作流提供了模型异步计算的表示，并包含了各种用于手动构造和操作 `Async` 值的成员（以防你需要更细粒度的控制）。

首先，创建一个表示要处理 URL 的 `Async`。你可以看到一个快速且简单的实现，它对计算通过 URL 访问文本文件的字数提供了良好的近似：

```fsharp
let processUrl url = 
async (
    let uri = new System.Uri(url)
    let client = new System.Net.WebClient()
    let content = client.AsyncDownloadString url
    let res =
        content.Split([ |'\'|'r'|'t'|'/'|'||'\'|'\''|'='|';' ' |])
        |> Seq.filter (fun s -> s <> "")
        |> Seq.distinct
        |> Seq.length
    return res)
```

`Microsoft.Sharp.Control.WebExtensions`

你在定义 `processUrl` 之前打开的 `Microsoft.Sharp.Control.WebExtensions` 模块包含了几个扩展成员（在 F# 术语中称为类型增强），它们使得从基于 Web 的活动创建 `Async` 值变得更容易。特别是 `AsyncDownloadString`，它接受一个 `Uri` 参数并返回一个将其内容下载为字符串的异步计算。

请注意，在之前的计算中，`AsyncDownloadString` 是使用 `let` 调用的。事实上，在异步表达式中，`let` 绑定通过异步调用右侧来实现（因此它必须是一个 `Async` 值），并让线程睡眠直到计算返回——本质上，这为你提供了一种方便处理异步计算的语法糖。

如果你真的从使 `processUrl` 异步化中获益，你必须分叉几个线程并让它们并行竞争。因此，作为第二步，你可以获取几个文本 URL，将它们映射到 `Async` 值，并行运行它们，并通过运行 `Async.RunSynchronously` 将它们的结果收集到一个结果中。

```fsharp
let pages =
[ "http://www.google.com/robots.txt"
  "http://www.yahoo.com/robots.txt"
  "http://www.bing.com/robots.txt" ]
let res =
  pages
  |> List.map processUrl
  |> Async.Parallel
  |> Async.RunSynchronously
```

如果你仔细观察，这会产生一个 `(string * int)` 元组列表，每个元组代表 URL 和相应的字数。最后，你可以直接将它们打印在屏幕上：

```fsharp
res
|> Array.iter (fun (url, wcount) ->
  printf "The page at %s has approx. %d\n" url wcount)
```

由于通过 URL 定位远程文件具有较高的延迟，当你增加要处理的 URL 数量时，这种实现的性能会好得多。与其顺序处理这些 URL，此版本能够将工作分散到几个线程上，并通过保持 CPU 尽可能繁忙来最小化空闲时间。

# 模式匹配 (Pattern Matching)

在本章较早之前，你已经看到如何使用模式匹配来检查判别联合（discriminated union）值。不仅于此，你可以使用模式匹配来检查各种不同类型的值。请表 25-15。

表 25-15：基本模式匹配案例

| 模式案例 | 示例 | 描述 |
|---|---|---|
| null | null | 匹配指定的字面量 |
| Lit | 12 | 匹配指定的字面量 |
| Id | Str | 匹配任何值并将其绑定到 id |
| _ | _ | 匹配任何值但不进行绑定 |
| id(patt,...) | Binop(f, opl, op2) | 匹配判别联合情况及其参数 |
| [] | [] | 匹配空列表 |
| 模式案例 | 示例 | 描述 |
| --- | --- | --- |
| [ patt; ... ] | [ elem ] | 匹配带有元素的列表 |
| id :: patt | hd :: tail | |
| hd1 :: hd2 :: [ last ] | 将列表解构为头部和尾部 | |
| [ ] | [ ] | 匹配空数组 |
| [ patt; ... ] | [ ell; _; el3 ] | 匹配带有元素的数组 |
| { id=patt; } | { FirstName=fn; LastName=ln } | 通过匹配字段来匹配记录 |
| patt | patt | [ elem ] | OR 模式 |
| patt & patt | | AND 模式 |

模式匹配是函数式编程中的一项基础技术，并且在 F# 代码中无处不在。所有的绑定都使用模式匹配来绑定左侧的右侧。考虑以下内容：

```fsharp
let (a, b, c) = 1, "my string", 2
let (x, y, _) = Compute3()[2]
```

```
-1
| when i>0 ->
1
```

尽管你可以像这个示例一样使用条件模式子，而且 F# 编译器在没有匹配所有可能的值时会向你发出警告。但这迫使你记住，对于你正在匹配的特定特征，不同“类型”数字之间的区别何。同样的问题也适用于普通的对象值，它们对于普通的模式匹配是“密封”（sealed）的，而且当你再次诉诸各种发布并使用这些值的成员来驱动模式匹配时，情况也是如此。

我们需要的是一种机制，将给定类型的值转换为一组“形状”（shapes），然后你可以对这些形状进行模式匹配。幸运的是，F# 通过其所谓的“活动模式”（active pattern）功能提供了这种机制。活动模式（也称为活动模式识别器）允许你为任何值定义一组命名的分区，称为“活动模式结果”，你可以像匹配它们是是判别 union（discriminated union）中的简单情况一样进行匹配。

活动模式可以像普通的判别 union构造函数一样携带值，允许你为每个模式结果标记任意复杂程度的值。此外，你的活动模式定义可以是全备的（total）或部分的（partial）。

你应该关注有种基本类型的活动模式，每种类型都有其独特的优势和用法模式。它们总结在表 25-17 中。
