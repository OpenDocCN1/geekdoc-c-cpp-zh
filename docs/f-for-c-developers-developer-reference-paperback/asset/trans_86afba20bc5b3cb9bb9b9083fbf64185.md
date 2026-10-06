

```
// define an X property
member.X with get() = x
and set(v) = x <- v

// 使用自动实现的属性定义 Y 属性
member val Y = 0.0 with get, set
```

> 注意：自动实现的属性不支持具有不同访问级别的访问器或设置器。因此，在使用自动实现的属性时，你无法定义私有的设置器函数。

索引属性（indexed property）本质上只是一个带有某些输入参数的属性。列表 2-9 显示了索引属性的示例。它定义了一个 Screen 类型，并用于通过索引来获取点。Item 属性是一个特殊属性，可以通过两种方式使用：screen.[0] 或 Item(0)。

## 列表 2-9 带有点列表的索引属性

```
// 定义一个带有点列表的 Screen
type Screen() = System.Collections.Generic.List<Point2D>()

// 属性 item 属性
member this.Item with get(x) = points.[x]
and set x v = points.[x] <- v
```

> 注意：设置器函数不接受 (x, v) 元组。它有两个参数，x 和 v。

C# 提供了对象初始化器来设置属性值。F# 具有类似的功能，用于初始化属性值。列表 2-10 提供了一个示例。在这个示例中，p 被初始化，x 和 y 被设置为 1。

## 列表 2-10 创建对象时设置属性值

```fsharp
type Point2D() =
    member val X = 0. with get, set
    member val Y = 0. with get, set

let p = Point2D(X = 1., Y = 1.)
```

## 定义方法

*方法*（method）是与类型关联的函数。可以通过成员方法或成员函数调用。如果你定义一个属性，将出现任何问题。在列表 2-11 中，我们定义了 GetDistance 方法。GetDistance 方法需要编译器知道输入参数是 Point2D 类型。在这种情况下，类型推断不起作用。列表 2-11 的 C# 版本被标记为虚拟的（virtual）。我将在后面的章节中讨论如何定义虚拟方法。

## 列表 2-11 定义成员函数

```
// 定义一个 Point2D 类
type Point2D() =
    // 定义字段 x
    let mutable x = 0.0

    // 定义 X 属性
    member this.X with get() = x
        and set(v) = x <- v

    // 使用自动实现的属性定义 Y 属性
    member val Y = 0.0 with get, set

    // 定义一个获取当前点距离的函数
    member this.GetDistance(point:Point2D) =
        let xDif = this.X - point.X
        let yDif = this.Y - point.Y
        sqrt (xDif**2 + yDif**2)

> 注意：双星号运算符 (**) 用于计算给定数的平方，sqrt 函数等同于 Math.Sqrt。随 Visual Studio 2010，C# 引入了可选参数和命名参数功能。这两种特性在 F# 中也可用。列表 2-12 显示了带有可选参数的 C# 版本。F# 不允许在参数后使用默认值；相反使用 defaultArg 函数。defaultArg 函数将可选参数作为第一个参数，并将默认值作为备用值。

## 列表 2-12 使用可选参数

```csharp
// 带有可选参数的 C# 方法
// 计算到给定点的距离
public double GetDistance(double x = 0, double y = 0)
{
    var xDif = this.X;
    var yDif = this.Y;
    var distance = Math.Sqrt(xDif * xDif + yDif * yDif);
    return distance;
}
```

```fsharp
// 带有可选参数的 F# 方法
// 获取当前点的距离
member this.GetDistance(xValue, yValue) =
    // 取 (xValue, yvalue) 元组并决定是否使用默认值
    let x, y = defaultArg xValue, defaultArg yValue
    let xDif = this.X
    let yDif = this.Y
    sqrt (xDif**2 + yDif**2)
```

可选参数暴露给 C# 项目，C# 项目需要引用 Microsoft.Fsharp.Core.dll 来创建 F# option 类型。见列表 2-13。

## 列表 2-13 引用带有可选参数的 F# 方法

```fsharp
// 定义带有可选参数的 F# 代码
namespace MyClass

type MyClass() =
    member this.PrintValue(value:int) =
        match value with
        | Some(n) -> printfn "value is %A" n
        | None -> printfn "sorry, no value"
```

```csharp
// 调用 F# 方法的 C# 代码
static void Main(string[] args)
{
    var myClass = new MyClass.MyClass();

    myClass.PrintValue(new Microsoft.Fsharp.Core.FsharpOption<int>.None);
    myClass.PrintValue(new Microsoft.Fsharp.Core.FsharpOption<int>(1));
}
```

C# 代码的执行结果：
sorry, no value
value is 1

如果引用 FSharp.Core.dll 不是首选方法，可以使用 System.Runtime.InteropServices.DefaultParameterAttribute 来暴露可选参数。列表 2-14 显示了一个示例。

## 列表 2-14 在不引用 FSharp.Core.dll 的情况下暴露 F# 可选参数

C# 代码的执行结果：
(2, "null value")
(0, "null value")
(3, "three")

> 注意：代码段 [<Optional;DefaultParameterValue(0)>] 包含两个属性。一个是 OptionalAttribute，另一个是 DefaultParameterValue。

从 F# 侧调用带有可选参数的 C# 方法很容易。列表 2-15 显示了如何调用带有可选参数的 C# 方法。

**列表 2-15 从 F# 调用带有可选参数的 C# 方法

```csharp
// 定义带有可选参数的 C# 代码
public class CSharpClass
{
    public void MyMethod(int a = 11)
    {
        Console.WriteLine("{0}", a);
    }
}
```

```fsharp
// 调用带有可选参数的 C# 方法的 F# 代码
let c = ConsoleApplication1.CSharpClass()
c.MyMethod()
c.MyMethod(100)
c.MyMethod(a=199)

// F# 代码的执行结果：
a = 11
a = 100
a = 199
```

## 定义静态方法

我们已经将*字段、属性和成员*方法从 C# 转换到 F#。现在我们可以转换静态方法 *FromXY*。在 C# 中，需要 *static* 关键字来定义静态方法。实现此目标的一种方法是使用元组，另一种是定义两个独立的参数。如果你还记得“定义元组”、“C# 和 F# 数据结构”中提到的设计原则，那么元组方法是更好的选择，因为它要求同时传递 *x* 和 *y*。F# 代码如列表 2-16所示。

```fsharp
// 定义一个 Point2D 类
type Point2D() =
    // 定义字段 x
    let mutable x = 0.0

    // 定义 X 属性
    member this.X with get() = x
        and set(v) = x <- v

    // 使用自动实现的属性定义 Y 属性
    member val Y = 0.0 with get, set

    // 定义一个获取当前点距离的函数
    member this.Distance(point:Point2D) =
        let xDif = this.X - point.X
        let yDif = this.Y - point.Y
        let distance = sqrt (xDif**2 + yDif**2)
        distance

    // 定义一个静态方法从 (x,y) 元组返回 a2D
    static member FromXY(x:double, y:double) =
        let point = Point2D()
        point.X <- x
        point.Y <- y
        point
```

