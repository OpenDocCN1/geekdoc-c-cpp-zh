

如果 `inherit` 声明出现在主构造函数中，它被称为隐式类构造。列表 2-31 中的代码始终使用隐式构造函数并提供隐式构造函数（或重载）的良好实践。然而，列表 2-30 中的代码没有包含主构造函数，而是指定了所需的基类构造函数。我们此称为显式类构造。这是使用隐式构造函数的一种推荐方法。

列表 2-31 关键字基类的示例

```
type Particle()
  inherit Point2D()
  member val Mass = 0. with get, set
  override this this.ToString() =
    sprintf("Particle_%s with Mass=%f", (base.ToString()) this.Mass)
```

## 使用抽象类和密封类

类层次结构通过继承形成树形结构。有时树的根可以是抽象类。C# 使用 `abstract` 关键字来定义抽象类。与 C# 不同，F 在没有提供默认实现时需要使用 `AbstractClass` 特性来定义抽象类。请参列表 2-32 中的代码。

列表 2-32 定义抽象类

```
[AbstractClass]
type MyAbstractClass()
  member this.F() = 1

  // 定义一个抽象成员函数
abstract member FunctionNotImplemented : unit -> int
```

> 提示 如果你忘记如何编写成员方法的函数定义，你也可以使用 FSI。例如，如果你想定义一个以 `int` 参数为输入并以 `int` 输出的函数，可以在 FSI 中写 `f (int) = 1`，`val : int -> int` 就会显示该函数的定义。在 C# 中，如果方法是虚方法，则可以被重写。F 没有用于定义虚方法的 `virtual` 关键字。相反，F 使用 `abstract` 和 `default` 关键字来定义虚方法。在列表 2-33 中，`GetDistance` 方法被定义为虚方法，然后定义了该方法的默认实现。

```fsharp
// 定义一个带有主构造函数的 Point2D 类
type Point2D(xValue:double, yValue:double) =
  // 定义字段
  let mutable x = xValue

  // 定义一个名为 count 的静态字段
  static let mutable count = 0

  // 执行 do 绑定以增加计数
  do
    count <- count + 1

  // 额外的构造函数
  new() = Point2D(0.,0.)

  // 输出消息
  member this.Print() = printf "In class Point2D"

  // 定义一个 X 属性
  member this.X with get() = x
    and set(v) = x <- v

  // 使用自动实现属性定义 Y 属性
  member val Y = yValue with get, set

  // 定义一个虚函数来获取当前点的距离
  abstract GetDistance : point:Point2D -> double
  default GetDistance(point) =
    let xDif = point.X
    let yDif = point.Y
    let distance = sqrt (xDif*xDif + yDif)

  // 定义一个静态方法，从 (x,y) 元组返回 Point2D
  static member FromXY(x, y) = Point2D(x,y)

  override this.ToString() = sprintf "Point2D(%f, %f)" this.X this.Y
```

非虚方法不是一种良好的实践，尽管在某些情况下它是必要的方法。F# 不像 C# 那样支持 `new` 关键字，但它仍然允许用户这样做。如果你重写了一个非虚方法，将会产生警告。列表 2-34 显示了一个示例。

列表 2-34 重写非虚方法

```csharp
// 使用 new 关键字的 C# 代码
public class MyClass : List<int>
{
    public new void Add(int n)
    {
        base.Add(n);
        // <额外的操作>
    }
}
```

```fsharp
// 重写非虚方法的 F# 代码
type MyList() =
    inherit System.Collections.Generic.List<int>()

    // 添加元素
    member this.Add(n) = // 此处产生警告
        base.Add(n)
        // <额外的操作>
```

> 注意 你可以使用 `[#warn]` 来禁用警告。

我将稍微改变方向，引入一下特性（Attributes）。F# 中的特性使用方式与 C# 非常相似。列表 2-35 显示了如何用 `DebugDisplayAttribute` 装饰 `Point2D` 类。

列表 2-35 为类添加 DebugDisplay 特性

```fsharp
// 定义一个带有主构造函数的 Point2D 类
[System.Diagnostics.DebugDisplay("{X}, {Y}")]
type Point2D(xValue:double, yValue:double) =
  // 定义字段
  let mutable x = xValue

  // 定义一个名为 count 的静态字段
  static let mutable count = 0

  // 执行 do 绑定以增加计数
  do
    count <- count + 1

  // 额外的构造函数
  new() = Point2D(0.,0.)

  // 输出消息
  member this.Print() = printf "In class Point2D"

  // 定义一个 X 属性
  member this.X with get() = x
    and set(v) = x <- v

  // 使用自动实现属性定义 Y 属性
  member val Y = yValue with get, set
```

`AbstractClass` 特性用于定义抽象类，而 `Sealed` 特性用于定义密封类。请参列表 2-36。

列表 2-36 密封类定义

```fsharp
[<Sealed>]
type MySealedClass()
    member this.F() = 1
```

## 实例化

F# 使用 **new** 关键字创建对象。除非类实现了 *IDisposable* 接口，否则在创建新对象时 **new** 关键字是可选的。如果不使用 *new* 关键字，将会产生编译警告，指示 *new* 关键字且该类实现了 *IDisposable*。请参列表 2-37。

列表 2-37 创建实现 *IDisposable* 对象时使用 *new* 关键字

```csharp
// 使用 new 关键字创建实现 IDisposable 接口的对象
let myObj = System.Data.SqlClient.SqlConnection()

// 警告：建议使用 'using()' 创建支持 IDisposable 接口的对象
// 而不是 'new Type()'以表示资源可能由生成的值所有
let myObj2 = System.Data.SqlClient.SqlConnection()
```

> 注意 当类实现 *IDisposable* 接口时，在非模块上下文中，**use 可以替换 let**。请记住 C# 中的 *use* 与 F# 不同。

