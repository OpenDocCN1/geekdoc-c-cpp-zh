
```fsharp
let CADAmount : float<CND> = LanguagePrimitives.FloatWithMeasure 1000.

canadaAccount.Deposit(CADAmount)

printf "Canadian interest = %M" (canadaAccount.PayInterest())
```

对于一些 C# 开发者来说，类型（`type`）是他们每天都会遇到但很少关注的东西。每天都有大量的测试用例被检查程序的正确性。你是否考虑过，在运行程序之前，编译器实际上会在每个分支上检查你的代码？如果错误可以在编译时被捕捉，修复将容易得多。单位测量就是利用类型系统减少错误可能性的一个示例。在本节的后续部分，你将看到更多使用类型系统来减少错误概率的示例。

## 处理记录（Records）

如前所述，元组（`tuple`）是一组值。你可以将记录（`record`）视为元组的增强版本。记录是一组命名的值，它提供的功能比元组更多。列表 6-23 显示了如何定义和创建记录。如果记录定义中的标签（`label`）是唯一的，那么在创建记录实例时记录名称是可选的；否则，你必须指定记录类型名称。例如，`Point2D` 和 `Point` 都有 `x` 和 `y` 标签。因此，在创建 `Point2D` 或 `Point` 的记录实例时需要类型名称。

### 列表 6-23 定义并创建记录

```fsharp
// 定义记录

type Point2D = { x : float; y: float }

type Point = { x : float; y: float }

type Student = { Name: string; Age : decimal; }

type Person = { First : string
    Last : string }

// 创建记录
// 因为标签不是唯一的，所以记录名称是强制的

let point2DRecord = { Point2D.x = 1.; Point2D.y = 2. }

let pointRecord = { Point.x = 1.; Point.y = 2. }

// 因为标签是唯一的，所以记录名称是可选的

let studentRecord = { Name = "John"; Age = 18m; }

let personRecord = { First = "Chris"
    Last = "Root" }
```

![](img/63aaf94e22830ab98ce16c5946be8ef6_317_0.png)

注意：当你将每个标签放在新的一行时，分号（`;`）是可选的。同样，最后一个分号也是可选的。

记录中的字段默认是不可变变的。列表 6-24 显示了如何使用 `with` 关键字创建现有记录的副本。

### 列表 6-24 记录拷贝

```fsharp
type Person = { First : string
    Last : string }

let personRecord = { First = "Chris"
    Last = "Root" }

let personRecord2 = { personRecord with First = "Matt" }

// 执行结果
// type Person =
//     {First: string;
//     Last: string}
// val personRecord : Person = {First = "Chris"; Last = "Root"}
// val personRecord2 : Person = {First = "Matt"; Last = "Root"}
```

注意：为了避免编译错误，请确保 `First` 和 `Last` 对齐正确。强烈建议使用 F# IDE 来协助此操作。

如果记录字段装饰了 `mutable` 关键字，则可以是可变的。此外，记录可以定义成员函数或属性来扩展其功能。请参见列表 6-25。

### 列表 6-25 带有可变字段的记录

```fsharp
type Car =
  Make : string
  Model : string
  mutable Odometer : int
  member this.drive(mile) =
    this.Odometer <- this.Odometer + mile
  member this.CurrentMileage = this.Odometer

let myCar = { Make = "Plymouth"; Model = "Neon"; Odometer = 0 }

myCar.drive(20)

printf "current mileage = %d" myCar
```

注意：为了避免编译错误，请确保 `First` 和 `Last` 对齐正确。强烈建议使用 F# IDE 来协助此操作。

单位测量只能应用于 `float` 和有符号整数类型。如果你想在自定义类型上使用单位，则需要使用泛型类型定义。单位是一种特殊类型，因此可以无问题地在泛型类型定义中使用。列表 6-22 定义了一个银行账户类。通过应用不同的单位测量，你为不同货币生成了银行账户。

注意：在 `printf` 语句中，你必须使用 `%A` 作为类型标识符。变量 `result1` 在运行时是一个 `float`，但在编译时是 `float<'unit>` 类型。`%f` 与该单位不兼容，将无法通过编译。

F# 同样支持使用 `LanguagePrimitives.FloatWithMeasure` 和 `LanguagePrimitives.Float32WithMeasure` 创建带有单位的 `float` 值。此外，你可以通过将其转换为数字来移除单位。请参见列表 6-21。

# 列表 6-21 在数字与单位测量值之间进行双向转换

```fsharp
// 移除单位并返回 float
let removeUnit<'Measure> u = float x
let result = removeUnit 4.unit

// 给 float 赋予单位
let float4b : float<'unit> = LanguagePrimitives.FloatWithMeasure result
```

单位测量只能应用于 `float` 和有符号整数类型。如果你想在自定义类型上使用单位，则需要使用泛型类型定义。单位是一种特殊类型，因此可以无问题地在泛型类型定义中使用。列表 6-22 定义了一个银行账户类。通过应用不同的单位测量，你为不同货币生成了银行账户。

# 列表 6-22 使用单位测量的银行账户

```fsharp
// 账户状态枚举
type AccountState =
| Overdrawn
| Silver
| Gold

// 单位测量：美元和加元
[<Measure>] type USD
[<Measure>] type CND

// 银行账户类
type Account<'Measure> u() =
    let mutable balance = 0.0<'unit
    member this.State
    with get() =
        match balance with
            when balance <= 0.0<'unit -> Overdrawn
            when balance > 0.0<'unit && balance < 10000.0<'unit -> Silver
            -> Gold
```

```fsharp
member this.PayInterest() =
    let interest =
        match this.State with
        | Overdrawn -> 0.
        | Silver -> 0.01
        | Gold -> 0.02
    interest

member this.Deposit x = balance <- balance + x
member this.Withdraw x = balance <- balance - x
```

```fsharp
let measureSample() =
    // 创建美元账户
    let account = Account<USD>
    let USDAmount = LanguagePrimitives.FloatWithMeasure 10000.
    account.Deposit(USDAmount)
    printf "US interest = %M" (account.PayInterest())

    // 创建加元账户
    let canadaAccount = Account<CND>
    let CADAmount : float<CND> = LanguagePrimitives.FloatWithMeasure 1000.
    canadaAccount.Deposit(CADAmount)
    printf "Canadian interest = %M" (canadaAccount.PayInterest())
```
