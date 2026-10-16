
+   2. 一组称为**态射**或箭头的元素。每个态射 **f** 都有一个源对象 **a** 和一个目标对象 **b**。

## **范畴** C

![](img/d73681d801b4b826e0b2a293897bbba4_47_0.png)

在我们的类型范畴中，例如，从 `int` 到 `bool` 的任何箭头都表示一个函数 `int → bool`。一些例子可能是：

```
bool isEven(int a)=> a%2==0;
```

或者这个：

```
bool isLessThan10(int a)=> a<10
```

## 类型的**范畴**

![](img/d73681d801b4b826e0b2a293897bbba4_47_1.png)

范畴论的基本焦点**是对象之间的关系**，而不是对象本身，这与主要关注对象集合的集合论形成对比。函数式程序员很快接受了范畴论的这一独特视角。

## 2.2 幺半群

> “另一种说法是，范畴论的基本概念是幺半群”
> ——《给数学工作者的范畴论》

幺半群是一种深刻而又易于理解、无处不在的思想。幺半群属于代数范畴。在函数式编程中，有几种特别重要的方式来组织不同的结构。代数就是其中之一。Fantasy Land 规范中包含了一些最重要的代数。

维基百科说，幺半群是一种具有单个结合二元运算和单位元的代数结构。任何具有这两个要素的结构都是幺半群。

假设 S 是一个结构，⊗ 是某种二元运算 S ⊗ S → S，那么 S 与 ⊗ 构成一个幺半群，如果它满足以下两条公理：

-   1. 结合律：对于 S 中的所有 a、b 和 c，等式 (x ⊗ y) ⊗ z = x ⊗ (y ⊗ z) 成立。

![](img/d73681d801b4b826e0b2a293897bbba4_48_0.png)

-   2. 单位元：在 S 中存在一个元素 e，使得对于 S 中的每个元素 a，等式 e ⊗ a = a ⊗ e = a 成立。

![](img/d73681d801b4b826e0b2a293897bbba4_48_1.png)

让我们以整数为例，我们可以将加法视为两个整数之间的二元运算。加法是结合的。这意味着加法的顺序并不重要。

```
(x+(y+z)) = ((x+y) +z)
```

而 0 是加法的单位元，因为：

```
x + 0 = x
```

基于这些原因，配对 (0, +) 在整数上构成了一个幺半群。然而，我们可以在整数上构造其他不同的幺半群。例如，乘法 * 也可以被视为一个幺半群，其对应的单位元是 1。这样，(1, *) 就是整数上的另一个

幺半群。C# 中的字符串有一个默认的幺半群，它由连接操作和空字符串 ("", Concat) 构成。

我们将在代码中使用幺半群，通过定义简单的对象字面量来实现，其中包含两个函数：一个返回单位元，称为 Empty；一个表示二元运算，称为 Concat。

> [在本书中，我们将遵循 Fantasy Land 规范中关于幺半群的命名约定，尤其是因为 C# 已经对字符串和数组使用了 Concat。]

```
public interface IMonoid<T>
{
    T Empty { get; }
    T Concat(T x, T y);
}
```

这个接口的类型是：IMonoid<T>: (Empty: T, Concat: (T × T)→ T)，另一种写法是 Concat 的柯里化版本 (T → T)→ T，这是一种常见的类型表示方法。

我们将这样使用幺半群：

```
var sum = new Sum();
var total = sum.Concat(1, sum.Concat(3, 4));
```

这个定义允许我们直接将其用于列表的 Aggregate 函数：

```
total = new[] { 1, 3, 4, 5 }.Aggregate(sum.Empty, sum.Concat);
```

我们也可以将幺半群定义为一个元组：

```
(int empty, Func<int, int, int> concat) sum = (0, (x, y) => x + y);
```

另外，如果我们希望具有封闭性 [意味着 Concat 和 Empty 的返回类型与初始对象是同一类型]，我们可以为每个幺半群定义一个类。

```
public interface IMonoidAcc<T>
{
    T Identity { get; set; }
    IMonoidAcc<T> Concat(IMonoidAcc<T> m);
}
```

```
public class Sum : IMonoidAcc<int>
{
    public Sum(int value) => Identity = value;
    public int Identity { get; set; }
    public IMonoidAcc<int> Concat(IMonoidAcc<int> m) =>
        new Sum(m.Identity + Identity);
}
```

```
var total = new Sum(0).Concat(new Sum(1)).Concat(new Sum(2)).Concat(new Sum(3));
```

![](img/d73681d801b4b826e0b2a293897bbba4_49_0.png)

这种写法的优点在于它允许流畅的链式调用 var total = new Sum(0) .concat(new Sum(1)) .concat(new Sum(2))，因为 empty 和 concat 都返回相同类型的结果。这也更符合数学定义：如果 S 是一个结构（在编程语言中，这对应一个类型），那么 S × S → S 意味着该运算返回同一种结构。

在实践中，只要我们清楚自己正在处理幺半群，就不必在意严格的定义。

### 2.2.1 折叠幺半群

幺半群有一个非常理想的特性：如果我们持续应用这个二元运算 ⊗，我们总能将计算归约为同一类型的单个元素：

(M⊗...(M⊗(M⊗M)))→M

这被称为折叠。

(((v:M ⊗ u:M) ⊗ w:M ) ⊗ ... ⊗ z:M) =a:M

![](img/d73681d801b4b826e0b2a293897bbba4_50_0.png)

假设我们有一个整数序列 2,4,5,6，想要将它们相加，这是一个入门级问题：

```
var list = new[] { 1, 2, 3, 4 };
var accumulation = 0;
foreach (var current in list)
    accumulation = accumulation + current;
(0,+) monoid
```

我在这里强调的只是一个初始元素 0 和加法，加法是两个整数之间返回一个整数的运算。

如果我们想将它们相乘呢？

```
var accumulation = 1;
foreach (var current in list)
    accumulation = accumulation * current;
(1,*) monoid
```

+ 和 * 都可以抽象为 lambda。对于 + 的情况：

```
Func<int, int, int> add = (int x, int y) => x + y;
```

在第二种情况下，我们从初始元素 1 开始，使用乘法作为两个整数之间的运算：

```
Func<int, int, int> add = (int x, int y) => x * y
```

因为两者具有相同的签名，我们可以对它们进行抽象，创建一个可以复用的高阶函数：

```
public T Fold<T>(List<T> list, T accumulation, Func<T, T, T> concat)
{
    foreach (var current in list)
        accumulation = concat(accumulation, current);
    return accumulation;
}
```

现在我们可以在这两种情况下使用这个函数：

```
var sum = Fold<int>(new[] { 1, 2, 3, 4 }, 0, (x, y) => x + y);
var product = Fold<int>(new[] { 1, 2, 3, 4 }, 1, (x, y) => x * y);
```

此外，我们还可以使用 (T accumulation, Func<T, T, T> concat) 参数（即幺半群）的其他组合来折叠数组。例如：

```
var max = Fold(new[] { 1, 2, 3, 4 }, int.MinValue, (x, y) => x > y ? x : y);
```

显然，这个 Fold 函数非常重要，所有编程语言都为数组数据结构实现了它。在 .NET 中，它被称为 Aggregate：

```
var sum = new List<int> { 1, 2, 3, 4 }
    .Aggregate(0, (accumulation, current)=> accumulation + y);

var product = new List<int> { 1, 2, 3, 4 }
    .Aggregate(1, (accumulation, current) => accumulation * y);
```

如果你在任意 List 上通过元数据定义（按 F12）查看类型签名，你会看到以下内容：

```
TAccumulate Aggregate<TSource, TAccumulate>(TAccumulate seed, Func<TAccumulate, TSource, TAccumulate> func);
```

[附注：Aggregate 通常就是我们所说的 FoldMap，它与 Fold 相同，但还包含一个 Map（即 Select）操作，这允许我们让结果 TAccumulate 的类型不同于 List 的类型 TSource。]

## 2.3 折叠幺半群展示

在本节中，我们将展示一些使用 Aggregate 函数进行幺半群折叠的示例。在所有示例中，我们将会：

-   1. 确定某个类型 S，并找到某种将两个 S 组合成单个 S 的方法。
-   2. 然后，给定一个 S 的 List，我们可以使用 Aggregate 来折叠它们。

# 折叠委托 Func<,>

我们将在本章后面详细研究这个案例，因为它是许多经典面向对象模式的基础。这里我们将从两个 Func<int, int> 委托开始：

```
Func<int, int> A = (x) => x + 1;
Func<int, int> B = (x) => x + 2;
```

有了这两个委托，我们可以找到一个将它们组合成单个 Func<int, int> 的函数：

```
Func<int, int> compose = (x) => A(x) + B(x);
```

有了这个函数，我们现在可以将整个 Func<int, int> 列表折叠成一个。

```
List<Func<int, int>> list = new List<Func<int, int>>() { A, B };
```

```
Func<int, int> accumulation = (x) => x;
foreach (var current in list)
{
    accumulation = (x) => accumulation(x) + current(x);
}
```

这个 for 循环可以使用 Aggregate 方法来简化：

```
var folding = list.Aggregate(
    (int x) => x,
    (Func<int, int> accumulation, Func<int, int> current) =>
        (x) => accumulation(x) + current(x)
);
```

```
Console.WriteLine(folding(2));
```

# 折叠回调

有了两个回调，我们可以找到一种将它们组合成单个回调的方法：

```
Action<int, Action<int>> square = (x, callback) => callback(x * x);
Action<int, Action<int>> cube = (x, callback) => callback(x * x * x);
```

```
Action<int, Action<int>> Compose(Action<int, Action<int>> c1,
```

