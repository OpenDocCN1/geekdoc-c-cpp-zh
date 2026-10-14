

```
```haskell
add :: a -> a -> a
```
```

接受 2 个参数，而不是 3 个。

然而，我们的 `add` 函数中有 3 个参数。如果还记得之前的内容，我们可以将变量移到等号另一侧。让我们这样做，看看我们实际上只有 2 个参数：

```
```haskell
instance semiringFn :: Semiring b => Semiring (a -> b) where
  add f g = \\x -> f x + g x
```
```

等价于上面原始的 `add` 函数，但现在左侧只有 2 个参数。

现在我们只有 2 个参数。原始的编码方式要干净得多，但写出 Lambda 版本只是为了提醒我们它真正的工作原理。

接下来一行代码：

```
```haskell
instance semiringFn :: Semiring b => Semiring (a -> b) where
  add f g x = f x + g x
  zero = \\_ -> zero
```
```

`add` 的恒等元是 `zero`，它看起来像是无限循环，因为等号两边都有 `zero`。但事实并非如此。

左侧的 `zero` 是 `Semiring (a -> b)` 的 `zero`，即函数 的 `zero`。

右侧的 `zero` 是 `Semiring b` 的 `zero`，即 b 的零，无论 b 的类型是什么。

起初这可能看起来很 confusing，但请记住，`zero` 的整个右侧的类型是 a（参见 Typeclass 定义），这里是 `(a -> b)`。这意味着表达式 `\\_ -> zero` 接受一个 a（它会忽略它）并返回一个 b，在本例中为 `zero`。这表明右侧的 `zero` 是 b 的 `zero`。因此这里没有无限循环。

剩下的代码行：

```
```haskell
instance semiringFn :: Semiring b => Semiring (a -> b) where
  add f g x = f x + g x
  zero = \\_ -> zero
  mul f g x = f x * g x
  one = \\_ -> one
```
```

`mul` 和 `one` 与 `add` 和 `zero` 类似，其中 `one` 是 `mul` 的恒等元。

## 8.19. 函数的 Semiring 律

我们应该验证我们的 `Semiring` 实例的律。它们再次列出如下：

可交换幺半群（其二元运算可交换）的律和加法：

```
(`R`, `+`) 是具有 `0` 恒等元的 **可交换幺半群**：

(a + b) + c = a + (b + c)    [**结合律**] (**半群**)
0 + a = a + 0 = a              [**恒等律**] (**幺半群**)
a + b = b + a                  [**可交换律**] (**可交换幺半群**)
```

接下来是幺半群和乘法的律：

```
(`R`, `·`) 是具有 `1` 恒等元的 **幺半群**：

(a · b) · c = a · (b · c)    [**结合律**] (**半群**)
1 · a = a · 1 = a              [**恒等律**] (**幺半群**)
```

然后是乘法在加法左右分配的律：

```
a · (b + c) = (a · b) + (a · c)              [**左分配律**]
(a + b) · c = (a · c) + (b · c)              [**右分配律**]
```

最后是乘以 `0` 消去 `R` 的律：

```
0 · a = a · 0 = 0                         [**消去律**]
```

正如你所见，这将是一个冗长的过程，所以我们只做一个，但过程会类似。

让我们证明加法的右恒等律：

```
a + 0 = a ❶
```

❶ 在右手边加上 `0` 不会影响原始值（或我们这里的情况是函数）。

这是我们为函数提供的 Semiring 实例：

```
```purescript
instance semiringFn :: Semiring b => Semiring (a -> b) where
  add f g x = f x + g x
  zero = \_ -> zero
  mul f g x = f x * g x
  one = \_ -> one
```
```

这是我们的证明：

```
```text
b is a Semiring                                      [Given]
add h zero = \x -> h x + zero x                      [Definition] ❶
= \x -> h x + (\_ -> zero) x                         [Substitution] ❷
= \x -> h x + zero                                     [Function Application]
= \x -> h x                                            [Semiring Right Identity for b] ❸
= h                                                    [ETA Reduction] ❹
```
```

- ❶ 我们将 x 移到等号右侧。
- 
- ❷ 我们使用 `zero` 的定义进行替换。
- 
- ❸ 由于我们可以假设 `b` 是一个 `Semiring`，我们使用 `b` 的右恒等律来进行此化简。
- 
- ❹ ETA 化简，或我喜欢称之为右侧消去。

因此 `add h zero` 等于 h，证明了我们的实现遵守右恒等律。现在你可以想象证明左恒等律会多么容易，因为我们有了这个证明。

证明其他律是我们程序员必须做的事情，因为 PureScript 在这里帮不了我们。但证明相当简单，只是繁琐。因此我们不会全部做。我鼓励你练习为函数证明所有这些律。

## 8.20. 环

环在 Semiring 的基础上增加 1 个额外要求。

在环中，集合具有加法逆元：

```
```text
a + (-a) = 0        [加法逆元] ❶
```
```

❶ 环具有 Semiring 的所有律加上这一条。

这使得 `(R, +)` 成为可交换群，而对于 Semiring 来说它是可交换幺半群。

由于具有加法逆元，我们终于可以进行减法，因为减法只是加上逆元。

## 8.21. 环类型类

在 PureScript 中，我们有一个环的类型类：

```
class Semiring a <= Ring a where
  sub :: a -> a -> a

infixl 6 sub as - ①
```

① 注意 – 的优先级与 Semiring 中的 + 相同。

以下是 Int 的典型环实现：

```
instance ringInt :: Ring Int where
  sub = intSub

foreign import intSub :: Int -> Int -> Int ①
```

① 在 Javascript 中实现。

以下是 Unit 的平凡实现：

```
instance ringUnit :: Ring Unit where
  sub _ _ = unit
```

以及函数的环：

```
instance ringFn :: Ring b => Ring (a -> b) where
  sub f g x = f x - g x
```

没有真正的惊喜。这里的 sub 与 add 类似。

## 8.22. 可交换环类型类

环对加法是可交换的。但可交换环对加法和乘法都是可交换的。

类型类非常简单，因为我们无法在 PureScript 中强制可交换性：

```
class Ring a <= CommutativeRing a
```

规范实现是平凡的：

```
instance commutativeRingInt :: CommutativeRing Int
instance commutativeRingUnit :: CommutativeRing Unit
instance commutativeRingFn :: CommutativeRing b => CommutativeRing (a -> b)
```

由于 CommutativeRing 类型类中没有方法，它们的实例只是简单的声明。

## 8.23. 欧几里得环

欧几里得环是具有 1 个额外要求的可交换环。欧几里得环支持除法。

它有一些相当复杂的律，但我们这里不会涉及。

## 8.24. 总结

我们现在可以看到为什么简单算术运算符的类型对我们程序员来说如此奇怪。希望本章使它们没那么奇怪。在日常的函数式编程中，你最常使用 Semigroup 和 Monoid 类型类。

但了解它们在层级中的位置是好的：

![](img/8c0e9b687c62642e828ccb5481e11313_340_0.png)

了解算术运算符层级也很重要，这样我们就不会因为约束中使用的复杂名称而感到害怕：

|  |  |
|---|---|
| EuclideanRing | 除法 |
| CommutativeRing | (R, *) 是可交换幺半群 |
| Ring | (R, +) 是可交换群（减法） |
| Semiring | (R, +) 是可交换幺半群 (R, *) 是幺半群 |

```
```haskell
class Semigroup a where
  append :: a -> a -> a

infixr 5 append as <>
```
```

> ① 组合 2 个 `a` 并产生一个 `a`。这满足了在二元运算符 `<>` 下封闭的 Magma 要求。

## 9.4. 编写 `Monoid` 类型类

接下来，尝试在不查阅任何其他文档的情况下为 `Monoid` 编写类型类。

记住 Monoid 也必须是 Semigroup。

## 9.5. `Monoid` 类型类的代码

```
```haskell
class Semigroup a <= Monoid a where
  mempty :: a
```
```

> ① `Semigroup` 是 `Monoid` 的超类，即每个 Monoid 实例也必须有一个 `Semigroup` 实例。

## 9.6. 为 `AndBool` 编写 `Semigroup`

让我们从以下数据类型开始：

```
```haskell
import Data.Generic.Rep (class Generic)
import Data.Show.Generic (genericShow)

data AndBool = AFalse | ATrue
derive instance eqAndBool :: Eq AndBool
derive instance genericAndBool :: Generic AndBool _

instance showAndBool :: Show AndBool where
  show = genericShow
```
```

> ① 我们需要添加这些导入以使用 `genericShow`。

> ② 这是一个布尔型的数据类型，其二元运算符将是逻辑与。

> ③ 我们稍后在测试代码中需要它。

> ④ 我们为我们的类型派生 Generic 实例，以便可以使用 `genericShow`。

