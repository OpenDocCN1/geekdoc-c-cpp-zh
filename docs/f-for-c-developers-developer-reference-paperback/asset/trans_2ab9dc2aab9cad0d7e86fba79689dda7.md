

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

## 使用类

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
| public | 公共访问表示该类型、值和函数在任何地方都是可的。 |
| private | 私有访问修饰符是权限最低的访问。私有成员可以在声明它们的类或结构体体内被访问。类字段默认是私有的。 |
| internal | 如果只有一个程序集，则内部修饰符与 public 相同。内部类型无法从另一个程序集访问。当从同一个程序集访问时它是公共的，从不同程序集访问时则是不可的。 |

> 注意：F# 不支持 `protected` 关键字。当类型定义在支持保护级可见性的语言中时，F# 会尊重保护可见性。F# 的意图是在类中使用比 C# 较少的保护级别成员，相反地，它使用接口、对象表达式和高阶函数。

在列表 1-69 中，我们介绍了互递归函数的定义。你可以使用相同的方法来定义互递归类型。在列表 2-3 中，我们定义了一个互递归类型。

**列表 2-3** 不使用 `class` 关键字的互递归类型定义

```fsharp
type A() =
let b = B()
and B() =
let a = A()
```

与 C# 不同，F# 不支持部分类（partial classes），因此你必须将所有类代码放在单个文件中。F# 提供了类型扩展功能，我将在本章节的晚些部分介绍，以提供此类功能。

## 添加字段

我们需要在空的类定义中放入一些内容，逻辑上的起点是添加一个字段。F# 定义类的方式与在模块中定义值没有太大区别。列表 2-4 展示了如何在 *Point2D* 类中定义一个名为 `x` 的字段。一旦类变为空，我们就可以忽略 `class...end` 关键字。`x` 的初始值设置为 *0.0*，其类型被推断为 F# 的 float 类型。

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

（注：此处原文中大量重复段落已按要求剔除）

