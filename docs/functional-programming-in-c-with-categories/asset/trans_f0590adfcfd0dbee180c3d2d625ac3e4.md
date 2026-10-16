

```
public async Task<string> GetNameByIdAsync(int clientId)
    => await clients.GetByIdAsync(clientId)
        .Map(client => client.Name).Case_switch
{
    LeftCase<string, string>(var error) => error,
    RightCase<string, string>(var name) => name,
    _ => throw new NotImplementedException(),
};
}
```

Note :The use of .Case without the need to first await

Github: source

## 4.17 Functors from Algebraic Data Types

我们已经在第 3.4 节中看到了针对列表数据结构的代数定义实现的 map 函数。我在这里重述该实现：

```
public class Cons<T> : ListBase<T>
{
    ...
    public override ListBase<T1> Map<T1>(Func<T, T1> f) =>
        new Cons<T1>(f(Value), Rest.Map(f));
}
```

```
public class Empty<T> : ListBase<T>
{
    public override ListBase<T1> Map<T1>(Func<T, T1> f) => new Empty<T1>();
}
```

现在我们对函子有了更多了解，可以推导出二叉树的 map 实现。因此，让我们从线性到二次。

树也是一个递归数据结构。二叉树的定义是：

Tree (a)= leaf(a) + Node(Tree(a), Tree (a))

这说明 Tree(a) 可以是一个 Leaf (a) 或两个 Tree a 类型的 Node。

[Sidenote: 列表可以被视为一棵树，其所有节点的右侧始终是叶子：Tree a = Leaf a + Node (Leaf a) * (Tree a) ≅ List a = a + a * (List a) ]

```
public abstract class Tree<T>
{
    public abstract Tree<T1> Map<T1>(Func<T, T1> f);
}
```

```
public class Node<T> : Tree<T>
{
    public Tree<T> Left { get; set; }
    public T Value { get; set; }
    public Tree<T> Right { get; set; }

    public Node(Tree<T> left, Tree<T> right)
    {
        this.Left = left;
        this.Right = right;
    }
}
```

```
public class Leaf<T> : Tree<T>
{
    public T V { get; }
    public Leaf(T v) => V = v;
}
```

为了基于此代数数据类型创建一个函子，我们定义一个有效的 **map** 方法。我们将再次遵循 **结构归纳法** 来定义 **map**。

首先，因为它是一个 **余积**，我们必须在余积的两个子类型 Leaf 和 Node 中都定义 map 方法。

- 1. 我们从 Leaf 开始，它是结构归纳的基础情形。我们必须返回相同类型的东西。因此我们返回一个新的 Leaf，并将函数应用于该值
   
  `Tree<T1> Map<T1>(Func<T, T1> f) => new Leaf<T1>(f(V))`

**叶就是一个恒等函子。** 希望你能认出来。

- 2. Node 部分是两个树的乘积（Left, Right），两者都是我们想要定义 map 的相同类型。唯一的处理方式是假设两者都已经有了可按预期工作的 map 函数（这又是归纳假设），
  
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

## C# 8.0 Pattern Matching

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

## 4.18 Applicative Functors

Applicative 是一个相对容易理解的概念。它是一个包含函数（ a→ b ）而不仅仅是值的函子 F，我们必须提供一个有效的方法，该方法可以取另一个包含值 F(a) 的函子并给出一个 F(b)。我们称之为 apply（通常方法名为 Ap）：

Ap: F(a → b) → F(a) → F(b)

![](img/d73681d801b4b826e0b2a293897bbba4_160_0.png)

你可以将它与 map 签名 Map : (a → b) → F(a) → F(b) 进行比较，唯一的区别是初始的 F。

如果我们以恒等函子为例，可以按如下方式实现 apply：

## 4.19 Reader Applicative Functor optional

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

## Conventions: Bind and SelectMany

作为约定，我们将把我们的映射方法命名为 Bind，尽管在某些情况下如果我们需要 LINQ 支持，我们也可能会使用 SelectMany。Map 和 Select 在本书中可以互换使用。language-ext 库提供了 Bind 和 SelectMany 方法别名

