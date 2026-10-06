

# 使用 option 的 F# 代码

```sharp
// return a string option to indicate the return value can be an uninitialized value
let str = read_string()
match str with
  Some data -> printf("good, we got value and we can process...")
  None -> printf("what happened, call IT right now!")
```

> > 注意 read_string() 的简单实现是 Console.ReadLine()。当控制台 Ctrl+Z 时，Console.ReadLine() 方法返回 NULL。

对于 F# 程序员来说，情况有所不同。用户可能会提供无效输入，因此代码必须表示这种无效输入。option 类型被用于显式地指示无效状态。当 F# 程序员调用 `read_string` 函数时，返回的 option 类型会提醒（甚至强制）F# 程序员处理这种无效情况。F# 的设计帮助开发者避免了许多 bug。一个典型的例子是 F# 如何引入 option 而不是使用 NULL 值来表示多种类型。如果你数一下你上个月收到的许多 NULL 异常，那么理解为什么 F# 程序员会在代码中报告 bug 就不难了。

让我们来看 C# 中的一个自定义类示例。如果你有一个 `Person` 类型对象，赋值值 NULL 的意义是什么？它要么意味着对象处于未赋值状态，要么意味着对象处于特殊状态（即它有一个无效值）。这种歧义性破坏了单一责任原则，即 SOLID 的第一原则。如果同一团队的两个开发者对 NULL 对对象的含义有不同看法，那么应用程序中可能会出现很多空引用缺陷。如果将其与 F# 的 option 方法相比较，`None` 用于表示没有值，而 `Some(...)` 用于表示任何有效值。这明确了定义。

当我们设计这种语言时，我们知道并不是所有人都会同意上述论点。这完全没，因为你可以使用 `AllowNullable` 特性来使类可为空。列表 6-13 显示了如何使用 `AllowNullLiteral` 特性的示例。

+ 列表 6-13 在类型上使用 AllowNullLiteral

```fsharp
<AllowNullable()]
type NullableType()
  member this.TestNullable(condition) =
    if condition then Nullable()
    else null
```

> 注意 如果类型被装饰了 AllowNullLiteral 特性，则该代码将无法编译。

在读完列表 6-13 后，你可能会疑惑为什么 F# 仍然允许空值。这是因为 F# 处于一个接受 NULL 作为输入值的对象和方法的世界中。如果 F# 不支持 NULL，那么许多 .NET 调用将是不可能的。此外，当变量需要绑定到函数时，需要 NULL。参见列表 6-14。

# 列表 6-14 检查函数初始化

```fsharp
type A() =
    [DefaultValue>]
    val mutable MyFunction : unit -> int
    member this.IsMyFunctionInitialized
    with get() = box this.Function = null
```

总结来说，NULL 的限制仅存在于 F#。如果你从 C# 项目引用 F# 项目，你可以将 NULL 传递给 F# 函数。如果一个 C# 函数在 F# 代码内部返回 NULL 值，这仍然是可以接受的。

在结束本节之前，我将列出一些你可以用于处理 NULL 和 options 的辅助函数和技巧。列表 6-15 提供了一种将 NULL 值转换为 option 并在其为 None 的情况下转换回 NULL 的方法。除了使用 `AllowNullLiteral` 之外，这段代码为 NULL 问题提供了一种替代方案。`Unchecked.default<T>` 操作符返回 T 的默认值，例如 int 的 0 以及任何引用类型的 NULL。

# 列表 6-15 在与 C# 交互时将 NULL 转换为 option 或反之

```fsharp
type A() =
    let mutable a:option<A> = None
    member this.Value
    with get() =
      match a with
      | Some n -> n
      | None -> Unchecked.default<A>
    and set v =
      if v = Unchecked.default<A> then a <- None
      else a <- Some v
```

# 使用单位（Units of Measure）

当我从寒冷的安大略省多伦多开车到佛罗里达州的 NASA 太空中心时，我惊讶地看到 LED 屏幕显示当前温度为 28 度。几分钟前我刚穿过尼亚加拉瀑布，简直不敢相信天气竟然如此！！美国人会笑，因为他们知道 LED 上的温度是用华氏度表示的。因为加拿大使用摄度，公制和英制单位之间的差异困扰了我。信不信，我从 NASA 听到的故事是 1999 年的火星轨道事故，其根本原因是使用了错误的单位。

如果一种编程语言支持单位（如 F 那样），这些问题是完全可以避免的。列表 6-16 显示了如何定义一个单位。值 `x` 被绑定到 3 cm，如果你尝试将 2.8 的浮点数赋给值 `c`，它将不起作用，因为 `c` 是一个 `float<...>` 类型，不能接受 `float`。同样，值 `c` 不能接受 `x³`，因为毫升是厘米的立方。

**列表 6-16** 定义和使用单位类型

```fsharp
// 定义 the units
//define centimeter
[<Measure>] type cm

// 定义毫升，它是 cm3
[<Measure>] type ml = cm3

let x = 3.<cm>
let c = x * x * x
// let c:float<ml> = x * x //无法编译，因为 ml 是厘米的立方
```

