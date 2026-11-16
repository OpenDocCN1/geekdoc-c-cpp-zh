
恒等律:
zero ⊕ x = x ⊕ zero
one ⊗ x = x = x ⊗ one

结合律:
x ⊕ (y ⊕ z) = (x ⊕ y) ⊕ z
x ⊗ (y ⊗ z) = (x ⊗ y) ⊗ z

分配律:
x ⊗ (y ⊕ z) = (x ⊗ y) ⊕ (x ⊗ z)
(x ⊕ y) ⊗ z = (x ⊗ z) ⊕ (y ⊗ z)

吸收元: zero ⊗ x = zero = x ⊗ zero

图 1. 交换半环定律。

```
data X = X
example₁ :: Expr X
example₁ = Times (Var X) (Plus (Var X) One)
```

我们通过将符号表达式映射到一个（交换）半环，为符号表达式赋予了重载含义。半环中的“semi”指的是半环不需要具有加法逆元这一事实。此处省略该要求，因为自动微分（AD）不需要它。尽管如此，第 6.1 节表明，如果存在这样的逆元，则可以加以容纳。我们施加的交换律要求并非必需，但简化了展示。第 6.2 节将该方法扩展到非交换半环，这对于支持例如矩阵是必要的。重载使我们能够灵活地从表达式的普通值和不同的 AD 变体两方面来解释表达式。

### 定义 1（半环）

半环是一个集合，配备两个二元运算 ⊕（“加法”）和 ⊗（“乘法”）以及两个特殊元素 zero 和 one。这些应遵循图 1 的定律：⊕ 和 ⊗ 应该都满足结合律和交换律，并分别具有单位元 zero 和 one。此外，⊗ 应该对 ⊕ 具有分配律，并以 zero 为吸收元。

在 Haskell 中，我们在 Semiring 类型类中捕获半环的代数概念，并为遵循定律的数值类型（例如 Int、Float⁴）提供实例。

```
class Semiring d where
  zero :: d
  one :: d
  (⊕) :: d → d → d
  (⊗) :: d → d → d
```

```
instance Num a => Semiring a where
  zero = 0
  one = 1
  (⊕) = (+)
  (⊗) = (*)
```

有一个半环实例特别引起我们的兴趣：即针对符号表达式 Expr v 的实例，其由定律⁴商化。

```
instance Semiring (Expr v) where
  zero = Zero
  one = One
  (⊕) = Plus
  (⊗) = Times
```

使此实例特别的是，它是自由半环实例，从而产生了 fold 风格的 eval 函数。该求值器通过对符号表达式进行结构递归，在给定变量映射 var :: v → d 的情况下，将它们映射到半环 d 中的解释。

```
eval :: Semiring d => (v → d) → Expr v → d
eval var (Var x) = var x
eval var Zero = zero
eval var One = one
eval var (Plus e₁ e₂) = eval var e₁ ⊕ eval var e₂
eval var (Times e₁ e₂) = eval var e₁ ⊗ eval var e₂
```

这样，我们就可以使用 Int 半环对 example₁ 在 X = 5 时进行求值。

```
> eval (λX → 5) example₁
30
```

## 2.2. 同态

自由半环的概念、相关的 eval 函数及其性质是《程序设计代数》[5]中适用于任何代数结构的通用结果的特例。另一个相关概念，将证明是本文的核心，即同态。非正式地说，这是一个保持代数结构的函数。更正式地说，

### 定义 2（半环同态）

两个半环 D₁ 和 D₂ 之间的（半环）同态是一个函数 h :: D₁ → D₂，它保持半环结构：

h zero₁ = zero₂          h (x ⊕₁ y) = h x ⊕₂ h y
one₁ = one₂             h (x ⊗₁ y) = h x ⊗₂ h y

半环同态可复合：给定同态 h₁ :: D₁ → D₂ 和 h₂ :: D₂ → D₃，它们的复合 h₂ ∘ h₁ :: D₁ → D₃ 也是一个同态；并且预期的定律成立。此外，恒等函数 id :: D → D 平凡地是一个同态。函数 eval var 对于任何 var 的选择都是一个同态。事实上，它是满足 h (Var v) = var v 的唯一同态 h。从这一唯一性性质推导出两个有用的性质：

### 性质 1（融合）

融合性质允许我们将任何同态 h 纳入求值：h ∘ eval var = eval (h ∘ var)。

### 性质 2（反射）

反射性质观察到，使用 Var 进行求值是恒等函数：eval Var = id。

## 2.3. 符号微分与对偶数

eval 同态还允许我们进行符号微分。我们在 derive 函数中捕获其规则，使用 Expr v 的 Semiring 实例，并利用乘法情况中的交换律。

```
derive :: Eq v => v -> Expr v -> Expr v
derive x (Var y)   = if x == y then one else zero
derive x Zero      = zero
derive x One       = zero
derive x (Plus e₁ e₂) = derive x e₁ ⊕ derive x e₂
derive x (Times e₁ e₂) = (e₂ ⊗ derive x e₁) ⊕ (e₁ ⊗ derive x e₂)
```

这些不适合 eval 的 fold 风格递归方案，因为在 Times 的情况下，e₁ 和 e₂ 出现在递归调用之外（灰色）。利用所谓的“香蕉分割”性质 [3–11]，我们可以将此函数转换为适当的形式：我们使其返回一个元组 (Expr v, Expr v)，包含原始表达式和符号导数。

```
derive' x e = (e, derive x e)
```

我们由此获得 derive' 的以下结构递归定义，然后可以通过投影第二个分量来恢复 derive：

```
derive' :: Eq v => v -> Expr v -> (Expr v, Expr v)
derive' x (Var y)   = (Var y, if x == y then one else zero)
derive' x Zero      = (zero, zero)
derive' x One       = (one, zero)
derive' x (Plus e₁ e₂) = let (e'₁, d₁) = derive' x e₁
                             (e'₂, d₂) = derive' x e₂
                             in (e'₁ ⊕ e'₂, d₁ ⊕ d₂)
derive' x (Times e₁ e₂) = let (e'₁, d₁) = derive' x e₁
                             (e'₂, d₂) = derive' x e₂
                             in (e'₁ ⊗ e'₂, (e'₂ ⊗ d₁) ⊕ (e'₁ ⊗ d₂))
```

在将 derive' 的功能用 eval 编写之前，我们将 (Expr v, Expr v) 推广到其分量来自任意半环的元组。在 AD 文献中，这些被称为对偶数，最初由 Clifford [4] 提出。

```
data Dual d = D { primal :: d, tangent :: d }
instance Functor Dual where
  fmap :: (a -> b) -> Dual a -> Dual b
  fmap h (D f g) = D (h f) (h g)
```

对偶数是函子的；fmap f 使用 f 转换两个参数。对偶数 D d x 的两个分量分别称为原值 x 和切线 dx。对于半环 d，类型 Dual d 也承认半环结构，其中切线的定义精确地遵循 derive 的相应情况。

```
instance Semiring d => Semiring (Dual d) where
  zero = D zero zero
  one = D one zero
  (D f d) ⊕ (D g dg) = D (f ⊕ g) (d ⊕ dg)
  (D f d) ⊗ (D g dg) = D (f ⊗ g) ((g ⊗ d) ⊕ (f ⊗ dg))
```

现在，符号微分可以被视为另一种求值实例，但目标是符号表达式上的对偶数半环：

```
symbolic :: Eq v => v -> Expr v -> Dual (Expr v)
symbolic x = eval gen where gen y = D (Var y) (δ_x y)
δ_x y = if x == y then one else zero
```

## 2.4. 经典前向自动微分

自动微分（AD）是程序化地计算表达式在某一点处的值和导数的算法的统称 [12-14]。因此，如果我们将符号微分与随后求值到半环 d 相结合，我们就得到了前向模式 AD 的规范：

```
forwardAD var x = fmap (eval var) . symbolic x
```

我们可以通过利用 eval 的融合性质使此规范更高效。

```
fmap (eval var) . symbolic x
= {- definition of symbolic -
fmap (eval var) . eval gen where gen y = D (Var y) (δ_x y)
= {- eval fusion (Property 1.) -
eval (fmap (eval var) . gen) where gen y = D (Var y) (δ_x y)
= {- fmap (eval var) . gen -
δ_x y = if x == y then one else zero
```

在将 fmap (eval var) 内联到 gen 后，我们得到了前向模式 AD 的经典定义，它只调用一次 eval。与 symbolic 相比的差异以灰色突出显示。

```
forwardAD :: (Eq v, Semiring d) => (v -> d) -> v -> Expr v -> Dual d
forwardAD var x = eval gen where gen y = D (Var y) (δ_x y)
δ_x y = if x == y then one else zero
```

例如，example_1 在 X = 5 处的导数是 11；计算结果的过程如图 2 所示。

```
> forwardAD (\X -> 5) X example₁
D 30 11
```

## 2.5. 将符号 AD 作为前向 AD

请注意，符号微分与自动微分之间唯一的本质区别在于：前者求值到符号 Expr v 半环，而后者使用“数值”半环 d。事实上，我们也可以让 forwardAD 使用符号半环，用 Var 解释变量。

```
forwardAD Var
= {- AD specification (Specification 2.4.) -
```
