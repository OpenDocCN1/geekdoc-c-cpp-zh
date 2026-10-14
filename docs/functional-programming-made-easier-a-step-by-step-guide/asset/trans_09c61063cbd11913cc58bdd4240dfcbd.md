

![](img/8c0e9b687c62642e828ccb5481e11313_422_0.png)

在 PureScript 中，我们可以证明组合是结合的：

```text
compose :: ∀ a b c. (b -> c) -> (a -> b) -> (a -> c)
compose g f x = g (f x)  -- ①
```

① 这个等式将在下面的证明中使用。

```text
h ∘ (g ∘ f)               = (h ∘ g) ∘ f                 -- Given (Math)
compose h (compose g f) x = compose (compose h g) f x -- Given (PureScript)
h ((compose g f) x)      = compose (compose h g) f x -- Subst left using ①
h ((compose g f) x)      = (compose h g) (f x)      -- Subst right using ①
h (compose g f x)        = (compose h g) (f x)      -- Remove Parentheses
h (g (f x))              = (compose h g) (f x)      -- Subst left using ①
h (g (f x))              = h (g (f x))              -- Subst right using ①
```

我们现在已经展示了如何将类型作为对象、函数作为态射构成一个守法的范畴。并且在对范畴论这个非常简短的介绍之后，我希望你能看出函数式语言设计者是如何受到这个相对较新的数学领域（约 1945 年）的影响的。

## 12.10. Hask 中的具体示例

让我们从 Show 方法 show 开始，在 Hask 中看一些示例：

```text
class Show a where
  show :: a -> String
```

我们可以将其图示表示为：

![](img/8c0e9b687c62642e828ccb5481e11313_423_0.png)

对于 Show 的 Int 实例：

```text
instance showInt :: Show Int where
    show = showIntImpl

foreign import showIntImpl :: Int -> String  -- ①
```

① Javascript 中的实际实现。

我们可以将其表示为：

![](img/8c0e9b687c62642e828ccb5481e11313_424_0.png)

希望，这些简单的例子基于我们迄今为止所做的内容是有意义的。但这些例子似乎过于简单了。多个参数的函数呢？

```text
f :: Int -> Int -> String
```

记住所有函数都是柯里的。并且可以将此函数重写为其非柯里形式：

```text
f :: Tuple Int Int -> String  -- ①
```

① 从技术上讲，我们已经将此函数 *非柯里化* 了。（稍后会详细介绍）

现在它只接受一个参数，我们可以在范畴 Hask 中绘制它：

![](img/8c0e9b687c62642e828ccb5481e11313_425_0.png)

希望，你可以想象我们如何用 3 个参数的函数来做这件事：

```text
g :: Int -> Boolean -> String -> String

g' :: Tuple Int (Tuple Boolean String) -> String
```

等等。

在这一简短介绍之后，我们现在应该能够看到函子在范畴论中是如何工作的，并将其与编程中的函子进行比较。

## 12.11. 范畴论中的函子

到目前为止，我们只看过一个范畴以及在该范畴内将对象变形为同一范畴中其他对象的方式。这就是 PureScript 中的函数所做的：

```text
f :: ∀ a b. a -> b  -- ①
```

① 将类型映射到类型。

而态射是在对象之间的映射，函子是在范畴之间的映射。而在 PureScript 中，正如我们所见，函子只是函数，即 map。

但在编程中，我们只有一个范畴，因为我们的函数只能将类型映射到类型。映射回同一范畴的函子被称为 *EndoFunctors*。因此 PureScript 中的所有 *函子* 实际上都是 EndoFunctors，但大家都只是称之为 *函子*。

函子还有另一个非常重要的要求。

> 函子保持范畴结构。在抽象代数中，保持群等代数结构的函数称为 *同态*（*Homo* 意为 *相同*，*morph* 意为 *形状*）。这里函子就像同态，因为它们也保持范畴结构。

如果对象 a 有一个到对象 b 的态射，那么函子必须在将它们映射到新范畴时保持该态射。它也不能在映射时丢弃任何对象或态射，也不能创建原始范畴中不存在的新对象或态射：

![](img/8c0e9b687c62642e828ccb5481e11313_426_0.png)

这里函子 F 将对象和态射从范畴 C 映射到 D。

在此图中，F 将 a 映射到 F a 并将 b 映射到 F b，即映射所有对象（未显示所有映射）。

它还显示 F 将 f 映射到 F f，即映射所有态射（未显示所有映射）。

当我们用隐含的括号来看 PureScript 中的 map 时：

```text
class Functor f where
  map :: ∀ a b. (a -> b) -> (f a -> f b)  -- ①

infixl 4 map as <$>
```

① 我们添加了隐含的括号。

我们可以看出态射的映射，即 a -> b 被映射到 f a -> f b。

但在 PureScript 中，a 到 f a 和 b 到 f b 的映射在哪里。对于这一点，我们必须等待 Applicative 函子。但这里有一个预览：

```text
class Apply f <= Applicative f where  -- ①
  pure :: ∀ a. a -> f a
```

① Functor 是 Apply 的超类，这意味着 Applicative 也是一个函子。因此，Applicative 具有 map 和 pure，这涵盖了范畴函子对对象（pure）和态射（map）的映射。

我们很快就会遇到 Applicative 函子，但就目前而言，还有很多关于函子需要学习和做的事。

## 12.12. 函子定律

在 PureScript 中无法强制执行函子定律。验证其实现是否遵守这些定律的责任在于类型类的作者：

```text
map identity = identity          [Identity]
map (g <<< f) = map g <<< map f   [Composition]
```

简而言之，这些定律规定函子必须保持恒等和组合。

恒等定律说，如果我们映射恒等函数，那么它等价于仅在函子上调用恒等。请注意，这一定律意味着 map 永不能改变函子的结构。因此 Just 永不能变成 Nothing，Left 不能改变为 Right。换句话说，映射恒等会保持函子不变。

从范畴的角度来看，函子将范畴 C 中的恒等态射映射到范畴 D 中的恒等态射：

![](img/8c0e9b687c62642e828ccb5481e11313_428_0.png)

**组合** 定律说，映射 2 个函数的组合等价于分别映射它们然后组合结果。我们可以用范畴在图示上看到这一点：

![](img/8c0e9b687c62642e828ccb5481e11313_428_1.png)

将 g ∘ f 映射到 F (g ∘ f) 等价于将 f 映射到 F f 并将 g 映射到 F g，然后将它们组合得到 F g ∘ F f。这是有意义的，因为函子必须保持范畴结构和规则，其中之一就是态射可组合。

暂时离开范畴论，回到编程，我们可以看到从 **恒等** 定律，映射恒等函数（或态射）没有效果。

让我们用 `Maybe` 看看这意味着什么：

```text
instance functorMaybe :: Functor Maybe where
  map _ Nothing  = Nothing
  map f (Just x) = Just $ f x
```

这里 `Nothings` 保持为 `Nothings`，`Justs` 保持为 `Justs`。如果不是这样，我们就会破坏 `Identity` 定律。

`Either` 的 `Lefts` 和 `Rights` 也是如此：

```text
instance functorEither :: Functor (Either a) where
  map _ (Left x)  = Left x
  map f (Right y) = Right $ f y
```

## 12.13. 验证 `Maybe` 的函子定律

让我们从以下开始：

```text
data Maybe a = Nothing | Just a

instance functorMaybe :: Functor Maybe where
  map _ Nothing  = Nothing  -- ①
  map f (Just x) = Just $ f x  -- ②
```

① 这个等式将在下面的证明中使用。

② 这个等式将在下面的证明中使用。

让我们验证定律。我们的方法是先从定律开始，然后使用我们的实现，减少等式的左边然后右边。如果结果相同，则它们显然相等。

首先，`Nothing` 的恒等：

```text
map identity Nothing  = identity Nothing       -- Identity Law
Nothing              = identity Nothing       -- Subst left using ①
Nothing              = Nothing                -- Function Application
```

接下来，`Just`：

```text
map identity (Just x) = identity (Just x)    -- Identity Law
Just (identity x)    = identity (Just x)    -- Subst left using ②
Just x               = identity (Just x)    -- Function Application
Just x               = Just x              -- Function Application
```

接下来，我们将验证 `Nothing` 的组合定律：

```text
map (g <<< f) Nothing = (map g <<< map f) Nothing -- Composition Law
Nothing               = (map g <<< map f) Nothing -- Subst left using ①
Nothing               = map g (map f Nothing)     -- Function Composition
Nothing               = map g Nothing             -- Subst right using ①
Nothing               = Nothing                  -- Subst right using ①
```

最后，使用 `Just`：

```text
map (g <<< f) (Just x) = (map g <<< map f) (Just x) -- Composition Law
Just ((g <<< f) x)      = (map g <<< map f) (Just x) -- Subst left using ②
Just (g (f x))          = (map g <<< map f) (Just x) -- Function Composition
Just (g (f x))          = map g (map f (Just x))     -- Function Composition
Just (g (f x))          = map g (Just (f x))         -- Subst right using ②
Just (g (f x))          = Just (g (f x))             -- Subst right using ②
```

## 12.14. `Either` 的函子实例

让我们在记住我们对 `Left` 进行短路的情况下，遵循我们对 `Maybe` 所做的，为 `Either` 编写 `Functor` 实例：

```text
data Either a b = Left a | Right b

instance functorEither :: Functor Either where -- COMPILE ERROR!!
  map _ (Left x)  = Left x  -- ①
  map f (Right y) = Right $ f y  -- ②
```

- ① 短路。
- ② 将 `f` 应用于上下文中的值，即 `y`。

让我们看看编译器错误：

