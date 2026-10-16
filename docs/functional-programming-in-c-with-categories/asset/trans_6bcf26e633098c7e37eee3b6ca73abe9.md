

```csharp
Func<double> ProductA = () => 100;
Func<double> ProductB = () => 200;
Func<Func<double>, Func<double>> Packaging =
    (product) => () => product() + 10;

Func<double> packagedProduct = Packaging(ProductA);
```

因此，从某种意义上说，任何形如 `(T a) => (R b) => {}` 的函数，都等价于这样一个对象：构造函数接收一个 `a: T`，并且只有一个接受 `b: R` 作为参数的方法。

仅使用函数：`(Func<double> product) => () => {...}`
面向对象：`class Packaging { constructor(IPriced product) {...} double getPrice() {...} }`

这里的思路是，让那些在返回类型为 `Product` 的被装饰函数之后出现的装饰组合函数也能采用同样的形式。

![](img/d73681d801b4b826e0b2a293897bbba4_61_0.png)

## 元组记法

表示该对象的另一种方式是使用元组。不幸的是，C# 不允许只有单个成员的元组。因此，为了演示，我们给 product 添加另一个返回名称的方法 `getName: () => name`。现在我们可以用一个充当构造器的函数来定义 product：

```csharp
Func<string, double, (Func<string> getName, Func<double> getPrice)> Product =
    (string name, double price) =>
        (getName: () => name, getPrice: () => price);
```

我们可以用这个来创建产品：

![](img/d73681d801b4b826e0b2a293897bbba4_61_1.png)

```csharp
(Func<string> getName, Func<double> getPrice) ProductA = Product("A", 100);
(Func<string> getName, Func<double> getPrice) ProductB = Product("B", 200);
```

现在我们可以如下定义装饰器函数：

```csharp
Func<(Func<string> getName, Func<double> getPrice),
    (Func<string> getName, Func<double> getPrice)>
    Packaging =
    product =>
    (
        getName: () => product.getName() + "Packaging",
        getPrice: () => product.getPrice() + 0.1
    );
```

然后我们可以这样使用它：

```csharp
(Func<string> getName, Func<double> getPrice) packagedProduct = Packaging(ProductA);
```

```csharp
(Func<string> getName, Func<double> getPrice) doublePackagedProduct = Packaging(Packaging(ProductA));
```

显然，这里“元组作为对象”的最小语法仅用于演示。在 C# 9.0 中，加入了不可变记录类型，以覆盖我们希望遵循更简约的函数式编码风格的情况。

## 2.8 谓词幺半群组合

最著名的逆变函数类型是谓词（Predicate），即任何类型为 `_ → bool`（返回布尔值）的函数。我们已经看到 .NET 提供了原生的 Predicate 委托：

```csharp
public delegate bool Predicate<in T>(T obj);
```

在实践中，我们通常使用委托 `Func<T, bool>` 来表示谓词。.NET 框架内部也大多使用 `Func<T, bool>` 作为谓词类型。例如，.NET 框架中 `List<T>.Where` 的定义具有以下签名：

```csharp
IEnumerable<TSource> Where<TSource>(this IEnumerable<TSource> source, Func<TSource, bool> predicate)
```

### 范畴论：逆变类型

这类类型被称为逆变类型，是因为它们将“变化的（类型）”放在“函数的负侧（即输入侧）”。输入参数是可变的 `(T x) → bool`。当我们这里说输入参数可变时，指的是输入参数的类型是泛型的（输入参数具有参数多态性），而返回类型则固定为 `bool`。

要理解为什么它是逆变的，可以尝试将一个函数 `T → R` 与一个谓词 `(R a) => bool` 组合，得到一个谓词 `(T a) => bool`。唯一可行的组合方式是将 `T → R` 预先复合到 `(R a) => bool` 之前，从而得到 `(T a) => bool`。

![](img/d73681d801b4b826e0b2a293897bbba4_63_0.png)

这在视觉上看起来像这样：

`T → R ∘ R → ● ⇔ T → ●`

其中 `●` 在我们的例子中就是 `bool`。

通过这种方式，对于谓词，我们可以定义一个 PreCompose（预复合）函数：

```csharp
Predicate<R> PreCompose<T, R>(Func<R, T> f, Predicate<T> g) => (R x) => g(f(x));
```

当你看到下面这个简单示例时，整个逆变预复合就变得一目了然了：我们对 Price 有一个 `Predicate<double>`，并希望使用一个用于 Price 的投影 GetPrice 来产生一个作用于 Product 的 `Predicate<Product>`：

```csharp
Predicate<double> IsHighPriced = (price) => price > 100;
```

```csharp
Func<Product, double> GetPrice = (product) => product.Price;
```

```csharp
Predicate<Product> IsHighPricedProduct = PreCompose(GetPrice, IsHighPriced);
```

这是组合像 Predicate 这样的逆变类型的一种方式。

另一种方式是幺半群组合。利用 bool 上的幺半群运算 `&&`、`||`、`~`，我们可以定义多种组合 `And`、`Or` 和 `Not`，从而能够从更简单的谓词构造出更大的谓词。

规范模式（Specification pattern）就是基于这一思想，其定义如下：

```csharp
Func<T, bool> And<T>(Func<T, bool> p1, Func<T, bool> p2) => (T x) => p1(x) && p2(x);
```

```csharp
Func<T, bool> Or<T>(Func<T, bool> p1, Func<T, bool> p2) => (T x) => p1(x) || p2(x);
```

```csharp
Func<T, bool> Not<T>(Func<T, bool> p1) => (T x) => !p1(x);
```

![](img/d73681d801b4b826e0b2a293897bbba4_64_0.png)

我们可以同时应用两个谓词，然后将它们的布尔结果粘合在一起，从而创建出新的谓词。

然后我们可以在产品上使用一些基本的谓词：

```csharp
Func<string, Func<Product, bool>> nameContains = pattern => product =>
    product.Name.Contains(pattern);
```

```csharp
Func<Product, bool> highPriced = product => product.Price > 1000;
```

接着我们可以使用 `And`、`Or` 和 `Not` 将它们组合成更复杂的谓词，例如：

```csharp
Func<Product, bool> highPricedAndContainsA = And(highPriced, nameContains("A"));
```

我们可以将这些谓词与数组的 filter 方法一起使用：

```csharp
var products = new List<Product>{
    new Product("widgetA", 100),
    new Product("widgetB", 1100),
    new Product("widgetA", 2000),
    new Product("widgetB", 300)
};
```

```csharp
var notHighPricedAndContainsA = Not(highPricedAndContainsA);
```

```csharp
var filteredProducts = products.Where(notHighPricedAndContainsA);
```

运行此示例：.NET Fiddle

或者尝试用以下谓词过滤该 List：

```csharp
var filter = Or(highPriced, nameContains("B"));
```

```csharp
var filter = Not(Or(highPriced, nameContains("B")));
```

我们还可以通过提供静态扩展来进一步简化语法，以实现流畅（fluent）的组合：

```csharp
public static partial class FunctionalExt
{
    public static Func<T, bool> And<T>(this Func<T, bool> @this, Func<T, bool> p) =>
        (T x) => @this(x) && p(x);

    public static Func<T, bool> Not<T>(this Func<T, bool> @this) =>
        (T x) => !@this(x);
}
```

现在我们可以这样写：

```csharp
Func<Product, bool> notHighPricedAndContainsA = highPriced.And(nameContains("A")).Not();
```

## 2.9 规范模式——函数式视角

我们可以将这些机制提取为一个流畅的构造过程，从而创建谓词表达式。这就是非常著名的规范模式。规范模式常常引起褒贬不一的反应，甚至被许多人视为反模式。尽管如此，它仍是 Eric Evans 所设想的领域驱动设计战术模式的一部分。

![](img/d73681d801b4b826e0b2a293897bbba4_65_0.png)

规范模式的基本思想，就是我们之前看到的在布尔幺半群上对谓词进行组合。其主要面向对象的增强之处，是添加了一个流畅的构建器，允许我们链式编写如下表达式：

```csharp
var spec1 = new Spec(nameContains("A")).And(highPriced);
```

而不是“函数式”的写法：

```csharp
And(highPriced, nameContains("A"))
```

其核心是 `CompositeSpecification`，所有其他表达式都继承自它：

```csharp
public interface ISpecification<T> {
    bool IsSatisfiedBy(T item);
}
```

// 为了给 And、Or、Not 添加流畅构建器语义

```csharp
public abstract class CompositeSpecification<T> : ISpecification<T>
{
    public CompositeSpecification<T> And(ISpecification<T> spec) =>
        new And<T>(this, spec);
    public CompositeSpecification<T> Or(ISpecification<T> spec) =>
        new Or<T>(this, spec);
    public CompositeSpecification<T> Not() =>
        new Not<T>(this);
    public abstract bool IsSatisfiedBy(T item);
}
```

这里我们将会有一个基类 `Spec<T>`：

```csharp
public class Spec<T> : CompositeSpecification<T>
{
    private Func<T, bool> expression;
    public Spec(Func<T, bool> expression) => this.expression = expression;
    public override bool IsSatisfiedBy(T item) => expression(item);
}
```

看一下 `And<T>`：

```csharp
public class And<T> : CompositeSpecification<T>
{
    private ISpecification<T> left;
    private ISpecification<T> right;
    public And(ISpecification<T> left, ISpecification<T> right)
    {
        this.left = left;
        this.right = right;
    }
    public override bool IsSatisfiedBy(T item) =>
        left.IsSatisfiedBy(item) && right.IsSatisfiedBy(item);
}
```

> CompositeSpecification 提供了一个流畅的接口。

运行此示例：.NET Fiddle

