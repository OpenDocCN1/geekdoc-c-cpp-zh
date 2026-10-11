
```csharp
// 计算到原点 (0,0) 的长度
public double LengthToOriginal()
{
    return this.GetDistance(this.OriginalPoint());
}

// 默认构造函数
public Point2D()
    : this(0,0)
{}

// 带参数 x 和 y 的构造函数
public Point2D(double x, double y)
{
    this.X = x;
    this.Y = y;
    count++; // 创建新实例时增加计数器
}

// 将 (x,y) 转换为 Point2D 的静态方法
public static Point2D FromX(double x, double y)
{
    return new Point2D(x, y);
}

// 计算到给定点的距离
public virtual double GetDistance(Point2D point)
{
    var xDif = this.X - point.X;
    var yDif = this.Y - point.Y;
    var distance = Math.Sqrt(xDif * xDif + yDif * yDif);
    return distance;
}

// 重写 ToString 函数
public override string ToString()
{
    return String.Format("Point2D({0}, {1})", this.X, this.Y);
}
```

### 使用类

在定义类时，C# 总是需要 `class` 关键字。在 F# 中，该关键字是可选的。列表 2-2 展示了 F# 中的类定义。

### 列表 2-2 类的类定义

```fsharp
// 不带默认访问修饰符的类定义
// 定义一个公共的 Point2D 类
type Point2D() = class

end
```

```fsharp
// 带有显式访问修饰符的类定义
// 定义一个内部的 Point2D 类
type internal Point2D() = class

end

// 不使用 class 关键字定义类
type MyClass() =
// 类字段、方法和属性，例如下面的字段
let myField = 9
```

> 注意：如果类包含任何成员或操作，则必须使用 `class` 关键字；否则，`class` 关键字是可选的。

你可能在想 `public` 关键字在哪里。与 C# 类默认为内部不同，F# 类默认是公共的。忽略 `public` 关键字可以减少输入量。F# 还支持使用模块来组织代码。表 2-1 列出了 F# 支持的所有访问修饰符。

### 表 2-1 访问修饰符定义

| 访问修饰符 | 说明 |
|---|---|
| `public` | 公共访问表示该类型、值和函数在任何地方都是可的。 |
| `private` | 私有访问修饰符是权限最低的访问。私有成员可以在声明它们的类或结构体体内被访问。类字段默认是私有的。 |
| `internal` | 如果只有一个程序集，则内部修饰符与 `public` 相同。内部类型无法从另一个程序集访问。当从同一个程序集访问时它是公共的，从不同程序集访问时则是不可的。 |

> 注意：F# 不支持 `protected` 关键字。当类型定义在支持保护级可见性的语言中时，F# 会尊重保护可见性。F# 的意图是在类中使用比 C# 较少的保护级别成员，相反地，它使用接口、对象表达式和高阶函数。

在列表 1-69 中，我们介绍了互递归函数的定义。你可以使用相同的方法来定义互递归类型。在列表 2-3 中，我们定义了一个互递归类型。

**列表 2-3** 不使用 `class` 关键字的互递归类型定义

```fsharp
type A() =
let b = B()
and B() =
let a = A()
```

与 C# 不同，F# 不支持部分类（`partial classes`），因此你必须将所有类代码放在单个文件中。F# 提供了类型扩展功能，我将在本章节的晚些部分介绍，以提供此类功能。

## 添加字段

我们需要在空的类定义中放入一些内容，逻辑上的起点是添加一个字段。F# 定义类的方式与在模块中定义值没有太大区别。列表 2-4 展示了如何在 *Point2D* 类中定义一个名为 `x` 的字段。一旦类变为空，我们就可以忽略 `class...end` 关键字。`x` 的初始值设置为 *0.0*，其类型被推断为 F# 的 `float` 类型。

**列表 2-4** 在类 *Point2D* 中定义字段 x

```fsharp
// 定义一个 Point2D 类
type Point2D() =
// 定义字段 x
let mutable x = 0.0
```

> **注意** 当在类中使用时，`let` 关键字仅能定义私有字段或函数。

定义显式字段的另一种方法是使用 `val` 关键字。列表 2-5 使用 `val` 关键字定义了显式字段 `x`。定义显式字段时，必须在字段定义中显式提供类型信息。显式字段定义可以带有 *public* 等访问修饰符。名为 `y` 的字段是一个公共字段。

### 列表 2-5 在类中定义显式字段

```fsharp
// 定义一个 Point2D 类
type Point2D()
  // 使用显式字段定义字段 x
  [DefaultValue] val mutable x : float

  // 定义具有公共访问性的字段 y
  [DefaultValue] val mutable y : float
```

> 注意：如果类具有主构造函数，则 `DefaultValue` 属性是强制性的。我将在稍后的“使用构造函数”部分解释这一点。

没有定义公共静态字段的方法。

`DefaultValue` 属性指定了字段 `x` 和 `y`。如果类具有主构造函数，则 `DefaultValue` 属性是强制性的。我将在稍后的“使用构造函数”部分解释这一点。

```
// define an X property
member.X with get() = x
and set(v) = x <- v

// 使用自动实现的属性定义 Y 属性
member val Y = 0.0 with get, set
```

> 注意：自动实现的属性不支持具有不同访问级别的访问器或设置器。因此，在使用自动实现的属性时，你无法定义私有的设置器函数。

索引属性（indexed property）本质上只是一个带有某些输入参数的属性。列表 2-9 显示了索引属性的示例。它定义了一个 `Screen` 类型，并用于通过索引来获取点。`Item` 属性是一个特殊属性，可以通过两种方式使用：`screen.[0]` 或 `Item(0)`。

## 列表 2-9 带有点列表的索引属性

```
// 定义一个带有点列表的 Screen
type Screen() = System.Collections.Generic.List<Point2D>()

// 属性 item 属性
member this.Item with get(x) = points.[x]
and set x v = points.[x] <- v
```

> 注意：设置器函数不接受 `(x, v)` 元组。它有两个参数，`x` 和 `v`。

C# 提供了对象初始化器来设置属性值。F# 具有类似的功能，用于初始化属性值。列表 2-10 提供了一个示例。在这个示例中，`p` 被初始化，`x` 和 `y` 被设置为 1。

## 列表 2-10 创建对象时设置属性值

```fsharp
type Point2D() =
    member val X = 0. with get, set
    member val Y = 0. with get, set

let p = Point2D(X = 1., Y = 1.)
```

## 定义方法

*方法*（method）是与类型关联的函数。可以通过成员方法或成员函数调用。如果你定义一个属性，将出现任何问题。在列表 2-11 中，我们定义了 `GetDistance` 方法。`GetDistance` 方法需要编译器知道输入参数是 `Point2D` 类型。在这种情况下，类型推断不起作用。列表 2-11 的 C# 版本被标记为虚拟的（virtual）。我将在后面的章节中讨论如何定义虚拟方法。

### 列表 2-11 定义成员函数

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
```

> 注意：双星号运算符 (`**`) 用于计算给定数的平方，`sqrt` 函数等同于 `Math.Sqrt`。随 Visual Studio 2010，C# 引入了可选参数和命名参数功能。这两种特性在 F# 中也可用。列表 2-12 显示了带有可选参数的 C# 版本。F# 不允许在参数后使用默认值；相反使用 `defaultArg` 函数。`defaultArg` 函数将可选参数作为第一个参数，并将默认值作为备用值。

### 列表 2-12 使用可选参数

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

可选参数暴露给 C# 项目，C# 项目需要引用 `Microsoft.Fsharp.Core.dll` 来创建 F# `option` 类型。见列表 2-13。

### 列表 2-13 引用带有可选参数的 F# 方法

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

如果引用 `FSharp.Core.dll` 不是首选方法，可以使用 `System.Runtime.InteropServices.DefaultParameterAttribute` 来暴露可选参数。列表 2-14 显示了一个示例。

## 列表 2-14 在不引用 FSharp.Core.dll 的情况下暴露 F# 可选参数

C# 代码的执行结果：
(2, "null value")
(0, "null value")
(3, "three")

> 注意：代码段 `[<Optional;DefaultParameterValue(0)>]` 包含两个属性。一个是 `OptionalAttribute`，另一个是 `DefaultParameterValue`。

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

### 列表 2-17 使用参数化构造函数作为主构造函数

```sharp
// 定义一个带有参数化主构造函数的 Point2D 类
type Point2D(xValue:double, yValue:double) =
    // 定义字段 x
    let mutable x = xValue
    // 定义 X 属性
    member this.X with get() = x
    and set(v) = x <- v
    // 使用自动实现属性定义 Y 属性
    val Y = yValue with get, set
    // 定义一个获取与当前点距离的函数
    member this.GetDistance(point:Point2D) =
        let xDif = this.X - point.X
        let yDif = this.Y - point.Y
        let distance = sqrt(xDif**2 + yDif**2)
        distance
    // 定义一个静态方法，从 (x,y) 元组返回 Point2D
    static FromXY(x, y) =
        Point2D(x,y)
```

> 注意：成员函数无法在构造函数代码中被调用。

在某些情况下，你需要不同的方法来初始化对象。C# 允许多个构造函数。列表 2-18 显示了如何在 F# 中定义一个额外的构造函数。

### 列表 2-18 额外的构造函数

```sharp
// 定义一个带有参数化主构造函数的 Point2D 类
type Point2D(xValue:double, yValue:double) =
    // 定义字段 x
    let mutable x = xValue
    // 额外的构造函数
    new() = Point2D(0.,0.)
    // 定义 X 属性
    member this.X with get() = x
```
