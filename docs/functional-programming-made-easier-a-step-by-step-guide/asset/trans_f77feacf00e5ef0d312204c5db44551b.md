
# 14.10. 同态

*Homo* 意为 *相同*，*morph* 意为 *形态*。而 *同态* 是保持形态或结构的态射。

函子（Functor）是同态，因为它们保持了范畴结构。但“保持范畴结构”是什么意思？实际上问题在于“范畴结构”指的是什么。

回顾一下，范畴包含对象，以及这些对象之间可能存在零个或多个态射。

另外，请记住，每个对象至少有一个称为恒等态射的*自同态*（*Endo* 意为*内部*）。

范畴还有另一个要素：复合。在映射到另一个范畴后，这一点也必须得到保持。

因此，“保持范畴结构”意味着函子必须将所有对象和态射映射到新范畴，同时保持这些对象之间相同的态射。

例如，如果源范畴中对象 a 和 b 之间存在一个态射，那么函子必须保持目标范畴中它们对应对象之间的这个态射。

## 14.11. 自然变换

自然变换就是函子之间的态射。它们也是同态。

符号 η 用来表示自然变换，因为它看起来有点像字母 N，我猜。实际上，它是希腊字母中被称为 Eta 的 H 的小写形式。

让我们用下面的图来帮助理解自然变换：

![](img/8c0e9b687c62642e828ccb5481e11313_491_0.png)

让我们一次只看这个图的一部分。

在左侧，我们有范畴 C。态射 f 从 a 映射到 b。

在右侧，我们有范畴 D。函子 F 将 a、b 和 f 从范畴 C 映射到范畴 D。

我们还有函子 G，它同样进行映射。

现在，让我们在函子 F 和 G 之间添加态射：

![](img/8c0e9b687c62642e828ccb5481e11313_492_0.png)

当且仅当以下条件成立时，函子之间的这些态射才是自然变换：

- 1. 对于范畴 C 中的每个对象 x，态射 η x : F x → G x 在范畴 D 中都存在。
- 2. 对于范畴 C 中的每个态射 f : a → b，在范畴 D 中有 η b ∘ F f = G f ∘ η a。

注意，条件 #1 处理的是从 C 到 D 的对象映射，条件 #2 处理的是态射映射。这并不奇怪，因为函子两者都映射。

这里还要注意一点：上面范畴 D 中的图是交换的。

> 交换图是这样一种图：所有具有相同起点和终点的有向路径都会导向相同的结果。

需要注意的是，上面的图是针对协变函子的，在 PureScript 中它们被称为 Functor。

如果我们想要表示逆变函子，就需要反转图中所有的垂直箭头。逆变函子的自然变换条件如下：

- 1. 对于范畴 C 中的每个对象 x，态射 η x : F x → G x 在范畴 D 中都存在。与协变情况相同。
- 2. 对于范畴 C 中的每个态射 f : b → a，在范畴 D 中有 η a ∘ F f = G f ∘ η b。a 和 b 交换了位置。

让我们看一个现实世界的例子：从 Maybe 到 Either Unit 的同态：

```
hom :: Maybe ~> Either Unit
 hom Nothing = Left unit
 hom (Just x) = Right x
```

① ~> 是 PureScript 中表示自然变换的符号。

我们本可以同样轻松地将类型签名写成：

```
hom :: ∀ a. Maybe a -> Either Unit a
```

① 这等价于 η a : F a -> G a，其中 Maybe 是 F，Either Unit 是 G。

我们不必证明自然变换条件 #1 成立，因为我们的函数能编译，而且我们的类型签名基本上就是该条件。

对于协变情况的条件 #2：

```
f : a -> b
hom ∘ (mMap f) = (eMap f) ∘ hom
```

① mMap 是 Maybe 的 map，即函子 F。

② eMap 是 Either Unit 的 map，即函子 G。

从第二个等式的左边开始，如果我们先使用 Maybe 的 map（即 mMap f），再转换为 Either 的 hom，这等同于先转换为 Either 的 hom，再使用 Either 的 map（即 eMap f）进行映射。

我们可以确信这个等式成立，这要归功于函子定律。

如果你仍然有疑问，可以看看 Maybe 和 Either a（在我们的例子中 a 是 Unit）的 Functor 实现：

```
instance functorMaybe :: Functor Maybe where
  map _ Nothing = Nothing
  map f (Just x) = Just $ f x

instance functorEither :: Functor (Either a) where
  map _ (Left x) = Left x
  map f (Right y) = Right $ f y
```

你能看出相似之处吗？

如果你还是不相信，直接做代数代入即可。这里再次给出 hom：

```
```haskell
hom :: Maybe ~> Either Unit
hom Nothing  = Left unit ⑤
hom (Just x) = Right x ⑥
```
```

首先，Nothing 的情况：

```
```text
(hom ∘ (mMap f)) Nothing = ((eMap f) ∘ hom) Nothing        — Given
hom Nothing = ((eMap f) ∘ hom) Nothing                       — Substitute into ❶
Left unit = ((eMap f) ∘ hom) Nothing                         — Apply on left side ⑤
Left unit = (eMap f) (Left unit)                              — Apply on right side ⑤
Left unit = Left unit                                         — Substitute into ❸
```
```

接下来是 Just x 的情况：

```
```text
(hom ∘ (mMap f)) (Just x) = ((eMap f) ∘ hom) (Just x)       — Given
hom (Just $ f x) = ((eMap f) ∘ hom) (Just x)                — Substitute into ❷
Right $ f x = ((eMap f) ∘ hom) (Just x)                     — Apply on left side ⑥
Right $ f x = (eMap f) (Right x)                             — Apply on right side ⑥
Right $ f x = Right $ f x                                    — Substitute into ❹
```
```

## 14.12. 幺半群同态

数学中的函数将元素从输入集合（称为定义域 Domain）映射到输出集合（称为陪域 Codomain）：

![](img/8c0e9b687c62642e828ccb5481e11313_495_0.png)

幺半群是带二元运算符并满足某些限制的集合：

- 1. 二元运算符必须在集合上是封闭的。原群（Magma）
- 2. 二元运算符必须是可结合的。半群（Semigroup）
- 3. 集合必须有一个单位元。幺半群（Monoid）

可能存在一个函数，其输入集合（定义域）来自幺半群 M。但无法保证输出集合（陪域）也是幺半群。这取决于函数本身。

这里我们使用的是恒等函数的等价形式：

```
idHom :: ∀ m. Monoid m => m -> m
idHom x = x
```

显然，这保持了幺半群结构，也就是说，这个函数对输入没有任何影响，因此其结果仍然是幺半群。

下面是另一个例子，它只是 const mempty 的等价形式：

```
constHom :: ∀ m. Monoid m => m -> m
constHom _ = mempty
```

这同样保持了幺半群结构，因为它是一个只包含 mempty 的集合，而 mempty 满足幺半群的所有要求：

```
mempty <> mempty = mempty                 Closed      Magma
(mempty <> mempty) <> mempty = 
    mempty <> (mempty <> mempty)   Associative  Semigroup
mempty <> mempty = mempty                Identity     Monoid
```

我们还可以编写一个破坏该结构的函数：

```
always123 :: String -> String
always123 _ = "123"
```

这个函数将 String 幺半群中的每个 String 映射为 "123"。得到的集合（陪域）不是幺半群。事实上，它甚至不是原群（Magma）：

```
"123" <> "123" = "123123"          NOT CLOSED
```

但到目前为止，我们只看到了一些刻意构造的简单例子。然而，有一个我们都用过很多次的常见函数是幺半群同态，那就是 length，即字符串长度函数。它将 String 映射为 Int。

但在验证 length 是幺半群同态之前，最好先给出幺半群同态的形式定义：

一个函数 h : M -> N，将幺半群 M 中的元素映射到幺半群 N，如果满足以下条件，则它是一个同态：

```
h (m1 • m2) = h(m1) * h(m2)
```

换句话说，先在 M 中组合 m1 和 m2，再映射到 N，等于先将 m1 和 m2 映射到 N，再在 N 中组合。

注意，在 M 中组合使用的是 M 的二元运算符 •，而在 N 中组合使用的是 N 的二元运算符 *。在 length 这个同态中，这两个二元运算符不同，但在使用 idHom 或 constHom 时，它们是相同的。

下面我们来看看它的实际应用：

