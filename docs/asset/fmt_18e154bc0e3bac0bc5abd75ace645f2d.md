
`instance applyWriterT`

```haskell
:: (Semigroup w, Bind m) => Apply (WriterT w m) where
```

```haskell
apply (WriterT mf) (WriterT mx) = do
  Tuple f w1 <- mf -- COMPILER ERROR!
  Tuple x w2 <- mx
  pure $ Tuple (f x) (w1 <> w2)
```

+   1. 这里有一个语法说明：对于类型类实例，我们需要在括号内用逗号分隔来添加多个约束。

```
No type class instance was found for
runW
runW        Control.Applicative.Applicative m2
inst
  ma while checking that type forall a f. Applicative
      is at least as general as type t0 -> t1
inst while checking that expression pure
  ap   has type t0 -> t1
  ap in value declaration applyWriterT
    where m2 is a rigid type variable
pure $ Tuple (f x) (w1 <> w2)
```

由于我们在使用 `pure`，它要求 `m` 有 `Applicative` 约束。但我们已经有了 `Bind` 约束。如果我们将这两个约束组合起来，就得到一个 `Monad` 约束，因为它们都是 `Monad` 的超类。

让我们将 `Bind` 约束改为 `Monad` 约束：

```haskell
instance applyWriterT
  :: (Semigroup w, Monad m) => Apply (WriterT w m) where ①
apply (WriterT mf) (WriterT mx) = WriterT do
  Tuple f w1 <- mf
  Tuple x w2 <- mx
  pure $ Tuple (f x) (w1 <> w2)
```

① 将 `Bind` 约束改为 `Monad` 约束。

回顾我们刚才所做的工作，可以看出我们始终确保在底层 `Monad` 中操作。这似乎是一个反复出现的主题。

你可能会问，我们是否可以跳过这些编写，直接使用 `ap` 来“作弊”，因为 `WriterT` 最终会是一个 `Monad`。答案是肯定的，但那样我们就学不到这么多东西了。

接下来，我们将编写 `Applicative` 实例：

```haskell
instance applicativeWriterT
  :: (Semigroup w, Monad m) => Applicative (WriterT w m) where ①
```

① 我们主动在这里添加了与 `Apply` 相同的约束，因为它是我们的超类。

接下来，是等号左侧的代码：

```haskell
instance applicativeWriterT
  :: (Semigroup w, Monad m) => Applicative (WriterT w m) where
  pure x = ???
```

现在我们需要将 `Pure` 值包装两次，首先在底层 `Monad` 中使用其 `pure`，然后在 `WriterT` 中：

```haskell
instance applicativeWriterT
  :: (Semigroup w, Monad m) => Applicative (WriterT w m) where
  pure = WriterT <<< pure -- COMPILER ERROR!! ①
```

① 在改为 Point-free 记法时移除了 `x` 参数。

看起来编译器发现了问题：

![](img/8c0e9b687c62642e828ccb5481e11313_912_0.png)

再次，我忘记了 `Tuple`。为了修复这个问题，我们需要先将 `Pure` 值包装在 `Tuple` 中，然后在底层 `Monad` 中，最后在 `WriterT` 中：

```haskell
instance applicativeWriterT
  :: (Semigroup w, Monad m) => Applicative (WriterT w m) where
  pure x = WriterT $ pure $ Tuple x ??? ①
```

① 放弃了 Point-free 记法。

但我们应该在 `???` 处放入什么作为我们的日志？

我们希望 `Pure` 值的日志为空，就像我们在 `Writer` 中所做的那样。所以我们将使用 `mempty`：

```haskell
instance applicativeWriterT
  :: (Semigroup w, Monad m) => Applicative (WriterT w m) where
  pure x = WriterT $ pure $ Tuple x mempty -- COMPILER ERROR!! ❶
```

❶ 添加了 `mempty`。

而且，编译器仍然不太满意：

![](img/8c0e9b687c62642e828ccb5481e11313_913_0.png)

你能看出我做错了什么吗？

现在我们使用 `mempty`，需要将我们的 `Semigroup` 升级为 `Monoid`：

```haskell
instance applicativeWriterT
  :: (Monoid w, Monad m) => Applicative (WriterT w m) where ❶
  pure x = WriterT $ pure $ Tuple x mempty
```

❶ 将 `Semigroup` 改为 `Monoid`。

最后，我们平息了编译器的异议。

再次，我们必须考虑到底层的 `Monad`。我们可以预期同样的顾虑会在我们编写 `Bind` 实例时再次出现：

```haskell
instance bindWriterT
  :: (Semigroup w, Monad m) => Bind (WriterT w m) where ❶
```

❶ 与 `Apply` 相同的约束，因为它是我们的超类。

接下来，我们将编写左手边：

```haskell
instance bindWriterT :: (Semigroup w, Monad m) => Bind (WriterT w m) where
  bind (WriterT mx) f = ??? ❶ ❷
```

① 我们解构以获取底层的 `Monadic` 值 `mx`。
② 请记住 `f` 是一个 `Monadic` 函数，即它将返回一个 `WriterT`。

此时你会下一步做什么？

说实话，我并不清楚下一步该做什么。但，很明显的是我不知道 `f` 看起来是什么。我不知道它的类型签名。所以最好的办法是为 `bind` 编写专门的类型签名：

```haskell
instance bindWriterT :: (Semigroup w, Monad m) => Bind (WriterT w m) where
  bind :: ∀ a b. WriterT w m a -> (a -> WriterT w m b) -> WriterT w m b ①
  bind (WriterT mx) f = ???
```

① 我们不需要在 `∀` 中添加 `w` 和 `m`，因为它们已在实例定义中定义。事实上，如果我们添加它们，它们将与我们之前的 `w` 和 `m` 独立，这绝对不是我们想要的。

好吧，现在我们做了这个，你能看出下一步该做什么吗？

如果不能，那么也许我们应该写下类型：

```haskell
mx :: m (Tuple a w)
f :: a -> WriterT w m b
```

现在呢？

查看类型，很明显我们不能简单地将 `mx` 传递给 `f`。我们首先需要从中提取一个 `a`，不要忘记它在 `Tuple` 内部：

```haskell
instance bindWriterT :: (Semigroup w, Monad m) => Bind (WriterT w m) where
  bind :: ∀ a b. WriterT w m a -> (a -> WriterT w m b) -> WriterT w m b
  bind (WriterT mx) f = WriterT do ①
    Tuple x w <- mx
    ???
```

① 在 PureScript 中，在 `do` 关键字前不需要加 `$`。但是在 Haskell 中，除非使用名为 `BlockArguments` 的语言扩展，否则情况并非如此。

我们现在有一个可以传递给 `f` 的 `a`，即 `x`，所以让我们这样做：

```haskell
instance bindWriterT :: (Semigroup w, Monad m) => Bind (WriterT w m) where
  bind (WriterT mx) f = WriterT do
    Tuple x w1 <- mx
    Tuple y w2 <- runWriterT $ f x
    pure $ Tuple y $ w1 <> w2 ①
```

① `pure` 将我们的 `Tuple` 包装在底层 `Monad` 中。

而通常，`Monad` 实例非常简单：

```haskell
instance monadWriterT :: (Monoid w, Monad m) => Monad (WriterT w m)
```

注意，我们在这里必须使 `w` 成为 `Monoid`。你知道为什么吗？

因为 `Monad` 是一个 `Bind` 和一个 `Applicative`。`Bind` 对 `w` 只有 `Semigroup`，但 `Applicative` 需要 `Monoid`。由于 `Monoid` 也是 `Semigroup`，我们只需要指定 `Monoid` 即可满足两个要求。

## 20.8. 编码 ReaderT

编码 `ReaderT` 应该与编码 `WriterT` 相似，唯一的区别是 `ReaderT` 包含一个函数而不是一个值。

让我们从类型开始：

```haskell
newtype ReaderT r m a = ReaderT (r -> m a)
```

注意 `ReaderT` 包含一个返回底层 `Monad m` 上下文中值的 `Monadic` 函数。

将其与 `Reader` 对比：

```haskell
newtype Reader r a = Reader (r -> a)
```

接下来，让我们编写 `runReaderT`，因为我们在编写 `WriterT` 时在 `bind` 中可能需要它：

```haskell
runReaderT :: ∀ r m a. ReaderT r m a -> (r -> m a) ①
runReaderT (ReaderT mf) = mf ②
```

① 返回一个返回底层 `Monad`，即 `m` 中值的 `Monadic` 函数。
② 名称 `mf` 提醒我们它是一个 `Monadic` 函数，这意味着它是一个形如 `a -> m b` 的函数或具体地 `r -> m a`。

现在我们可以从其类型签名开始编写 `Functor`：

```haskell
instance functorReaderT :: Functor (ReaderT r m) where
```

现在等于号左手边：

```haskell
instance functorReaderT :: Functor (ReaderT r m) where
  map f (ReaderT mg) = ??? ①
```

① 我们解构 `ReaderT` 以访问底层的函数。名称 `mg` 提醒我们我们有一个 `Monadic` 函数。

接下来，我们使用构造函数式 `Monad` 的模式，这是在 `WriterT` 中没有做到的，因为它是一个值的 `Monad`：

```haskell
instance functorReaderT :: Functor (ReaderT r m) where
  map f (ReaderT mg) = ReaderT \r -> ???
```

现在是时候思考了。我们有一个在底层 `Monad` 中的函数 `mg`，以及我们想要映射的函数 `f`。那么为什么不只是依赖底层 `Monad` 的 `map` 来为我们做脏活呢？

我找不到任何理由它不会起作用：

```haskell
instance functorReaderT :: Functor (ReaderT r m) where
  map f (ReaderT mg) = ReaderT \r -> f <$> mg -- COMPILER ERROR!!
```

而且，当然，编译器持不同意见：

![](img/8c0e9b687c62642e828ccb5481e11313_917_0.png)

看起来我有类型不匹配。但不太清楚我做错了什么。你能看出我错在哪里吗？

当我们得到类型不匹配而无法弄清原因时，写下类型总是好的：

```haskell
f :: a -> b
mg :: r -> m a
```

好吧，现在我可以看到我试图通过简单映射来映射 `mg` 中的 `a`。但 `mg` 是一个函数而不是 `m a`。

相反，我首先需要调用函数 `mg`，然后我将拥有想要的 `m a`：

```haskell
f :: a -> b
mg :: r -> m a
mg r :: m a
```

所以让我们这样做：

```haskell
instance functorReaderT :: Functor (ReaderT r m) where
  map f (ReaderT mg) = ReaderT \r -> f <$> mg r -- COMPILER ERROR!!
```

现在，我们有一个全新的编译器错误：

![](img/8c0e9b687c62642e828ccb5481e11313_918_0.png)

`m3` 或我们称之为 `m` 没有 `Functor` 实例。那是因为我在想 `m` 是一个 `Monad`，或者在这种情况下是一个 `Functor`，因为我只在它上面使用 `<$>`。但编译器读不懂我的想法。

所以，我们将通过在 `m` 上添加 `Functor` 约束来修正我的错误：

```haskell
instance functorReaderT :: Functor m => Functor (ReaderT r m) where ①
  map f (ReaderT mg) = ReaderT \r -> f <$> mg r
```

① 添加了 `Functor` 约束，因为我们使用了 `<$>`。

现在我们可以继续进行 `Apply` 实例：

```haskell
instance applyReaderT :: Functor m => Apply (ReaderT r m) where
```

我们 proactively 添加了 `Functor` 约束，因为我们的 `Functor` 实例有它，而且它是我们的超类。

接下来，我们将添加左手边：

```haskell
instance applyReaderT :: Functor m => Apply (ReaderT r m) where
  apply (ReaderT fmf) (ReaderT fmx) = ???
```

- 名称 `fmf` 提醒我们我们有一个返回底层 `Monad` 中函数的函数。
- 名称 `fmx` 提醒我们我们有一个返回底层 `Monad` 中值的函数。

我们将添加常见的模式：

```haskell
instance applyReaderT :: Functor m => Apply (ReaderT r m) where
  apply (ReaderT fmf) (ReaderT fmx) = ReaderT \r -> ???
```

现在，我们必须停下来思考。我们想在调用函数获取其返回值之后再将 `fmf` 应用于 `fmx`。我们不想像上次那样忘记调用函数。

而且由于 `fmf` 返回一个函数，`fmx` 返回一个值，两者都在底层 `Monad` 中，我们可以只利用底层 `Monad` 的 `<*>` 实现：

```haskell
instance applyReaderT :: Functor m => Apply (ReaderT r m) where
  -- COMPILER ERROR!!
  apply (ReaderT fmf) (ReaderT fmx) = ReaderT \r -> fmf r <*> fmx r
```

利用底层 `Monad` 的 `apply` 实现。

现在编译器有异议：

![](img/8c0e9b687c62642e828ccb5481e11313_919_0.png)

我们缺少对 `m` 的 `Apply` 实例。我将其约束为 `Functor`，但然后使用了 `<*>`。让我们修复我的

hasty mistake:

```haskell
instance applyReaderT :: Apply m => Apply (ReaderT r m) where
  apply (ReaderT fmf) (ReaderT fmx) = ReaderT \r -> fmf r <*> fmx r
```

当然，我们总是可以用 `ap` 来作弊，但为了学习，手工编码要好得多。

现在，我们可以开始 `Applicative` 实例：

```haskell
instance applicativeReaderT
  :: Apply m => Applicative (ReaderT r m) where ①
```

① proactively adding Apply Constraint since our Superclass has that Constraint. But, this time, I’ll keep in mind that this Constraint may change based on our code.

现在我们可以编写左手边：

```haskell
instance applicativeReaderT
```
