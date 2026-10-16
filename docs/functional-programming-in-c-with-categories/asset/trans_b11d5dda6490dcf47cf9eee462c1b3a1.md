

```
public T Value { get; set; }
public Id(T value) => Value = value;

public T1 MatchWith<T1>(Func<T, T1> callback) => callback(Value);
public void MatchWith(Action<T> callback) => callback(Value);
}
```

![](img/d73681d801b4b826e0b2a293897bbba4_118_0.png)

```
new Id<int>(3).MatchWith(Console.WriteLine);
```

```
Console.WriteLine( new Id<int>(3).value)    // Instead of this
```

如果我们只想获取值，可以在内部传递恒等函数

```
var value =new Id<int>(3).MatchWith (x=>x);
```

这里我们将第一次以一种平凡的方式使用 C# 8.0 的模式匹配。
看一下：

```
string result = new Id<int>(5)
    switch
    {
        Id<int> { Value: var v } => v.ToString(),
    };
```

使用以下 switch 语法：

```
switch
{
    _ =>
};
```

我们可以窥探 Id<int>( ) 的内部

```
switch
{
    Id<int> { } => _
};
```

并匹配值（访问值，对 Id<int>( ) 在被拆解时看起来如何做出断言）

```
switch
{
    Id<int> { Value: var v } => _
};
```

在某些纯函数式语言中，这可能看起来像这样：

**Id(5) = Id(x)**

并且 x 立即被推断为 5，因为左侧必须作为模式匹配右侧。C# 的语法更冗长。

## 模式匹配于组合

让我们在 Id 内部再添加一个属性，并将其制作成一个 Pair“容器”（基本上是一个自定义的 Tuple）

```
public class Pair<T>
{
    public T Value1 { get; set; }
    public T Value2 { get; set; }
    public Pair(T value1, T value2) { Value1 = value1; Value2 = value2; }
    public Pair<T1> Map<T1>(Func<T,T1> f) =>new Pair<T1>(f(Value1),f(Value2));
}
```

我们可以将 MatchWith 定义为：

```
public T1 MatchWith<T1>(Func<T, T, T1> callback) =>
    callback(Value1, Value2);
```

这只是 Value1 和 Value2 的面向对象组合，或者在另一种解释中是 Value1 和 Value2 的乘积类型。我们现在可以使用 MatchWith 来提取值：

```
string pairResult1 = new Pair<int>(4, 5)
    .MatchWith((v1, v2) => (v1 + v2).ToString());
```

## 使用 C# 8.0 模式匹配

如果我们使用原生语法，这就变成了：

```
string pairResult = new Pair<int>(4,5)
    switch
    {
        Pair<int> { Value1: var v1, Value2:var v2} => (v1+v2).ToString(),
    };
```

运行此代码：.Net Fiddle

## 模式匹配于继承

假设现在你有一个简单的形状层次结构：

```
abstract class Shape { }
```

```
class Rectangle : Shape
{
    public int Width { get; set; }
    public int Height { get; set; }
}

class Circle : Shape
{
    public int Radius { get; set; }
}
```

现在如果我将一个 Shape 变量赋值。我可以分配矩形或圆形。这里我选择矩形：

```
Shape shape = new Rectangle { Width = 100, Height = 100, };
```

运行时如何得知我放入的是哪种形状？当然使用模式匹配。从继承的角度来看，通常我们使用像 case analysis 这样的词。

我们可以使用自 C# 7.0 以来的传统 switch 用法

```
string GetShapeDescription(Shape shape)
{
    switch (shape)
    {
        case Circle c:
            return $"found a circle with radius {c.Radius}";
        case Rectangle s:
            return $"Found {s.Height }x {s.Width} rectangle";
        default:
            throw new System.Exception(nameof(shape));
    }
};
```

很好，但与上一节的精神相同，我们可以定义一个 MatchWith，它接受一些暴露值的回调：

```
abstract class Shape
{
    public abstract T MatchWith<T>(Func<Rectangle, T> rectangleCase,
        Func<Circle, T> circleCase);
}
```

```
class Rectangle : Shape
{
    public int Width { get; set; }
    public int Height { get; set; }

    public override T MatchWith<T>(Func<Rectangle, T> rectangleCase,
```

```
Func<Circle, T> circleCase)
=> rectangleCase(this);
```

```
}

class Circle : Shape
{
    public int Radius { get; set; }
    public override T MatchWith<T>(Func<Rectangle, T> rectangleCase,
        Func<Circle, T> circleCase)
        => circleCase(this);
}
```

我们可以用它像这样使用：

```
Shape shape = new Rectangle { Width = 100, Height = 100, };
```

```
var description = shape.MatchWith<string>(
    rectangleCase: r => $"Found {r.Height}x {r.Width} rectangle",
    circleCase: c => $"found a circle with radius {c.Radius}"
);
```

## 使用 C# 8.0 模式匹配

正如你所想象的，我们可以在 C#8.0 中用以下方式编写，而无需创建像这样的自定义模式匹配定义：

```
string GetShapeDescription(Shape shape) =>
    shape switch
    {
        Rectangle { Height: var h,Width: var w } => $"Found {h }x {w} rectangle",
        Circle { Radius: var r } => $"found a circle with radius {r}",
    };
```

并像这样使用它：

```
Shape shape = new Rectangle{Width = 100, Height = 100,};
```

```
var description = GetShapeDescription(shape);
```

我们将在具有继承结构的许多 Functor 中看到模式匹配。

## 4.5 Id<T> Functor 即时创建

我们可以使用扩展方法允许从值 T 创建 Id<T> 并立即使用 Map 然后 Fold。

```
public static Id<T> ToId<T>(this T @this) => new Id<T>(@this);
```

并且这样写：

```
(5).ToId()
.Map(x => x + 1)
.MatchWith(Console.WriteLine);
```

这有用吗？也许有用，也许没用。但它标志着一种非常常见的函数式编程写法，使用链式调用和使用 .ToId() 之类的转换方法，以便在一种数据结构和另一种数据结构之间移动。

Id<T> 和 T 是同构的。它们包含完全相同的信息，因此我们可以使用 ToId<T> 和 Fold() 方法在两者之间来回转换，而不会丢失任何信息或需要任何额外信息（它们在某种意义上是逆运算）

![](img/d73681d801b4b826e0b2a293897bbba4_122_0.png)

在这本书的整个过程中，我们将看到许多同构。在 Functor 的情况下，这些同构被称为自然变换。我们将在后面的章节中更详细地看到它们。现在，我们将看到另外四个同构（Task、Func、Lazy、IO）与普通值 T，从而为处理它们提供统一的抽象。

### 4.5.1 其他同构

但首先让我们再创建一个与 T 相关的函子。值 T 本身可以看作是一个仅包含一个元素的 List：

```
public static List<T> ToList<T>(this T @this) => new List<T> { @this };
```

它的逆运算是 First()，因为例如 5.ToList().First()==5;

![](img/d73681d801b4b826e0b2a293897bbba4_122_1.png)

T 也是一个只有一个元素的 ValueTuple

```
ValueTuple<int> t1 = ValueTuple.Create(5);
```

其逆运算是微软为元组提供的通用 Fold 实现：

```
static S Fold<A, S>(this System.ValueTuple<A> self, S state, System.Func<S, A, S> fold);
```

这是标准的 Fold 签名，它等价于 List.Aggregate，我们可以用它来获取值，如下所示：

```
var value = t1.Fold(0, (a, e) => a + e);
```

![](img/d73681d801b4b826e0b2a293897bbba4_123_0.png)

最后，显然 ValueTuple<T> 与 List<T> 同构，因此我们可以创建一些扩展方法在两者之间转换

```
static List<T> ToList<T>(this ValueTuple<T, T> @this) => new List<T> {
    @this.Item1,
    @this.Item2
};
```

ValueTuple 是一个 Functor，因为它等价于 List()，但为了好玩我们可以直接创建 ValueTuple .Map 扩展方法：

```
static ValueTuple<T1, T1> Map<T, T1>(this ValueTuple<T,T> @this, Func<T, T1> f) => (f(@this.Item1), f(@this.Item2));
```

## SideNote:

一个非常明显的观察是，如果我们正确实现了 ValueTuple<T, T>.ToList<T>() 和 ValueTuple<T1, T1>.Map<T, T1>(f)，那么以下表达式的结果应该相等：

```
(3, 4).ToList().Select(x => x + 4);
(3, 4).Map(x => x + 4).ToList();
```

这两个表达式代表了以下图表中的不同路径：

![](img/d73681d801b4b826e0b2a293897bbba4_123_1.png)

