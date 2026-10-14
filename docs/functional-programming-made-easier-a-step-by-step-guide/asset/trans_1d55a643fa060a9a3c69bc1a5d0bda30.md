

实例 **必须** 为 *以下两者之一*：

+   1. 在与类型类 **相同** 的模块中定义。
+   2. 在与类型 **相同** 的模块中定义。

以下是这两种情况的图示：

![](img/8c0e9b687c62642e828ccb5481e11313_264_0.png)

在 **选项 A** 中，我们在与类型类 **相同** 的模块中定义了 `Person’s` 实例。

**选项 B** 在其类型的 **相同** 模块中定义了 `Person’s` 实例，而类型类则定义在不同的模块中。

如果未遵循这两个要求中的任何一个，则我们就会得到一个 **孤立实例**。

乍一看，这一限制似乎很奇怪。让我们看看替代方案，看看问题出在哪里：

![](img/8c0e9b687c62642e828ccb5481e11313_264_1.png)

这里 **模块 3** 定义了 `Person’s HasAddress` 实例。但 **模块 4** 也这么做了。让我们想象 **模块 3** 和 **模块 4** 彼此完全独立，即两者互不导入。

现在我们将拥有 `Person` 的两个可能不同的 `HasAddress` 实现。如果我们的一半模块导入模块 3，而另一半导入模块 4，我们可能会陷入困境。

我们需要一个权威定义，而真正有权威的只有两个地方，即定义类型类的模块（模块 1）和定义类型的模块（模块 2）。

这看起来可能很局限，坦白说，有时确实如此。甚至在 Haskell 中，有办法告诉编译器允许在特定模块中使用孤立实例，即本质上将特定模块定义为权威。然而，这并非没有风险。如果过度使用，就可能导致同一实例的两个不同的定义。

因此在 PureScript 中，这是被禁止的，且没有可覆盖的选项。但当你发现自己遇到了孤立实例时会发生什么？让我们看一个这样的例子：

```
import Combine.Class (class Combine) ①

-- ORPHANED INSTANCE!!
instance combineInt :: Combine Int where ②
  combine = (+)
```

① 类型类定义在此模块之外。

② `Int` 类型定义在 PureScript 模块 `Prim` 中，因此类型也定义在此模块之外。

这是一个典型的孤立实例案例。你既不控制类型类也不控制类型。但你希望让该类型具有额外的功能。

可以怎么做？

我们需要控制类型类或类型中的一个。如果你创建另一个类型类，那么使用其他类型类的所有代码都将无法与你的类型类一起工作。但如果我们创建自己的类型，那么我们就是该类型的权威声音。

我们如何做到这一点？当然是用 newtype：

```
import Combine.Class (class Combine)

newtype AddInt = AddInt Int ①

instance combineAddInt :: Combine AddInt where ①
  combine (AddInt x) (AddInt y) = AddInt (x + y)
```

① 现在我们的 `AddInt` 类型与我们为 `AddInt` 定义的 `Combine` 实例位于同一模块中。不再有孤立实例。

这种解决方案并非免费。我们不能像使用 `Int` 一样使用 `AddInt`：

```
x :: AddInt
x = AddInt 10

y :: Int
y = 11

z :: Int
z = x + y --- COMPILER ERROR!! ①
```

① 这将导致类型不匹配错误。x 是 Int，y 是 AddInt，而 + 要求两个类型相同。

我们也不能添加两个不同的 AddInt：

```
z :: AddInt
z = (AddInt 7) + (AddInt 3) --- COMPILER ERROR!!
```

如果你尝试，就会得到以下编译器错误：

![](img/8c0e9b687c62642e828ccb5481e11313_266_0.png)

错误中最相关的部分是：

```
No Typeclass instance was found for

Data.Semiring.Semiring AddInt
```

这令人困惑，直到我们进入抽象代数部分学习一点关于半环的知识之前，它仍会令人困惑。现在让我们接受我们缺少一个实例来添加两个 AddInt。

对于好奇的人，这里是可以让我们对 AddInt 进行加法和乘法运算的实例，这两个运算是半环的运算：

```
instance semiringAddInt :: Semiring AddInt where
  add (AddInt x) (AddInt y) = AddInt (x + y)
  zero = AddInt 0
  mul (AddInt x) (AddInt y) = AddInt (x * y)
  one = AddInt 1
```

虽然 newtype 让我们绕过了孤立实例问题，但它并非没有缺点。很多时候我们需要为我们的 newtype 实现底层实例，使用 derive newtype：

```
import Data.Newtype (class Newtype)

newtype AddInt = AddInt Int
derive instance newtypeAddInt :: Newtype AddInt _ ①
derive newtype instance semiringAddInt :: Semiring AddInt ②
derive newtype instance ringAddInt :: Ring AddInt ③
derive newtype instance commutativeRingAddInt :: CommutativeRing AddInt ④
derive newtype instance euclideanRingAddInt :: EuclideanRing AddInt ④
```

① 我们必须先为我们的类型派生 Newtype 实例，然后才能利用 derive newtype。

② 现在，虽然我们还不了解半环是什么，但我们仍然可以利用 `Int` 的底层实现。这个定义让我们可以对 AddInt 进行加法和乘法。

③ 这让我们可以对 AddInt 进行减法。

④ 这些让我们可以对 AddInt 进行除法。CommutativeRing 是 EuclideanRing 的超类，因此我们必须同时实现两者，因为 EuclideanRing 提供了除法操作。

幸运的是，derive newtype 大大减少了我们的工作量。不幸的是，我们在使用 AddInt 的不同情况下，可能会发现自己不断向此列表中添加内容。

## 6.11. 实例依赖

实例也可以受约束，即实例依赖于一个或多个实例：

```
data Maybe = Nothing | Just a

instance showMaybe :: Show a => Show (Maybe a) where
  show Nothing = "Nothing"
  show (Just x) = "(Just " <> show x <> ")" ①
```

① 调用 `show x` 的原因在于 `x` 的类型是 `a`，因此 `a` 必须是 `Show` 的实例。

该实例依赖于 `Show`，即只要我们可以显示 `a`，我们就可以显示 `Maybe a`。

这里是另一个例子：

```
data Either a b = Left a | Right b

instance showEither :: (Show a, Show b) => Show (Either a b) where ①
  show (Left x)  = "(Left " <> show x <> ")" ②
  show (Right y) = "(Right " <> show y <> ")" ③
```

+   ① 我们使用括号和逗号列出多个约束。
+   ② 调用 `show x` 的原因在于 `a` 必须是 `Show` 的实例。
+   ③ 调用 `show y` 的原因在于 `b` 必须是 `Show` 的实例。

你可能已经注意到，在实例定义中，我们不使用 ∀。那是因为它是隐含的。

## 6.12. 多参数类型类

到目前为止，我们只看到具有单个类型参数的类型类，通常是 `a`，但也可以有多个：

```
import Data.List (List) ①
import Data.List as List ②
import Data.String.CodeUnits as String ③

class Decapitate collection element where ④
  decapitate :: collection -> Maybe {head :: element, tail :: collection}

instance decapitateList :: Decapitate (List a) a where ⑤
  decapitate = List.uncons

instance decapitateString :: Decapitate String Char where ⑥
  decapitate = String.uncons
```

+   ① 我们只导入 `List` 类型，这样就不需要写 `List.List`。
+   ② 然后我们将 `Data.List` 中的所有内容导入到命名空间 `List` 中。这意味着我们必须为此模块的所有导入加上 `List.` 前缀，例如 `List.uncons`。
+   ③ 这是非 Unicode 的 `String` 模块。
+   ④ 用于从 `collection` 中移除头部 `element` 的类。

+   ⑤ `List` 实例，我们利用 `List` 的 `uncons` 函数。`a` 是我们 `List` 的元素。

+   ⑥ `String` 实例，我们利用 `String` 的 `uncons` 函数。`Char` 是我们 `String` 的元素。

`collection` 和 `element` 是 `Decapitate` 类型类的类型参数。`collection` 是集合的类型，`element` 是集合中每个元素的类型。

`decapitate` 删除 `collection` 的头部，并以 `Record` 的形式返回它和剩余元素。由于这可能失败，因此返回 `Maybe`。

`List` 实例在第二个类型参数中被称为 **多态**，即类型 `a`。记住 **Poly** 表示 **多**，**morph** 表示 **形状**：

```
instance decapitateList :: Decapitate (List a) a where
  decapitate = List.uncons
```

第二个类型参数 `a` 可以采用多种形状，即 `a` 可以与多种类型统一。

相比之下，`String` 实例在第二个类型参数中是 **单态** 的，即 `Char`。记住 **Mono** 表示 **一**，**morph** 表示 **形状**：

```
instance decapitateString :: Decapitate String Char where
  decapitate = String.uncons
```

第二个参数 `Char` 是一个单一、固定的类型。

## 6.13. 函数依赖

回到我们对 `Decapitate` 的 `String` 实例：

```
import Data.String.CodeUnits as String

instance decapitateString :: Decapitate String Char where
  decapitate = String.uncons
```

这是非 Unicode 版本的 `String`。但如果我们也想支持 Unicode 呢：

