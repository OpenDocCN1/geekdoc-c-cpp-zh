

我们可以使用 C# 中可用的语法以多种方式形成乘积，以下是乘积或由两个对象形成的 arity-2（arity 是项目的数量），但可以有任意大小的乘积

```
(int A, int B) product = (A: 10, B: 20); //tuples are products.
```

```
public class Product
{
    public int A { get; set; }
    public int B { get; set; }
}
//objects are products.
```

```
var product = new List<int> { 10, 20 }; //a list can be seen as a product.
```

所有这些都是同构的，包含完全相同的信息，我们可以构造函数将一个转换为另一个。

这就是为什么我们可以例如用元组或对象替换方法上的参数列表。以下所有都是等价的：

```
public static void GetDiscount(int A, int B) { }
public static void GetDiscount((int A, int B) product) { }
public static void GetDiscount(Product product) { }
```

这种转换通常称为引入参数对象重构移动。它基于这样一个事实：两者 (,,,) 和元组 ((,,)) 都是乘积。为了将某物视为乘积，最重要的定律是我们必须能够编写两个函数，它们将接受一个乘积并给出我们组件部分。这些函数称为投影。

![](img/d73681d801b4b826e0b2a293897bbba4_76_0.png)

例如，对于乘积的数组定义 [, ]，投影将是：

```
var product = new List<int> { 10, 20 };
Func<List<int>, int> first = p => p[0];
Func<List<int>, int> second = p => p[1];
```

对于乘积的元组 (int A, int B) 定义，投影将是：

```
(int A, int B) product = (A: 10, B: 20);
```

```
Func<(int A, int B), int> first = p => p.A;
Func<(int A, int B), int> second = p => p.B;
```

## 3.2 可选的一个

如果我们定义了 + 和 • 也许，我们可以定义一个 1 项，它将与我们通常的代数规则 a•1 = a 一致，对于 C# 数组，如果我们假设 • 是 Concat 操作，那么 1 应该是 [] 以便保持 a.Concat([]) = a 。项 1 被称为范畴的终对象。

**终对象**：终对象是范畴中从任何对象到它只有一个且唯一一个态射的对象。

![](img/d73681d801b4b826e0b2a293897bbba4_77_0.png)

在列表的范畴中，终对象可以是空列表 [ ]，因为我们可以从任何其他列表得到一个函数到空列表，如果我们丢弃所有元素。然而，我们不能在没有任何特设特定说明的情况下对任何其他列表有一个单一的函数。这不是一个很有趣的想法，但它展示了代数在不同领域之间的一致性。例如对于列表的代数定义，我们有

x = 1 + a • x

我们可以将左侧的 x 用定义替换并得到：

x = 1 + a• ( 1 + a • x ) =1+a+a • a • x

如果我们继续这样做，我们得到：

x= 1 + a + a•a + a•a•a•x...

这说明一个列表可以是空的 1 = [] 或只有一个元素 [a] 或两个元素 [a, a] 或三个元素 [a ,a, a]，等等，这与列表的定义非常一致。此外，我们可以尝试这样求解：

x•(1- a) = 1 => x=1/(1- a)

然而，由于我们没有除法的定义，我们可以在 1/(1-x) 上使用泰勒展开，这展开为几何级数 1 + a + a²+ a³+a⁴+...

代数的一致性令人惊叹。

## 3.2.1 带乘积类型的 Lambda 演算 可选

简单类型 lambda 演算 λ→ 的下一个有用扩展是添加乘积 _×_ λ→,×

### 类型

λ→ 中唯一的只是基类型集合 B 和通过以下简单 BNF 形式语法产生的所有其他内容：

τ ::= τ→τ | τ×τ | T where T ∈ B

(int × int) → int

![](img/d73681d801b4b826e0b2a293897bbba4_78_0.png)

(int→ bool) → (int × char)

![](img/d73681d801b4b826e0b2a293897bbba4_78_1.png)

C# 中的 (int × int) → int 是委托：

```
Func<(int, int), int> f = ((int, int) a) => default(int);
```

或者在 lambda 记法中现在我们可以有变量为乘积类型的 lambdas

λx:(int× int).B: (int× int)→int

而第二个 (int→ bool) → (int × char) 将是：

```
Func<Func<int, bool>, (int a, char b)> g = (Func<int, bool> a) =>
    (a: default(int), b: default(char);
```

此外，我们必须将 Func<(int,int), int> 和 Func<int, int, int> 视为等价，因为我们可以找到两个路径将一个转换为另一个：

```
Func<A, B, C> Path1(Func<(A, B), C> f) => (A x, B y) => f((x, y));
```

```
Func<(A, B), C> Path2(Func<A, B, C> f) => ((A, B) p) => f(p.Item1, p.Item2);
```

![](img/d73681d801b4b826e0b2a293897bbba4_79_0.png)

出于这个原因，我们必须说这两种语法在 C# 类型系统中是等价的：

```
Func<(A, B), C> ≈ Func<A, B, C>
```

在 lambda 记法中，这两者是通过允许多参数 lambdas λ(x,y).B 以及单变量 lambdas 表示的，其中变量是乘积类型 λx:(A × B)：

```
Func<(A, B), C> λx:(A×B).B: (A × B)→C
```

```
Func<A, B, C> λ(x:A, y:B).B: (A × B)→C
```

### 引入消除规则

对于乘积有一个单一的引入规则：

![](img/d73681d801b4b826e0b2a293897bbba4_79_1.png)

这只是一个构造函数，它接受一个 A 和一个 B 并返回一个 A× B

```
Func<A, B, (A, B)> Intro = (A x, B y) => (x, y);
```

消除规则是两个投影：

![](img/d73681d801b4b826e0b2a293897bbba4_79_2.png)

![](img/d73681d801b4b826e0b2a293897bbba4_79_3.png)

```
Func<(A, B), A> Pr1 = ((A, B) p) => p.Item1;
```

```
Func<(A, B), B> Pr2 = ((A, B) p) => p.Item2;
```

### 计算规则

### β-归约

乘积的 β-归约意味着如果我们有一个以规范形式存在的乘积并且我们投影第一个，我们应该得到第一个元素，同样对于第二个投影：

```
π1( (x, y) : A×B ) ≡ x:A ×β1
```

```
π2( (x, y) : A×B ) ≡ y:B ×β2
```

这说明来自 Gentzen 的，**消除是引入的后逆**规则：

π₁( (x, y): A×B ) ≡ x:A  ×β₁

如果我们有一对项并首先使用构造函数（即引入）得到一个 ( , ) 然后立即使用投影 π₁( · )（即消除，即析构）那么这些应该相互抵消并得到回原始元素，对于适当的消除。对于 C# 元组，这意味着我们可以提供如下构造：

```
A Beta1<A, B>(A x, B y) => (x, y).Item1;
```

```
B Beta2<A, B>(A x, B y) => (x, y).Item2;
```

并且理想情况下在其他一些设置中我们希望能够表达：

(x, y).Item1 ≡ x  for-all x

### η-归约

```
var t = (1, 2);
```

```
var y = (t.Item1, t.Item2);
```

```
(A, B) Eta<A, B>((A, B) p) => (p.Item1, p.Item2);
```

A ∧ B / A ∧E₁   A ∧ B / B ∧E₂
---------------------- I∧
      A ∧ B

### 递归子

> 而不是每次我们想要定义一个函数时都调用这个函数定义原理，一个替代方法是只在通用情况下调用一次，然后在所有其他情况下简单地应用 resulting 函数。也就是说，我们可以定义一个类型为的函数：

Homotopy Type Theory: Univalent Foundations of Mathematics

Recₐₓᵦ: (A→B→C) → A×B→C

这说明如果你给我一个函数 (A→B→C) 它接受一个 A 然后一个 B 并产生一个 C 那么如果你给我一个乘积类型 AxB 的东西我可以给你一个 C。这是反柯里化的定义。并且在 C# 中很容易实现：

```
Funcn<(A, B), C> Rec(Func<A, Func<B, C>> f) => ((A, B) p) => f(p.Item1)(p.Item2);
```

有了这个递归子，我们可以定义所有其他内容。例如，我们可以使用 Rec AxB 定义投影

```
Funcn<(A, B), A> Pr1<A, B> (Func<A, Func<B, A>> f) => Rec<A, B, A>(x => y => x);
```

```
Funcn<(A, B), B> Pr2<A, B> (Func<A, Func<B, B>> f) => Rec<A, B, B>(x => y => y);
```

我们将在实践中经常使用这个乘积递归子，以模式匹配包含组合的对象形式。

### Curry-Howard 对应

乘积等价于逻辑 AND 或两个命题 A 和 B 的合取 A ∧ B。为了得出命题 A ∧ B 成立，我们必须知道 A 和 B 都为真。或者等价地，如果我们可以证明 A 并证明 B 那么我们可以证明 A ∧ B。这个规则通常在数理逻辑中命名为引入，因为它从先前的命题中引入合取 ∧。

> A / A∧B ^I

同样，为了创建一个类型 A 和类型 B 的乘积，我们必须在调用乘积的构造函数 var product = (x, y) => _ 时具有两种类型的实例。这种等价源于 Curry-Howard 同构，这可能是计算机程序和数学证明之间最深刻的联系。如果我们有一个 A ∧ B 那么我们可以推导出 A 或 B 中的任何一个。这称为合取消除。从 A ∧ B 以下成立

> A∧B / A ^E1

> A∧B / B ^E2

或命题 A ∧ B → A , A ∧ B → B 是重言式。

乘积“构造成本高”因为我们需要所有组件，但使用容易，因为通过投影（第一个、第二个...）取出任何组件都是有效的。

