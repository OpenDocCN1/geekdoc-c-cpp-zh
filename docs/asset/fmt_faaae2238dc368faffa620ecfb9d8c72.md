
|---|---|---|

| 0 | 0 | 0 + 0 = 0 |

| 1 | 3 | 1 + 3 = 0 |

| 2 | 2 | 2 + 2 = 0 |

| 3 | 1 | 3 + 1 = 0 |

（如果上面的表格没有意义，尝试用我们的时钟检查这些情况。）

我们已经证明整数模 4，`ℤ₄`，二元运算符为 `+` 满足群的唯一要求。但我们需要确保它是幺半群。

要成为幺半群，我们需要一个恒等元素。那就是 `0`。用我们的二元运算符将其应用于集合的任意元素，我们会得到回那个元素。

```
type ConstrainAbelian a b = Abelian a b
```

这是一个更好的名字，因为它提醒我们 `Abelian` 类型别名提供了一种轻松约束 `a` 为阿贝尔群的方法，即 `a` 必须是 `Group` 且 `Commutative`。但 `Commutative` 究竟是什么？

`Commutative` 是一个类型类：

```
class Semigroup a <= Commutative a
```

`Commutative` 只是一个 `Semigroup`，具有以下隐含定律：

```
∀ x, y ⇒ x <> y = y <> x    [Commutative]
```

在 PureScript 中，我们无法强制 `<>` 运算符的交换性，所以最好的办法就是将其定义为这样。

为了更好地感受这个类型别名如何使用，让我们看一个简单的例子：

```
find :: ∀ a. Abelian a (Set a -> Maybe a) ❶
```

> ❶ 别名定义中的 `b` 是函数的完整类型签名，即 `(Set a -> Maybe a)`。

它展开为：

```
find :: ∀ a. Group a => Commutative a => Set a -> Maybe a
```

所以 `Abelian` 类型别名只是为函数类型签名添加必要约束的帮助器，即 `Group a => Commutative a =>`。

#### 8.15. PureScript 中的算术运算符

PureScript 中的算术运算符使用不熟悉的类型。在 Haskell 中，类型是 `Num`。一点也不吓人。

要查看这些类型，请使用以下命令运行 PureScript REPL：

```
npx spago repl
```

然后输入 `:t (+)` 来确定加法的类型签名：

```
```purescript

> :t (+)

forall a. Semiring a => a -> a -> a

```
```

类型签名中唯一令人困惑的部分是 `Semiring` 约束。`a -> a -> a` 有意义。事实上，它意味着 `+` 对类型 `a` 的居民集合是封闭的。所以 `Semiring` 至少是一个幺半群。

接下来，让我们试着看看乘法的类型签名是什么：

```
```purescript

> :t (*)

forall a. Semiring a => a -> a -> a

```
```

它也有 `Semiring` 约束。

减法呢：

```
```purescript

> :t (-)

forall a. Ring a => a -> a -> a

```
```

出乎意料。它有一个 `Ring` 约束，不知道那是什么。

最后，除法：

```
```purescript

> :t (/)

forall a. EuclideanRing a => a -> a -> a

```
```

再次，这个约束相当令人惊讶。

所以我们有：

```
```text

Semiring

Ring

EuclideanRing

```
```

谁会想到我们在小学学到的简单算术运算会如此复杂。

事实证明，在 PureScript 中，算术运算符是使用这些抽象代数结构定义的。这样做的好处是这些运算符可以用于非数值事物，从而赋予我们这些抽象的全部威力。

#### 8.17. Semiring 类型类

在 PureScript 中，`Semiring` 是一个类型类定义为：

```
class Semiring a where
    add :: a -> a -> a
    zero :: a
    mul :: a -> a -> a
    one :: a

infixl 6 add as +
infixl 7 mul as *
```

① 运算符优先级使 `*` 比 `+` 更高，这在数字算术中很常见。

我们可以看到 `add` 和 `mul` 的类型签名表明它们是封闭运算，因为它们取 2 个 `a` 并返回一个 `a`。并且存在一个恒等元 `zero` 用于 `add`，另一个恒等元 `one` 用于 `mul`。

典型实现是 `Int`：

```
instance semiringInt :: Semiring Int where
    add = intAdd
    zero = 0
    mul = intMul
    one = 1

foreign import intAdd :: Int -> Int -> Int
foreign import intMul :: Int -> Int -> Int
```

① 实际实现在 Javascript 中。

以下是 `Unit` 的平凡实现：

```
instance semiringUnit :: Semiring Unit where
    add _ _ = unit
    zero = unit
    mul _ _ = unit
    one = unit
```

由于 `Unit` 只有一个居民 `unit`，它是 `add` 和 `mul` 运算的唯一解。所以我们只是忽略输入参数。

并且由于 `zero` 和 `one` 必须属于集合，我们在两种情况下都使用我们唯一的居民 `unit`。

#### 8.18. 函数的 Semiring

使用抽象来表示简单算术的好处之一是你可以将数字推广到行为相似的事物。例如，函数。

你可能不会立刻想到用函数替换数字，但实际上可以做到。这里是函数的 `Semiring` 实例：

```
instance semiringFn :: Semiring b => Semiring (a -> b) where
  add f g x = f x + g x
  zero = \_ -> zero
  mul f g x = f x * g x
  one = \_ -> one
```

这有点复杂且令人困惑，所以让我们逐行分解。

```
instance semiringFn :: Semiring b => Semiring (a -> b) where
```

这个实例适用于类型 `a -> b` 的函数，其中 `b` 也是一个 `Semiring`。这在我们查看 `add` 和 `mul` 时会很重要。

但从中我们可能会问，关于多参数的函数呢？好吧，记住，由于柯里化，所有函数技术上只有一个参数。它们改为返回一个函数来支持多个参数。所以这里的 `b` 可能是个函数。

我们可以通过将 `b` 替换为 `(b -> (c -> d))` 最好地看到这一点。我们再次可以看到，多参数函数等价于一个返回另一个函数的函数，以此类推，直到耗尽所有参数。

并且由于多参数函数只是取 1 个参数并返回一个函数的函数，该函数满足 `Semiring b` 约束。

让我们看下一行：

```
instance semiringFn :: Semiring b => Semiring (a -> b) where
  add f g x = f x + g x
```

`add` 函数在我们考虑其类型签名时看起来有点奇怪：

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

右侧的 `zero` 是 `Semiring b` 的 `zero`，即 `b` 的零，无论 `b` 的类型是什么。

起初这可能看起来很 confusing，但请记住，`zero` 的整个右侧的类型是 `a`（参见 Typeclass 定义），这里是 `(a -> b)`。这意味着表达式 `\\_ -> zero` 接受一个 `a`（它会忽略它）并返回一个 `b`，在本例中为 `zero`。这表明右侧的 `zero` 是 `b` 的 `zero`。因此这里没有无限循环。

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

#### 8.19. 函数的 Semiring 律

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

- ❶ 我们将 `x` 移到等号右侧。
- ❷ 我们使用 `zero` 的定义进行替换。
- ❸ 由于我们可以假设 `b` 是一个 `Semiring`，我们使用 `b` 的右恒等律来进行此化简。
- ❹ ETA 化简，或我喜欢称之为右侧消去。

因此 `add h zero` 等于 `h`，证明了我们的实现遵守右恒等律。现在你可以想象证明左恒等律会多么容易，因为我们有了这个证明。

证明其他律是我们程序员必须做的事情，因为 PureScript 在这里帮不了我们。但证明相当简单，只是繁琐。因此我们不会全部做。我鼓励你练习为函数证明所有这些律。

#### 8.20. 环

环在 `Semiring` 的基础上增加 1 个额外要求。

在环中，集合具有加法逆元：

```
```text

a + (-a) = 0        [加法逆元] ❶

```
```

❶ 环具有 `Semiring` 的所有律加上这一条。

这使得 `(`R`, +)` 成为可交换群，而对于 `Semiring` 来说它是可交换幺半群。

由于具有加法逆元，我们终于可以进行减法，因为减法只是加上逆元。

#### 8.21. 环类型类

在 PureScript 中，我们有一个环的类型类：

```
class Semiring a <= Ring a where
  sub :: a -> a -> a

infixl 6 sub as - ①
```

① 注意 `-` 的优先级与 `Semiring` 中的 `+` 相同。

以下是 `Int` 的典型环实现：

```
instance ringInt :: Ring Int where
  sub = intSub

foreign import intSub :: Int -> Int -> Int ①
```

① 在 Javascript 中实现。

以下是 `Unit` 的平凡实现：

```
instance ringUnit :: Ring Unit where
  sub _ _ = unit
```

以及函数的环：

```
instance ringFn :: Ring b => Ring (a -> b) where
  sub f g x = f x - g x
```

没有真正的惊喜。这里的 `sub` 与 `add` 类似。

#### 8.22. 可交换环类型类

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

由于 `CommutativeRing` 类型类中没有方法，它们的实例只是简单的声明。

#### 8.23. 欧几里得环

欧几里得环是具有 1 个额外要求的可交换环。欧几里得环支持除法。

它有一些相当复杂的律，但我们这里不会涉及。

#### 8.24. 总结

我们现在可以看到为什么简单算术运算符的类型对我们程序员来说如此奇怪。希望本章使它们没那么奇怪。在日常的函数式编程中，你最常使用 `Semigroup` 和 `Monoid` 类型类。

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

记住 `Monoid` 也必须是 `Semigroup`。
