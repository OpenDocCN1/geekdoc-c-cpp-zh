

## 列表 6-47 记录与标识符模式

```fsharp
对判别联合类型使用标识符模式
type Shape =
| Circle of double
| Triangle of double * double * double
| Rectangle of double * double

let getArea shape =
    match shape with
    | Circle(r) -> r * r * System.Math.PI
    | Triangle(a, b, c) ->
        let s = (a + b + c) / 2.
        sqrt ((s - a) * (s - b) * (s - c) )
    | Rectangle(a, b) -> a * b
```

使用记录模式
type Point2D = { x : float; y : float }

let isOnAxis p =
    match p with
    | Point2D { x = 0; y = _ } -> true
    | _ -> false
```

F# 使用系统类型来防止错误发生并提高可读性。列表 6-48 使用 Currency DU（判别联合）类型将小数转换为 USD 或 CAD 类型。该示例通过添加运算符扩展了 Currency DU 类型。

## 列表 6-48 在货币计算中使用 DU 和模式匹配

```fsharp
type Currency =
| USD of decimal
| CAD of decimal

// 使用 + 和 - 运算符扩展 DU 类型
with
    static member (+) (x:Currency, y:Currency) =
        match x, y with
        | USD(a), USD(b) -> USD(a+b)
        | CAD(a), CAD(b) -> CAD(a+b)
        | _ -> failWith "cannot add different unit value"

    static member (-) (x:Currency, y:Currency) =
        match x, y with
        | USD(a), USD(b) -> USD(a - b)
        | CAD(a), CAD(b) -> CAD(a - b)
        | _ -> failWith "cannot add different unit value"
```

```fsharp
// 执行货币加法和减法操作
try
    printf result = "%A" (USD(1m) + USD(11m))
    printf result = "%A" (CAD(1m) - CAD(11m))

    // 这一行会产生异常
    printf result = "%A" (USD(100m) - CAD(10m))
with
    | as e -> printf("%A") e

执行结果
result = USD 12M
result = CAD -10M
System.Exception: cannot add different unit value
```

注意：与度量衡方法不同，这种方法增加了运行时开销。

记录的模式匹配需要确保在执行匹配时对记录进行解构。列表 6-49 中的 `match` 语句即使在类型不同的情况下，也会与列出的任何记录进行匹配。匹配记录的正确方法在列表 6-50 所示。

**列表 6-49** 记录匹配示例 I

```fsharp
type MyRecord = { X : int list; Y : string }
type MyRecord2 = { XX : int; YY : string; Z : int }

let rr = { X = [100; 200]; Y = "aa" }
let r0 = { X = [100; 200; 3]; Y = "aa" }
let r1 = { X = 11; YY = "bb"; Z = 9 }

match r1 with
    | rr -> "a"
    | _ -> "b"
```

注意：最后一行将生成警告“此规则将永远不会被匹配”。

## 列表 6-50 记录匹配示例 II

## 使用与（或/）模式和模式分组

与（或/）模式通过 AND/OR 关系组合了两个模式。列表 6-51 使用 AND 模式测试点是否在轴上。匹配 列表中的所有模式都通过 OR 逻辑逻辑连接在一起；因此，OR 模式示例可以使用模式分组进行重写，如列表 6-52 所示。

## 列表 6-51 用于测试点的与（或/）模式

```fsharp
// 用于测试点的 And 模式
let testPoint2 point =
    match point with
    | x & 0, y -> "original point"
    | x & 0, _ -> "on x axis"
    | _ & y & 0 -> "on y axis"
    | _ -> "other"
```

```fsharp
// Or 模式
let testPoint3 point =
    match point with
    | x, y & (0, 0) -> "original point"
    | x, y & (0 | _, 0) -> "on x axis"
    | _ -> "other"
```

## 列表 6-52 模式分组

```fsharp
let testPoint4 point =
    match point with
    | (x, y) & (0, 0) -> "original point"
    | (x, y) & (0, _) | (x, y) & (_, 0) -> "on x axis"
    | _ -> "other"
```

## 使用变量模式和 when 守卫

到目前为止，你所看到的模式还没有处理解构数据项之间的关系。如果你想知道解构的数据是否符合标准，可以使用 `when` 守卫。列表 6-53 了 (x,y) 点是否在直线 f(x) = x 上。

**列表 6-53** 点相对于直线 f(x) = x

```fsharp
let testPoint tuple =
    match tuple with
    | x, y when x = y -> "on the line"
    | x, y when x > y -> "below the line"
    | _ -> "up the line"
```

注意：F# 不会根据 `when` 的结果来判断匹配表达式是否复杂。因此，如果你将列表 6-53 中的最后一个模式更改为 `when x < y`，编译器仍然会认为匹配表达式是不完整的并生成警告。另一个选项是使用活动模式（active patterns），它将在下一节中介绍。

## 使用 ? 模式和 as 模式

当输入参数被解构为不同的部分时，可能需要一个名称。`as` 模式就是为此目的而引入的。列表 6-54 显示了如何检查类型。F# 不像 C# 那样使用 `as` 运算符，而是使用 `?` 来检查类型。

**列表 6-54** 类型模式示例

```fsharp
let testType x =
    match x with
    | float as f -> printf "float value %f" f
    | int as i -> printf "int value %d" i
```

## Choice 模式

## 列表 6-55 使用 Choice 模式

*(注：由于原文文本似乎存在一些关于 Choice 的重复描述，此处已根据要求完成翻译)*

