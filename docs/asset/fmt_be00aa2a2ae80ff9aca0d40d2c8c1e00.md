
`Tree<T1> Map<T1>(Func<T, T1> f) => new Node<T1>(Left.Map(f), Right.Map(f))`

```
this.Left = left;
Value = value;
this.Right = right;
}
```

Tree (a)= leaf(a) + Node(Tree(a), a, Tree (a))

你能将之前的 map 定义扩展以提升节点的值吗？

你能为这个树版本写出 map 定义的符号方程吗？

### C# 8.0 Pattern Matching

我们可以使用 switch 和扩展方法重写 map，这样就跳过了自定义的 MatchWith 方法

```
public static Tree<T1> Map<T, T1>(this Tree<T> @this, Func<T, T1> f) =>
    @this switch
    {
        Leaf<T> { Value: var v } => new Leaf<T1>(f(v)),
        Node<T> { Left: var l, Right: var r } =>
            new Node<T1>(l.Map(f), r.Map(f)),
    };
```

Run This: .Net Fiddle

### 4.18 Applicative Functors

Applicative 是一个相对容易理解的概念。它是一个包含函数（ a→ b ）而不仅仅是值的函子 F，我们必须提供一个有效的方法，该方法可以取另一个包含值 F(a) 的函子并给出一个 F(b)。我们称之为 apply（通常方法名为 Ap）：

Ap: F(a → b) → F(a) → F(b)

![](img/d73681d801b4b826e0b2a293897bbba4_160_0.png)

你可以将它与 map 签名 Map : (a → b) → F(a) → F(b) 进行比较，唯一的区别是初始的 F。

如果我们以恒等函子为例，可以按如下方式实现 apply：

### 4.19 Reader Applicative Functor optional

Reader applicative 是一个存储函数作为表达式 expr 的 reader。实现有点复杂。试着想象你想要组合一个包含函数和一个仅包含值的 reader。这是我的实现：

```
public static class FunctionalExtensions
{
    public static Reader<Env, T1> App<Env, T, T1>
        (this Reader<Env, Func<T, T1>> @this, Reader<Env, T> fa) =>
    new Reader<Env, T1>(env => { return @this.Map(f => fa.Map(f).Run(env)).Run(env); });
}
```

```
var r = new Reader<(int, int), Func<int, int>>((g => (r) => g.Item1 + r))
    .App(new Reader<(int, int), int>(g => 1))
    .Run((1, 2));
```

如果我们取 applicative 操作

Ap: f(a→b)→f(a)→f(b) （这是 ⟨⊗...⟩ 的名称）

对于 reader 具体地，通过将 f 替换为 ((→) env) [即 (env →_)] 我们得到

⟨⊗⟩: ((→)env) (a→b) → ((→)env) a → ((→)env) b

经过一些化简我们得到形式

(env → (a→b)) → (env → a) → (env → b)

例如，如果我们有一个二元柯里化函数如 x=>y=>y+x，我们可以这样做

⟨add ⊗ 1 ⊗ 2⟩ → ⟨1+2⟩ 我们将得到一个加法的 reader

```
var t = new Reader<object, Func<int, Func<int, int>>>((g => x1 => y1 => x1 + y1))
    .App(new Reader<object, int>(g => 1)).App(new Reader<object, int>(g => 1))
    .Run(default);
```

Category Theory Monoidal Functor

设 (C,⊗_C,1_C) 和 (D,⊗_D,1_D) 为两个幺半范畴。它们之间的 lax 幺半函子是

- 1. 一个函子 F:C→D。

- 2. 一个态射 ε:1_D→F(1_C)

3. 对所有 x,y∈ C 的自然变换 μ_{x,y}:F(x)⊗_D F(y)→F(x⊗_C y)

ε:1_D→F(1_C) 表示 applicative 的纯操作，允许我们进入一个 applicative

F(x)⊗_D F(y)→F(x⊗_C y) 是 applicative 操作 ap。 这个定义有趣的地方在于它将一个范畴的“乘法” ⊗_D 与另一个范畴的“乘法” ⊗_C 连接起来。

在我们上面的例子中，等价性是整数的乘法 ⊗_Int : (+) 现在与 reader 的 ⊗_Reader、applicative 操作 ap ⟨ ⟩ 相同：

(+) → 是同一个 ⟨ ⟩

```
Reader(g=>x=>y=>y+x).ap(Reader(g => 1)).ap(Reader(g => 2)).run({});
```

两个完全不同的域，但在不同抽象层面上 ap 等价于 +。酷吧。

另外正如我们在 traversable 部分会看到的，数组的“乘法” ⊗_Array concat (:) 将被提升为现在与 reader 的 ⊗_Reader、applicative 操作 ap ⟨ ⟩ 相同

(:) → ⟨ ⟩

```
Reader(g=>x=>y=>[y].concat(x)).ap(...).ap(Reader(...)) ;
```

（希望你能认出 μ_{x,y}:F(x)⊗_D F(y)→F(x⊗_C y) 是一个幺半同态）

```
public Id<T1> Bind<T1>(Func<T, Id<T1>> f) => f(Value);
```

这里的新东西是 bind 方法。Id<T1> Bind<T1>(Func<T, Id<T1>> f) => f(Value)

```
Id(5).Bind(x=>Id(x+1)) == Id(6)
```

这个 bind 方法的类型为 Bind:(T→ M <T1>) →M<T1>，它接受一个函数 T→M <T1>，当提供包含的值 v 时返回一个新的单子 M<T1>，类型为 T1。

```
var result = new Id<int>(2)
    .Bind(x => new Id<int>(2)
        .Bind(y => new Id<int>(x + y)));
```

让我们把一个单子放在另一个单子中并用恒等 x=>x 进行 Bind 以得到初始的 Monad。

```
var IdInId = new Id<int>(5).Map(x => new Id<int>(x + 1));
var justId = IdInId.Bind(x => x);
```

在恒等单子中 bind 与 map 的区别在于 map 将提升的值传递给单子构造器 Id(f(v)) 而 bind 不会：f(v)。在其他单子中 map 将与 bind 有显著不同。

同样的推理适用于所有函子，这里有一些其他例子，使用 Map 导致了 Functor in a Functor 的相同情况：

```
New IO(()=>5).Map(x=> new IO(()=> x+1)) === new IO(()=>new IO(()=> 6))
```

```
var a = new[] { 4 }.Select(x => new[] { x + 1 });
var b = new[] { new[] { 4 } };
```

```
new Some<int>(4).Map(x=> new Some<int>(x+1)) === new Some (new Some (5))
```

因此通常在大多数 Functor 中定义一个 Bind，从而将它们升级为单子。

### Conventions: Bind and SelectMany

作为约定，我们将把我们的映射方法命名为 Bind，尽管在某些情况下如果我们需要 LINQ 支持，我们也可能会使用 SelectMany。Map 和 Select 在本书中可以互换使用。language-ext 库提供了 Bind 和 SelectMany 方法别名

## 5.1 范畴论中的 Monad 可选

> "A monad is just a monoid in the category of endofunctors"

> - A Brief, Incomplete, and Mostly Wrong History of Programming Languages

这个定义在函数式社区中已成为一个内部笑话。因为它让一个从编程角度看极易掌握的概念变得神秘。然而，在范畴论中由于涉及的抽象，monad 的定义理所当然地难以把握。我们已经看到了这个定义的全部组成部分。

monad 的等价定义是 **monad** 是一个 [endofunctor]( ) **F**（一个 [functor]( ) 将 [category]( ) 映射到自身），连同两个 [natural transformations]( ) 需要满足某些 [coherence conditions]( )（即定律）。

Monads 有两个操作叫做 return 和 join（这些是 **monoid** 操作）：

+   1. η: v → F(v) //Return（这是 monoid 的 empty）

+   2. μ: F(F(v)) → F(v) //Join（这是 monoid 的 concat）

**1)** 在这个第一个操作 v → F(v) 中，我们可以从一个对象 v 开始得到一个容器 F(v)。这是我们获得 monads 的方式。这只是用编程术语来说 **Monad constructor** 的花哨说法：

![](img/d73681d801b4b826e0b2a293897bbba4_166_0.png)

**2)** 第二个 F(F(v)) → F(v) 的意思是我们可以将两个容器合并/展平为一个。

![](img/d73681d801b4b826e0b2a293897bbba4_166_1.png)

你可能会觉得这很直接，并且你已经可以看到与 Id 和 array monads 的联系。我们在这里隐藏的概念是这些是自然变换。所以，让我们尝试以视觉方式看看这意味着什么。首先，我们将看看 Endofunctor 是什么意思。这可能需要一些数学想象力。

### Category Theory

### Endofunctor

从一个范畴到自身的函子称为 endofunctor。给定任意范畴 C，我们可以创建一个新的范畴 End(C) 称为 C 的 endofunctor 范畴。End(C) 的对象是 endofunctors F:C → C，而态射是此类 endofunctors 之间的 **natural transformation**。

以视觉形式这看起来如下。首先，我们有一个在同一范畴 **C** 之间的函子。由于本节更抽象，我暂时不会给出编程示例。让我们先说我们有这个范畴 C 它有一些对象和箭头（我们这里省略箭头）。对象只是那三个 ●、●、●

![](img/d73681d801b4b826e0b2a293897bbba4_167_0.png)

函子 F 转换绿色 ●→● 紫色 ●→● 和红色 ●→●

但由于对象是相同的，我们可以在同一张图中描绘它。

![](img/d73681d801b4b826e0b2a293897bbba4_167_1.png)

现在我们可以将这个 F 作为 Endofunctors 范畴中的一个点放置，其中对象是 C 中的函子

![](img/d73681d801b4b826e0b2a293897bbba4_168_0.png)

现在我们可以添加第二个 endofunctor。[箭头不应该相同，但我对第二个函子使用了相同对象之间的箭头以使图表在视觉上不混乱。]

![](img/d73681d801b4b826e0b2a293897bbba4_168_1.png)

第二个 Endofunctor

最后，两个 Endofunctors F,G 之间的自然变换 α 用黄色箭头表示

![](img/d73681d801b4b826e0b2a293897bbba4_168_2.png)

两个 endofunctors 之间的箭头

在这个 endofunctor 范畴中的一个 monoid 称为 C 上的 monad。

对于第一个操作 η: 1_F → F 从函子 F 的恒等 Id_F 描绘为 Id_F: ●→● 围绕绿色对象 ● 的浅绿色箭头

![](img/d73681d801b4b826e0b2a293897bbba4_169_0.png)

从 Id_F 到 F 的自然变换看起来像下面的黄色箭头：

![](img/d73681d801b4b826e0b2a293897bbba4_169_1.png)

现在对于第二个自然变换 μ: F ∘ F → F 它是从 F 与另一个 F 的复合而来。我们可以直观地看到这意味着什么，如果我们可以将两个箭头 ●→● 和 ●→● 替换为复合 ●→●→● 这被视为 F ∘ F 下面的红色箭头： ●→● 现在应该有一个从这个箭头到另一个 F 箭头的自然变换。这是操作 F ∘ F→ F

![](img/d73681d801b4b826e0b2a293897bbba4_169_2.png)

## 5.2 List Monad

如果我们有一个整数列表并尝试得到平方、立方和四次方的列表，我们可能会尝试使用 map：

```
var a = new[] { 2,3 }.Select(x => new[] { x * x, x * x * x , x * x * x *x});
```

这会创建一个列表中嵌套列表 var list = [[4,8,16], [9,27,91]]

如果有一种方法可以只得到这些子列表元素的并集就好了。嗯，这正是列表作为 monad 通过 SelectMany 使用的目的。

```
var b = new[] { 2,3 }.SelectMany(x => new[] { x * x, x * x * x , x * x * x *x});
```

让我们逐一重新审视 monad 的操作，专门针对列表。

+   1. η :c → T(c) 表示通过元素 new[] { _ } 构造数组。如果我们再次应用列表构造函数，我们会得到一个列表中的列表 [ [ ] ]

+   2. μ:T(T(c))→ T(c) 是 join 操作，它逆转了添加的一层包含并给我们 T(c) 再次 [ ]

+   new[] { new[] { _ } }.SelectMany(x=>x) = new[] { _ }

## 5.3 Identity Monad

Identity Monad 是 monad 的最简单形式。

```
public class Id<T>
{
    public T Value { get; set; }
    public Id(T value) => Value = value;
    public Id<T1> Map<T1>(Func<T, T1> f) => new Id<T1>(f(Value));
    public Id<T1> Bind<T1>(Func<T, Id<T1>> f) => f(Value);
}
```

它没做什么。它没有任何计算价值。Identity Monad 的新东西是 bind 方法，如我们已经看到的：

```
Id<T1> Bind<T1>(Func<T, Id<T1>> f) => f(Value)
```

```
var result = new Id<int>(2)
    .Bind(x => new Id<int>(2)
        .Bind(y => new Id<int>(x + y)));
```

#### 5.3.1 Identity Monad 的 Optional Monad 定律

一个 monad 有 3 条直接的定律，它们是：

+   1. 左恒等，应用 unit 函数到一个值然后将 resulting monad 绑定到函数 f 与直接对同一值调用 f 相同。

+   2. 右恒等，将 unit 函数绑定到 monad 不会改变 monad

+   3. 结合律，如果我们有一串 monadic 函数应用，它们的嵌套方式无关紧要：m.bind(f).bind(g) == m.bind(x => f(x).bind(g));

```
Func<int, Id<int>> f = x => new Id<int>(x + 2);
var m1 = new Id<int>(5).Bind(f);
var m2 = f(5);
```

```
var value = 5;
var m1 = new Id<int>(value).Bind(x => new Id<int>(x));
var m2 = new Id<int>(value);
```

```
Func<int, Id<int>> f = x => new Id<int>(x + 2);
Func<int, Id<int>> g = x => new Id<int>(x * x);
var value = 5;

var m1 = new Id<int>(value).Bind(f).Bind(g);
var m2 = new Id<int>(value).Bind(x => f(x).Bind(g));
```

![](img/d73681d801b4b826e0b2a293897bbba4_171_0.png)
