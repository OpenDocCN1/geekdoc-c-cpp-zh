
到目前为止，你应该知道如果没有办法，我是不会问这个问题。

## 12.16. `Bifunctor` 类型类

我们已经看到 `Functor` 只能映射 1 个类型参数。要映射 2 个类型参数，我们需要使用称为 `Bifunctor` 的东西（Bi 表示两个）。

以下是 PureScript 中的 `Bifunctor`：

```
class Bifunctor f where
  bimap :: ∀ a b c d. (a -> c) -> (b -> d) -> f a b -> f c d
```

① 类型构造子 `f` 接受 2 个参数，不像 `Functor` 只接受 1 个。

`bimap` 接受 2 个函数，一个用于映射第一个类型 `a`，一个用于映射第二个类型 `b`。

现在我们可以为 `Choice` 创建 `Bifunctor` 实例，而不会被迫短路：

```
instance bifunctorChoice :: Bifunctor Choice where
  bimap f _ (PickA x) = PickA $ f x
  bimap _ g (PickB y) = PickB $ g y
```

① 我们不再需要像在 `Functor` 中那样使用 `Choice a`，因为 `Bifunctor` 的 `f` 接受 2 个参数，`Choice` 也是如此。换句话说，它们的 Kinds 匹配，即 `Choice :: Type -> Type` 匹配 `f :: Type -> Type`。

现在我们对 `Choice` 的两种情况都进行映射，因为我们现在为每种情况都有一个量身定制的函数。

`Choice` 是一个和类型（`Coproduct`），但对于积类型呢？你能想到一个可以做成 `Bifunctor` 的积类型吗？

比如这个：

```
data Tuple a b = Tuple a b

instance bifunctorTuple :: Bifunctor Tuple where
  bimap f g (Tuple x y) = Tuple (f x) (g y)
```

在这里我们每次都映射 `Tuple` 的两边。但如果我们只想映射 `Tuple` 的左边呢？

我们可以写出以下函数：

```
lmap :: ∀ a b c f. Bifunctor f => (a -> b) -> f a c -> f b c
lmap f = bimap f identity
```

① 我们提供 `identity` 作为右侧映射，effectively 将右侧映射回自身。

结果是这个函数和 `rmap` 都在 PureScript `Bifunctor` 库中，包 `package-bifunctors`，模块 `Data.Bifunctor`。

`rmap` 映射 `Bifunctor` 的右侧，这基本上就是 `Functor` 中的 `map`。

## 12.17. 范畴论中的 Bifunctors

让我们回到 `Hask` 范畴，其中对象是类型，态射是函数。

当我们查看 `Hask` 中的 `Functors` 时，我们看到它如何将类型映射到其他类型。但我们只有一个类型可供使用，而 `Bifunctors` 将 2 个类型映射到 2 个类型。

因此，对于 `Bifunctors`，我们的对象必须是 2 个类型。所以我们需要一个是 2 个类型的类型。如果这听起来不可能或悖论，实际上并非如此。

让我们在跨过那座桥之前先看几件事。首先，让我们回顾一下 **笛卡尔积**。这里有一个例子：

```
A = { 1, 2, 3 }
B = { a, b }

A × B = { (1, a), (1, b), (2, a), (2, b), (3, a), (3, b) }
```

笛卡尔积是由取 `Set A` 的每个元素并与 `Set B` 中的每个元素组合而成的 `成对集合`。

而这里是正式定义：

```
A × B = { (a, b) : a ∈ A and b ∈ B }
```

再次，让我们解析一下数学：

```
A × B          （集合 A 和 B 之间的笛卡尔积）
{ ... }         （包含一个集合）
(a, b)         （元素对）
a ∈ A           （a 是集合 A 的元素）
b ∈ B           （b 是集合 B 的元素）
```

在范畴中，对象和态射都是集合。特别是在 `Hask` 中，我们有一个 `类型集合`。对于 `Bifunctor` 我们需要一个对象是 2 个类型的范畴。我们可以通过取 `Hask` 与 `Hask` 的笛卡尔积来创建这样的范畴。

![](img/8c0e9b687c62642e828ccb5481e11313_437_0.png)

我们新的范畴 Hask × Hask 是通过取我们对象的笛卡尔积而用一些黑魔法 conjured 出来的。但我们新的范畴是一个有效的范畴吗？

让我们确保态射可以组合。但等等，我们新范畴中的态射是什么？在 Hask 中，它只是从类型到类型的函数，但我们有一个类型对，这意味着我们需要一对函数。

![](img/8c0e9b687c62642e828ccb5481e11313_438_0.png)

我们接下来需要证明我们的态射可以组合：

```
(f, g) ∘ (f', g') = (f ∘ f', g ∘ g')
```

我们需要定义恒等态射：

```
(identity, identity)
```

¹ 只是 `identity` 函数的一对。

因此，这个范畴似乎是有效的。我说似乎是因为我们还没有穷举地证明一切，例如结合律。但它成立。

现在，我们可以在 `Hask × Hask` 中查看 Functors：

![](img/8c0e9b687c62642e828ccb5481e11313_439_0.png)

这相当不引人注目。它看起来就像任何范畴之间的 `Functor`，只是略有不同之处在于它对类型对进行操作，这基本上就是 `Bifunctor` 的定义，其定义如下：

```
对于 *范畴*，C、D 和 E，*函子*

    F: C × D → E

也称为从 C 和 D 到 E 的 *Bifunctor*。
```

C × D 在这个定义中是我们上面图表中的范畴 Hask × Hask。而 E 在这个定义中是我们上面图表中的范畴 D。

最后，我们准备好看看 `Either` 如何成为一个 `Bifunctor`。但首先让我们稍作停留。

首先要注意的是，我们在 PureScript 中使用 `Tuple` 来表示对，因此我们将有序对 (a, b) 编码为：

```
Tuple a b
```

接下来要注意的是这些有用的函数，它们形成了函数的同构：

```
bimap identity identity = identity      [Identity]
bimap (g1 <<< f1) (g2 <<< f2) =
    bimap g1 g2 <<< bimap f1 f2      [Composition]
```

它们与 `Functor` 定律类似：

```
map identity = identity      [Identity]
map (g <<< f) = map g <<< map f      [Composition]
```

看看你是否能看出它们之间的相似之处。

## 12.19. 从视角看 Functors

正常的函数应用如下所示：

```
f $ x ①
```

① 这里我们冗余地使用了 `$` 运算符。

我们可以取 Pure 值并将其应用于期望这些 Pure 值的函数。我们在查看 `$` 运算符的类型签名时可以看到这一点：

```
apply :: ∀ a b. (a -> b) -> a -> b ①

infixr 0 apply as $
```

① 所有值都是 Pure 的。

用隐含的括号重写 `apply`：

```
apply :: ∀ a b. (a -> b) -> (a -> b)
```

我们可以看到这只是针对函数的恒等函数，即接收 `a -> b` 并返回 `a -> b`。

表面上，这似乎没用，而且确实如此。`apply` 很少被直接调用。它存在的原因是为了让我们能够使用其运算符 `$` 的括号化好处。

但对于 `map` 来说，它不仅仅是便利：

```
map :: ∀ a b. (a -> b) -> f a -> f b
```

记住这是类方法，`f` 在 `class` 定义中定义。这就是为什么我们不需要在 `∀` 之后加上 `f`。

没有 `map`，我们就没有办法将 Context 中的值应用到接受 Pure 值的函数上。想象一下我们在 `Maybe` 中有一个 Pure 值：

```
Just 10
```

让我们也想象一下我们是从一个可能失败的函数中获得这个值的。而且，当它不失败时，我们希望将该函数的结果除以 2。

以下代码将无法工作：

```
div2 :: Int -> Int
div2 = (_ / 2)

x :: Maybe Int
x = div2 $ Just 10 — COMPILER ERROR
```

编译器抱怨它无法将 `Maybe Int` 与 `Int` 匹配。

这就是 `Functor` 类中的 `map` 发挥作用的地方。对我们的代码做一个很小的修改，我们就得到了可工作的程序：

```
div2 :: Int -> Int
div2 = (_ / 2)

x :: Maybe Int
x = div2 <$> Just 10
```

记住 `<$>` 是 `map` 的运算符。

所以 Functors 让我们可以将上下文值，即 Context 中的值，例如 `Just 10`，应用到期望 Pure 值的函数上。

我们在从未需要此功能的情况下编写了大量函数式代码。你可以想象，一切都进展顺利，使用简单的函数，直到人们开始创建这些复杂上下文的那一刻。一旦发生这种情况，就希望使用他们手头的众多函数来操作这些新的上下文值。

上下文只是我们称之为 `Functor` 的东西。`map` 函数允许我们访问封装的值或值并在原地操作它们：

```
map :: ∀ a b. (a -> b) -> f a -> f b
```

并且从同一枚硬币的另一面来看，`map` 接收并返回 Pure 值的函数，并将它们 *提升* 为接收并返回上下文值的函数：

```
map :: ∀ a b. (a -> b) -> (f a -> f b) ①
```

① 这里唯一的区别是我们添加了隐含的括号以强调提升效果。

有了这种视角，我们看到 `map` 接收期望 Pure 值的函数并将其转换为处理上下文值的函数。

# 第 13 章. 编码 Functors

在我们继续学习更高级的 `Functors` 之前，我们将首先为我们已经熟悉的一些类型编写 `Functor` 实例。然后我们将创建自己的类型并使它们成为 `Functors`。

返回你一直在编码的项目并创建一个名为 `Ch13.purs` 的文件并添加以下内容：

```
module Ch13 where

import Prelude (Unit)
import Effect (Effect)
import Effect.Console (log)

test :: Effect Unit
test = do
  log "placeholder"
```

① 只是提醒一下，我们通常会直接包含整个 `Prelude`，但由于我们将覆盖 `Prelude` 中的内容，我们将非常具体地只包含我们需要的东西。

② 我们很快就会删除它。它只是为了让编译器保持快乐而存在。

接下来，修改你的 `Main` 模块以导入 `Ch13` 并调用其 `test` 函数：

```
module Main where

import Prelude
import Effect (Effect)
import Ch13 as Ch13

main :: Effect Unit
main = Ch13.test
```

## 13.1. 为 `Maybe` 编写 `Functor` 实例

`Maybe` 是我们学过的第一个类型之一。`Maybe` 在非失败情况下具有上下文值，即 `Just`。

我们希望能够在保持上下文完整的同时操作这个值，因此我们将通过使 `Maybe` 成为 `Functor` 来实现这一点。为此，我们只需要为 `Maybe` 创建一个遵守定律的 `Functor` 实例。

从我们的测试代码中删除占位符行并替换为以下行：

```
log $ show $ (_ / 2) <$> Just 10 ①
log $ show $ (_ / 2) <$> Nothing ②
```

① 打印 `(Just 5)`。

② 打印 `Nothing`。

此外，编辑 `Prelude` 导入以包含我们需要执行这些测试的更多函数：

```
import Prelude (Unit, show, discard, ($), (/), (<$>)) ①
```

① 记住 `discard` 用于 `do` 语法（更多内容将在我们学习 Monads 时介绍）。

现在首先编写 `Maybe` 的类型。我们已经做过很多次了，所以这应该很容易。

接下来，编写 `Functor` 类型类定义。尽量不要作弊，看看你记住了多少。在这个阶段，查阅部分内容是很常见的。

最后，为 `Maybe` 编写 `Functor` 实例。这也应该很容易，因为你只需要 `Maybe` 的类型定义和 `Functor` 的类型类定义。

在继续之前先试试。

## 13.2. `Maybe` 的 `Functor` 实例代码

首先让我们编写 `Maybe` 类型定义：

```
data Maybe a = Nothing | Just a ①
```

① `Nothing` 定义在前面，以便它在排序时排在 `Just` 之前。

接下来，让我们一行一行地编写 `Functor` 类型类：

```
class Functor f where
```

这里 `f` 是 `Functor` 类型。在我们的例子中，它代表 `Maybe`。

现在让我们添加 `Functor` 方法：

```
class Functor f where
  map :: ∀ a b. (a -> b) => f a -> f b
```

① 注意 `f` 不是 `∀` 的一部分。那是因为它已经作为类型类定义的一部分定义了，这意味着 `∀ f`。

`map` 函数接收 Pure 值的函数 `a -> b` 和一个上下文值，并将该函数应用于该值并以相同的上下文返回结果。相同的上下文要求由恒等 `Functor` 定律决定。

最后，我们将一行一行地为 `Maybe` 编写 `Functor` 实例：

```
instance functorMaybe :: Functor Maybe where
```

我们使用了规范的命名 `functorMaybe`。此外，我们没有在 `Maybe` 之后指定 `a`。你还记得为什么吗？

这是因为 `f` 的 Kind 是 `Type -> Type`，`Maybe` 的也是。既然 `Maybe` 接收一个 `Type` 并返回一个 `Type`，它就与类型类中 `f` 的使用方式匹配。所以我们直接用 `Maybe` 替换 `f`。提示：这对于 Kind 为 `Type -> Type -> Type` 的 `Either` 不会成立。

接下来我们为 `Nothing` 情况编写 `map` 方法：

```
instance functorMaybe :: Functor Maybe where
  map _ Nothing = Nothing
```

① 第一个参数未使用。

如果我们有 `Nothing`，那么我们就没有值可以应用函数。唯一能做的就是返回 `Nothing`。

最后，我们编写 `Just` 情况：

```
instance functorMaybe :: Functor Maybe where
  map _ Nothing = Nothing
  map f (Just x) = Just $ f x
```

① 我们解包 `Just` 以暴露其值，然后将函数应用于该值并立即将其重新包装在 `Just` 中。

现在，在这一点上，你的代码有以下编译器错误：

```
No type class instance was found for

    Data.Show.Show (Maybe Int)
```

那是因为我们没有让 `Maybe` 可显示。停止在这里并为我们的 `Maybe` 创建一个 `Show` 实例。我们以前做过，这将是对该过程的良好复习。尽量不要作弊并查看你之前做过的事情，即除非你尝试过并完全卡住。

为 `Maybe` 添加 `Show` 实例的第一步是为 `Maybe` 派生一个 `Generic` 实例，以便我们可以利用 `genericShow`。

```
import Data.Generic.Rep (class Generic) ①

data Maybe a = Nothing | Just a
derive instance genericMaybe :: Generic (Maybe a) _ ②
```

① 添加 `Generic` 类型类的导入。

② 派生 `Generic`，第二个参数留空，即 `_`。

然后我们将 `Maybe` 的 `show` 委托给 `genericShow`：

```
import Prelude (class Show, Unit, show, discard, ($), (/), (<$>)) ①

import Data.Show.Generic (genericShow) ②

data Maybe a = Nothing | Just a
derive instance genericMaybe :: Generic (Maybe a) _

instance showMaybe :: Show (Maybe a) where ③
    show = genericShow
```

① 添加来自 `Prelude` 的 `Show` 类型类。

② 添加 `genericShow` 的导入。

③ 为 `Maybe` 添加 `Show` 实例，委托给 `genericShow`（因为 `Maybe` 有 `Generic` 实例）。

现在我们有编译器错误！！

为什么？

让我们仔细查看错误：
