
这里`ginverse`接收类型`a`的值并返回其逆值也是类型`a`。这是因为`Group`也是一个`Magma`。

## 9.28. 为 `Mod4` 编写 `Group`

在编写`Group`实例时，你必须确定集合中每个值的逆值是什么。记住恒等元素是它自己的逆。

另外，请记住，二元运算符是加法，这意味着要确定一个值的逆，我们必须问自己：“我必须加什么到这个值上才能得到我们的恒等值？”

如果有帮助，可以参考我们的时钟表盘。

试试看，看看你做得如何。

## 9.29. `Group` for `Mod4` 的代码

让我们从`Zero`开始：

```
instance groupMod4 :: Group Mod4 where
  ginverse Zero = Zero
```

由于`Zero`是我们的恒等值，它就是它自己的逆。

接下来我们编码`One`：

```
instance groupMod4 :: Group Mod4 where
  ginverse Zero = Zero
  ginverse One = Three
```

我们必须先加`Three`才能绕回到`Zero`。

接下来，我们添加`Two`：

```
instance groupMod4 :: Group Mod4 where
  ginverse Zero = Zero
  ginverse One = Three
  ginverse Two = Two
```

我们必须加比`One`情况少一个的值才能回到`Zero`。

最后，最后一种情况：

```
instance groupMod4 :: Group Mod4 where
    ginverse Zero  = Zero
    ginverse One   = Three
    ginverse Two   = Two
    ginverse Three = One
```

注意`One`和`Three`的加法与`Three`和`One`的加法相同。我们的运算符不必是可交换的，但事实证明它是可交换的。所以，如果我们愿意，我们可以为我们的类型创建可交换实例。

```
class Semigroup g <= Commutative g

instance commutativeMod4 :: Commutative Mod4
```

记住我们的类型只需要是`Semigroup`就可以使其可交换。

## 9.30. 为 `Mod4` 编写 `Eq` 和 `Show`

在为我们新的数据类型编写测试代码之前，我们需要一些有用的实例，即`Eq`和`Show`。

我们已经做过很多次了，所以应该相当容易。在继续之前自己写它们。

## 9.31. `Eq` 和 `Show` for `Mod4` 的代码

代码与`AndBool`和`OrBool`完全一样：

```
data Mod4 = Zero | One | Two | Three
derive instance eqMod4 :: Eq Mod4
derive instance genericMod4 :: Generic Mod4 _

instance showMod4 :: Show Mod4 where
    show = genericShow
```

## 9.32. 为 `Mod4` 编写 `verifyMod4Semigroup`

我们应该确保我们编写的`Semigroup`实例遵守定律。

我们可以参考`AndBool`和`OrBool`来看看如何创建验证函数。

不要忘记将此函数调用添加到你的测试代码中。

## 9.33. `verifyMod4Semigroup` for `Mod4` 的代码

```
verifyMod4Semigroup :: Effect Unit
verifyMod4Semigroup = do
  log "Verifying Mod4 Semigroup Laws (1 test)"
  log $ show $ (One <> Two) <> Three == One <> (Two <> Three) ①
```

① 打印 true。

同样，这个测试代码有很多变体。你的可以有所不同仍然是正确的。最主要的是确保左右两边仅在括号上有所不同。

## 9.34. 为 `Mod4` 编写 `verifyMod4Monoid`

接下来，我们想检查我们的`Monoid`是否是好公民。

参考`AndBool`和`OrBool`获取帮助，将`verifyMod4Monoid`添加到你的测试代码中，看看效果如何，然后再进入下一节。

## 9.35. `verifyMod4Monoid` for `Mod4` 的代码

```
verifyMod4Monoid :: Effect Unit ①
verifyMod4Monoid = do
  log "Verifying Mod4 Monoid Laws (1 test)"
  log $ show $ mempty <> One == One <> mempty && One <> mempty == One ②
```

① 在你的测试代码中添加对该函数的调用。

② 打印 true。

注意这里我们只有一个测试。我们只需要这个测试来证明`mempty`不会改变值，并且由于这个测试在左边和右边都有`Zero`，所以它涵盖了两种情况。

## 9.36. 为 `Maybe` 编写 `Semigroup`

有时，正如我们所见，组合事物的方式可能不止一种。例如，对于`Int`，我们可以通过加法或乘法来组合它们。我们通过为每种情况创建`newtype`来实现这一点，即`AddInt`和`MultInt`。

在为`Maybe`编写`Semigroup`时，有两种可能的情况。让我们举个例子：

```haskell
(Just 10 <> (Just 20 <> Just 30)) = Just 10 ❶
(Just 10 <> (Just 20 <> Just 30)) = Just 20 ❷
(Just 10 <> (Just 20 <> Just 30)) = Just 30 ❸
```

- ❶ 取第一个 `Just`。

- ❷ 有时取第一个 `Just` 然后取第二个 `Just`。这种情况没有意义。

- ❸ 取最后一个 `Just`。

要得到 `Just 20` 的结果，我们首先必须选择 `second` 值，即括号内的部分。接下来，为了评估括号内的内容，我们必须选择 `first`。这完全荒谬，因为我们不能随意选择。所以我们将忽略这种情况。

但是，我们在这新的例子中也没有好到哪里去，因为我们仍然有 2 种可能性。所以就像 `AddInt` 和 `MultInt` 一样，让我们为这两种情况创建 2 个 `newtypes`：

```haskell
newtype First a = First (Maybe a)

newtype Last a = Last (Maybe a)
```

我们称之为 `First` 和 `Last`，以表示在长串的 `appends` 中，我们取第一个 `non-Nothing` 值或最后一个。

### 9.37. 为 `First` 编写 `Semigroup` 和 `Monoid`

继续为`First`编写`Semigroup`和`Monoid`实例，记住`Nothing`是我们的恒等元，因此在使用`<>`应用时对任何值都没有影响。

在阅读解决方案之前自己尝试一下。

### 9.38. `Semigroup` 和 `Monoid` for `First` 的代码

首先，定义：

```haskell
newtype First a = First (Maybe a)
```

接下来，`Semigroup` 实例：

```
import Data.Maybe (Maybe (..)) ①

instance semigroupFirst :: Semigroup (First a) where
  append (First Nothing) last = last ②
  append first _             = first ③
```

① 添加了此导入。

② 如果第一个是`Nothing`则保留最后一个。

③ 否则，始终保留第一个。

我们保留第一个值，除非第一个是`Nothing`。请注意，一旦我们得到第一个非`Nothing`，我们就会无限期地保留它，因为整个右手边被忽略了。这将有效地在我们找到第一个非`Nothing`时短路计算。

最后，我们编写`Monoid`实例：

```
instance monoidFirst :: Monoid (First a) where
  mempty = First Nothing
```

请注意，它不仅仅是`Nothing`（双关语无意），而是`First Nothing`。

## 9.39. 为 `Last` 编写 `Semigroup` 和 `Monoid`

在完成了`First`之后，编写`Last`应该很容易。在继续解决方案之前先试试看。

## 9.40. `First` 的 `Semigroup` 和 `Monoid` 的代码

首先，定义：

```
newtype Last a = Last (Maybe a)
```

接下来是`Semigroup`实例：

```
instance semigroupLast :: Semigroup (Last a) where
  append first (Last Nothing) = first ①
  append _ last               = last ②
```

① 如果`last`是`Nothing`，则保留`first`。

② 否则，保留`last`。

同样，我们保留最后一个值，除非它是`Nothing`。与`First`不同，我们没有忽略右手边的机会，这意味着使用`Last`我们将不会短路。这使得合并`Last`的效率低于`First`，因为我们必须计算表达式的每个值：

```
First (Just 1) <> (First (Just 2) <> First Nothing) ①
Last (Just 1) <> (Last (Just 2) <> Last Nothing) ②
```

① 我们不需要计算`First (Just 2) <> First Nothing`，因为我们已经通过`First (Just 1)`找到了第一个非`Nothing`。

② 我们必须计算`Last (Just 2) <> Last Nothing`，因为我们必须继续寻找最后一个非`Nothing`。

最后，`Monoid`实例：

```
instance monoidLast :: Monoid (Last a) where
  mempty = Last Nothing
```

同样，它不仅仅是`Nothing`，而是`Last Nothing`。

让我们编写测试代码：

```
-- COMPILER ERROR!!
log $ show $ First Nothing <> First (Just 77) ①
log $ show $ Last (Just 1) <> Last (Just 99) ②
```

① 打印`(First (Just 77))`。

② 打印`(Last (Just 99))`。

为`First`和`Last`编写`Show`实例以消除编译器错误。

以下是这些更改：

```
length :: ∀ a. List a -> Int
length Nil      = 0 ①
length (x : xs) = 1 + length xs
```

① 当已耗尽`List`时终止。

这些是我们将更仔细研究的函数类型。

让我们从`length`开始：

```
length :: ∀ a. List a -> Int
length Nil      = 0
length (x : xs) = 1 + length xs ①
```

① 非尾递归。

请注意，我们这里没有`State`需要传递。`State`维护在`Stack`中。我们需要返回以加 1。这就是我们计数的方式。

但在`length`的尾递归版本中，我们显式传递`State`，这通过`go`函数的存在得以证明：

```
length :: ∀ a. List a -> Int
length l = go 0 l where
go :: ∀ a. Int -> List a -> Int ①
go acc Nil      = acc
go acc (x : xs) = go (acc + 1) xs
```

① 第一个参数是长度的累积计数。

这类函数非常适合一种称为`Fold`的过程。

> `Fold`是使用`State`迭代的通用方式。

`Fold`的一个主要限制是它们不会短路。这意味着我们可以使用`Fold`重写`length`，但不能重写`index`或`findIndex`。

## 10.1. `Fold` 的其他名称

在许多非函数式语言中，`fold`也称为`reduce`。在我们的`length`函数的情况下，我们将`List`归约为单个`Int`。但这并不总是如此。我们可以使用`fold`来分解一个结构并构建另一个结构，例如处理`List`并生成`Map`（键/值存储）。

在范畴论中，你会听到 **Catamorphism** 这个术语（*Cata* 表示 *down*，*morph* 表示 *shape*），本质上意味着 *分解结构*。

这与 **Anamorphism** 相反（*Ana* 表示 *up*，*morph* 表示 *shape*），本质上意味着 *构建结构*。

如果你忘记这些术语，你可以记住 Anabolic Steroids 它构建肌肉或 Catabolic Exercise 它分解肌肉组织并燃烧脂肪。

重点是 `folds` 被称为 `Catamorphisms` 因为它们分解原始结构。还有另一个概念称为 `unfold`，使用频率远低于它，被称为 `Anamorphisms` 因为它们从单个起始值构建结构。

我们这里只关注 `folds`。

## 10.2. `Foldable` 类型类

在 PureScript 中，如果一个类型具有`Foldable`的实例，则它可以是`Foldable`。以下是该类型类：

```purescript
class Foldable f where
  foldr :: ∀ a b. (a -> b -> b) -> b -> f a -> b
  foldl :: ∀ a b. (b -> a -> b) -> b -> f a -> b
  foldMap :: ∀ a m. Monoid m => (a -> m) -> f a -> m
```

让我们一次分解一个函数。首先是 `foldr`：

```purescript
foldr :: ∀ a b. (a -> b -> b) -> b -> f a -> b
```

让我们分解其每个参数：

```text
(a -> b -> b)    — 用于处理 Foldable 元素的函数
b                — 初始值
f a              — Foldable 类型 `f`，例如 `List` 或 `Array`
```

`foldr` 返回一个 `b` 作为折叠操作的最终结果。

函数名以 `r` 结尾，意味着操作是 **右结合** 的。我们很快会看到一个很好的例子。

接下来，我们来看 `foldl`：

```haskell
foldl :: ∀ a b. (b -> a -> b) -> b -> f a -> b
```

它与 `foldr` 相同，除了第一个参数。第一个参数是一个函数，其参数与 `foldr` 相比是 `flipped` 的。我们很快会看到为什么这很重要。

最后是 `foldMap`：

```haskell
foldMap :: ∀ a m. Monoid m => (a -> m) -> f a -> m
```

让我们分解其每个参数：

```text
(a -> m)    -- 用于将元素转换为 Monoid 的函数
f a         -- Foldable 类型 `f`，例如 `List` 或 `Array`
```

此函数返回一个 `m`，它是一个 `Monoid`。

你能想到为什么它是 `Monoid` 而不是 `Semigroup` 吗？它本可以是 `Semigroup`，但那样我们会让用户负担传递初始值的责任，而如果可能的话，这意味着该类型可能已经是 `Monoid`。

请注意 `foldMap` 不像 `foldl` 和 `foldr` 那样需要初始值。那是因为 `foldMap` 使用 `Monoids` 并且可以使用类型的 `mempty` 作为其初始值。

另外，请注意这里变量 `f` 被用作我们要折叠的集合或结构。同样，这是因为它代表 `Functor`，因为大多数 `Functors` 也是 `Foldable`。不用担心，我们很快就会花大量时间研究 `Functors`。

## 10.3. `Fold` 结合性

`foldr` 是右结合的，而 `foldl` 是左结合的，意味着：

```haskell
foldr (-) 99 [1, 2, 3] == 1 - (2 - (3 - 99)) == -97
foldl (-) 99 [1, 2, 3] == ((99 - 1) - 2) - 3 == 93
```

请注意初始值 `99` 的位置。对于 `foldr` 它在最右边，对于 `foldl` 它在最左边。

为了更好地理解差异，让我们重写 `(-)` 以显示其组成部分：

```haskell
foldr (\n acc -> n - acc) 99 [1, 2, 3] == -97
foldl (\acc n -> acc - n) 99 [1, 2, 3] == 93
```

请注意，在`foldr`中，我们的累加器`acc`在参数列表的右边，并且在二元运算符`−`的右边。

另外，请注意，在`foldl`中，`acc`在参数列表的左边，并且在`−`的左边。
