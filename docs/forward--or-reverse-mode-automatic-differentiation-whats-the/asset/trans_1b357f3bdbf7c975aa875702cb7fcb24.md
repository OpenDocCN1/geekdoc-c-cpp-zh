

![](img/e423791fd87c536ca132e7d760db042c_5_0.png)

图 2. 在示例上运行前向模式自动微分，X = 5 时。

![](img/e423791fd87c536ca132e7d760db042c_5_1.png)

图 3. 半环 D 上 D-模组 E 的定律，其中 E 是交换幺半群。我们重载了相应半环的幺半群运算 ⊕，以强调其加法解释。

```
fmap (eval Var) ∘ symbolic
= ( - reflection property (Property 2 ) - )
fmap id ∘ symbolic
= ( - functor law and id as unit of composition - )
symbolic
```

总之，symbolic 是 forwardAD 的一个特例：

```
symbolic = forwardAD Var
```

这为本文余下部分奠定了基础：我们使用代数技术来推导微分算法的结构，并通过暴露更抽象的结构，同一个抽象算法（第 3 节）涵盖了各种具体的 AD 变体。

## 3. 抽象自动微分

本文的核心主张是，我们可以将之前的两个微分函数（符号微分和经典前向模式 AD）以及后来将出现的几种更多变体，都表示为同一个单行泛型程序。本节确定了三种基本代数结构来实现这一点：d-模组、广义双数 d × e，和克罗内克三角函数。它还展示了如何实例化这些结构，以恢复一种前向模式 AD 版本，该版本一次性计算所有偏导数的梯度向量，而不是一次只针对单个变量。

### 3.1. 半环上的模组

我们的第一个抽象概括了表达式 e 的梯度 ∇e 的概念。

```
∇e = [ ∂e/∂x1 ]
     [ ...    ]
     [ ∂e/∂xn ]
```

与向量空间（在域上）或模组（在环上）类似，我们考虑半环 d 上的半模组 [15]，我们称之为 d-模组。

**定义 3**（半模组）。给定半环 D，D-模组 E 被定义为交换幺半群 E，加上标量乘法 (●) : D × E → E，它在 E 的加法结构上分配。这意味着 E 应该有一个交换、结合的二元运算 ⊕，其单位元为零。图 3 给出了 E 的幺半群定律以及 E 的幺半群结构与标量乘法之间交互作用的定律。

在 Haskell 中，我们在 Monoid 类型类之上，使用类型类 Module 来捕捉半模组的概念。

```
class Monoid e where
  zero :: e
  (⊕) :: e → e → e

class (Semiring d, Monoid e)
=> Module d e | e → d where
  (●) :: d → e → e
```

每个半环 d 都可以平凡地视为一个 d-模组，取 (●) = (⊗)。一个著名的非半环示例是向量空间 R³：它与向量加法和零向量 [ 0 0 0 ] 构成幺半群，并与通常的标量乘法构成 R-模组。

### 3.2. Nagata 数

第二个抽象将第 2.3 节的双数推广到两个具有不同类型的分量 d 和 e，反映了这样一个观点：表达式的值（其原始值）及其导数（其切向）在概念上处于不同的空间中。我们利用的正是允许原始值和切向独立变化的推广。这一概念最早出现在 Nagata [6] 20 世纪 50 年代初的工作中，名为“模组的理想化”。然而，将 Nagata 的构造应用于 AD 的研究似乎是新颖的。与双数类似，我们将类型 d x e 称为 Nagata 数。

```
data d x e = N { primN :: d,
                 tanN :: e }

instance Functor (d x ) where
  fmap h (N f d) = N f (h d)
```

请注意，类型构造子 d x 在其第二个参数上是函子的，在两个参数上都是双函子（附录 A）。

Nagata 证明了以下基本定理。

> 定理 1. 给定 d-模组 e，则 d x e 承认半环结构。

下面的 Haskell 类型类实例见证了此定理。

```
instance Module d e => Semiring (d x e) where
  zero        = N zero zero
  one         = N one   zero
  (N f df) ⊕ (N g dg) = N (f ⊕ g) (df ⊕ dg)
  (N f df) ⊗ (N g dg) = N (f ⊗ g) ((f ⊗ dg) ⊕ (g ⊗ df))
```

### 3.3. 克罗内克三角函数

我们拼图的最后一块来自以下观察：函数 δ_x y = if x == y then one else zero 是克罗内克三角函数。

```
δ_x(y) = { 1   x = y
         { 0   otherwise
```

这引出了我们第三个基本代数抽象。在 Haskell 中，我们在 Kronecker 类型类中捕捉了这一概念的广义化概念。

```
class Module d e => Kronecker v d e where
  delta :: v → e
```

请注意，此时，Kronecker v d e 上没有强加额外定律；稍后，我们将使用同构条件（定义 5）来约束不同的 AD 变体。其思想是 delta x 不仅为单个变量 y 计算 δ_x(y)，而是一次性为所有变量计算。因此，delta x 是 d-模组 e 中的一个值，其中只有 x 分量为 1，其他全为 0。一个有用的类比是将 v 视为 e 的基向量类型。然后，delta x 是基向量 x 到 e 的嵌入。继续第 3.1 节中 R-模组 R³ 的示例，通常有三个变量 x、y、z，使得

```
delta x = [1 0 0]
delta y = [0 1 0]
delta z = [0 0 1]
```

在 AD 文献中，这些只有一个分量为 1、其他分量为 0 的基向量通常被称为 one-hot 向量。

### 3.4. 抽象自动微分

有了这三个代数结构，我们提出了微分的抽象定义。

```
abstractD :: Kronecker v d => e -> (v -> d) -> Expr v -> d × e
abstractAD var = eval gen where gen x = N (var x) (delta x)
```

接下来，我们展示如何实例化此抽象定义以恢复 forwardAD。稍后，我们改变 e 以获得更高效的版本。

### 3.5. 基础情况：作为稠密函数空间中的 AD 的前向模式 AD

我们通过使用标准函数空间 e = v -> d，将 forwardAD——第 2.4 节给出的经典前向模式 AD 实现——作为 abstractD 的一个实例来恢复。我们将此空间称为 Dense，以与第 4.3 节即将出现的稀疏函数空间形成对比：与计算机代数 [16] 中稠密/稀疏多项式表示类似。

```
type Dense v d = v -> d
```

非正式地，我们可以将此结构视为梯度向量的函数表示，被最小二乘拟合、梯度下降和许多其他应用所需。就像梯度向量一样，它为每个类型 v 的变量包含一个 d 值。其幺半群和 d-模组实例的作用是逐点给出的，使用第 3.1 节的“d-as-d-module 构造”。

```
instance Semiring d => Monoid (Dense v d) where
  zero   = λv → zero
  f₁ ⊕ f₂ = λv → f₁ v ⊕ f₂ v
```

```
instance Semiring d => Module d (Dense v d) where
  d • f = λv → d • (f v) = λv → d ⊗ (f v)
```

稠密函数的克罗内克三角函数是教科书式的。

```
instance (Eq v, Semiring d) => Kronecker v d (Dense v d) where
  delta v = λw → if v ≡ w then one else zero
```

使用此 Kronecker 实例并将双数推广为 d × (Dense v d)，我们得到前向模式 AD 的以下定义。

```
forwardAD_dense :: (Eq v, Semiring d) => (v -> d) -> Expr v -> d × (Dense v d)
forwardAD_dense = abstractD
```

这是 forwardAD，其参数重新排列并将 Dual d 推广：

```
primD (forwardAD var x) = primN (forwardAD_dense var x)
tanD (forwardAD var x) = tanN (forwardAD_dense var x)
```

forwardAD 和 forwardAD_Dense 之间的本质区别是内涵上的。从计算 v -> d × d 中的值转移到计算 d × (v -> d) 中的值，我们不再为每个单独的 v 计算原始值和切向，而是仅为整个梯度计算一次原始值。换句话说，我们在所有偏导数之间共享原始值的计算。例如，示例 2 使用我们的表达式语言表示变量 x 和 y 中的表达式 (x × y) + x + 1。

```
data XY = X | Y
example_1 :: Exp XY
example_2 = Plus (Plus (Times (Var X) (Var Y)) (Var X)) One
```

我们在点 (5, 3) 处计算其梯度：

```
> let (var X = 5; var Y = 3; e = tanN (forwardAD_dense var example_2))
in (e X, e Y)
(4, 5)
```

相比之下，使用 forwardAD 时，我们需要调用它两次：

```
> let (var X = 5; var Y = 3; e = example_2)
in (tanD (forwardAD var X e), tanD (forwardAD var Y e))
```

## 4. 通过构造的 AD 变体

本节解释了我们的方法论，该方法基于构造 Kronecker 同构，并在 forwardAD_dense 的稀疏变体上演示了它。这种方法论将允许我们通过改变切向类型来实例化我们的抽象算法，以获得不同的自动微分变体。

### 4.1. 使用 Kronecker 同构关联 AD 变体

在设计新的 AD 变体时，一个关键关注点是其正确性。我们可以通过证明它们与既定 AD 基线的函数等价性来建立这一点。我们使用 Kronecker 同构来做到这一点。

**定义 4**（Kronecker 同态）。给定变量类型 V 和半环 D，以及类型 E1 和 E2，使得 Kronecker V D E1 和 Kronecker V D E2 成立（因此也成立 Monoid E1、Monoid E2、Module D E1 和 Module D E2），则 Kronecker 同态是一个函数 h :: E1 -> E2，它保留 Kronecker V D 结构：
h zeroE1 = zeroE2
h (x ⊕E1 y) = (h x) ⊕E2 (h y)
h (d •E1 v) = d •E2 (h v)
h (deltaE1 v) = deltaE2 v

**定义 5**（Kronecker 同构）。Kronecker 同构是一对 Kronecker 同态 h :: E1 -> E2 和 h' :: E2 -> E1，它们互为逆：h . h' = id 和 h' . h = id。

在本文余下部分，我们使用 Dense V D 作为基线。因此，在提出新的切向类型 E 时，我们还希望找到一个 Kronecker 同构 h :: Dense V D -> E 以建立其正确性。这个同构是一对函数，由表示函数 rep 及其逆 abs（抽象）组成，遵循数据表示 [17,18] 的术语。为了简化我们的方法，我们在类型类 CorrectAD 中捕获此同构。

```
class Kronecker v d e => CorrectAD v d e where
rep :: Dense v d -> e
abs :: e -> Dense v d
```

借助由 abstractD [20] 的参数性得出的自由定理 [19]，我们可以将算法的新实例与基线关联起来。

> **定理 2.** 给定 CorrectAD V D E 实例，我们有
> fmap abs (abstractD_E var e) = abstractD_Dense var e
> abstractD_E var e = fmap rep (abstractD_Dense var e)

