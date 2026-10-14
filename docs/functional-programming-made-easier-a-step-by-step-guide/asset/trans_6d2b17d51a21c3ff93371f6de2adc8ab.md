

```
```purescript
import Data.NonEmpty (NonEmpty, fromNonEmpty, (:|))

some :: ∀ a f
  . Unfoldable f
  => (a -> f a -> f a)
  -> Parser e a
  -> Parser e (NonEmpty f a)
some cons p = (:|) <$> p <*> defer \_ -> many cons p

some' :: ∀ e. Parser e Char -> Parser e String
some' p = fromCharArray <<< fromNonEmpty (:|) <$> some (:|) p

many :: ∀ e a f
  . Unfoldable f
  => (a -> f a -> f a)
  -> Parser e a
  -> Parser e (f a)
many cons p = fromNonEmpty cons <$> some cons p <|> pure none

many' :: ∀ e. Parser e Char -> Parser e String
many' p = fromCharArray <$> many (:) p
```
```

请在继续之前更新你的代码以匹配此内容。

顺便说一下，`some` 和 `many` 已经为 PureScript 中的 `Arrays` 和 `Lists` 实现了。这里是它们对 `Arrays` 的类型签名：

```
```purescript
some :: ∀ f a. Alternative f => Lazy (f (Array a)) => f a -> f (Array a)
many :: ∀ f a. Alternative f => Lazy (f (Array a)) => f a -> f (Array a)
```
```

从一种方式来看它们比我们更通用，从另一种方式来看则更少。这专门针对 `Arrays`。它也为 `List` 正常和惰性版本编写。因此我们的更通用，因为我们适用于任何 `Unfoldable`。

但是，与我们不同的是，这些将适用于任何具有 `Lazy` 实例的 `Alternative`。

事实证明我们可以增加这种灵活性。让我们将 `Parser e` 更改为任意 `Monad`，`m`。这样做将使这些函数更灵活，并允许我们将它们用于比仅我们的 `Parser` 更多类型的类型：

```
some :: ∀ a f m ① ②
  . Unfoldable f
  => (a -> f a -> f a)
  -> m a ①
  -> m (NonEmpty f a) ①
some cons p = (:|) <$> p <*> defer \_ -> many cons p -- COMPILER ERROR!!

many :: ∀ a f m ① ②
  . Unfoldable f
  => (a -> f a -> f a)
  -> m a ①
  -> m (f a) ①
many cons p = fromNonEmpty cons <$> some cons p <|> pure none
```

① 用 m 替换了 Parser e。

② 我们还从 ∀ 中移除了 e。

选择使用 m 是因为我们的 Parser e 是一个 Monad。我们可能永远不需要将 m 约束为 Monad。我们必须等到它编译后再看看。

说到编译器，我们有一个新的编译器错误：

![](img/8c0e9b687c62642e828ccb5481e11313_845_0.png)

我们需要添加一个 Apply 约束。因为我们使用了 <*>。让我们同时为两者添加 Apply m 约束：

```
some :: ∀ a f m
  . Unfoldable f
  => Apply m ①
  => (a -> f a -> f a)
  -> m a
  -> m (NonEmpty f a)
some cons p = (:|) <$> p <*> defer \_ -> many cons p -- COMPILER ERROR!!

many :: ∀ a f m
  . Unfoldable f
  => Apply m ①
  => (a -> f a -> f a)
  -> m a
  -> m (f a)
many cons p = fromNonEmpty cons <$> some cons p <|> pure none
```

① 添加了 Apply 约束。

我们修复了那个，但现在我们有一个新的错误：

![](img/8c0e9b687c62642e828ccb5481e11313_846_0.png)

这个错误是因为我们缺少一个 Lazy 约束。因为我们使用了 defer。编译器给出了如何编写约束的线索，其推断的类型为 Contol.Lazy.Lazy (m0 (f4 a2))。

m (f a) 是一个具有 Unfoldable a 的 Apply。一个例子是 Parser e (Array a)，其中 m 是 Parser e（记住我们之前做过这个替换）而 f 是 Array。

让我们为 some 和 many 都添加一个 Lazy (m (f a)) 约束：

```
some :: ∀ a f m
  . Unfoldable f
  => Alt m
  => Apply m
  => Lazy (m (f a))
  => (a -> f a -> f a)
  -> m a
  -> m (NonEmpty f a)
some cons p = (:|) <$ p <*> defer \_ -> many cons p

many :: ∀ a f m
  . Unfoldable f
  => Alt m
  => Apply m
  => Lazy (m (f a))
  => (a -> f a -> f a)
  -> m a
  -> m (f a)
many cons p = fromNonEmpty cons <$> some cons p <|> pure none
  -- COMPILER ERROR!!
```

还有另一个错误：

![](img/8c0e9b687c62642e828ccb5481e11313_848_0.png)

由于我们使用了 pure，我们需要一个 Applicative m 约束。但等等。我们已经有一个 Apply，它是 Applicative 的超类。所以，我们将用 Applicative 替换 Apply：

```
```purescript
some :: ∀ a f m
  . Unfoldable f
  => Alt m
  => Applicative m
  => Lazy (m (f a))
  => (a -> f a -> f a)
  -> m a
  -> m (NonEmpty f a)
some cons p = (:|) <$> p <*> defer \_ -> many cons p

many :: ∀ a f m
  . Unfoldable f
  => Alt m
  => Applicative m
  => Lazy (m (f a))
  => (a -> f a -> f a)
  -> m a
  -> m (f a)
many cons p = fromNonEmpty cons <$> some cons p <|> pure none
```
```

> ¹ 用 `Applicative` 替换了 `Apply`。

最后，我们有一个开心的编译器。注意我们不需要将 `m` 约束为 `Monad`。它只需要是一个 `Applicative`。

另外，注意我们不需要更改任何代码来使我们的函数更通用。在这次泛化最后一步中，我们只需要将特定类型更改为更通用的类型。这并不总是会发生，但很多时候我们可以通过简单地选择更通用的类型来泛化一个函数。

现在是时候对你的代码进行这些更改了。

现在我们可以在多种情况下使用这些版本的 `some` 和 `many`，而不仅仅是 `Parsers`。我们也不必为不同类型编写这些函数的多个版本，只要它们实现了 `Unfoldable`。让这些函数泛化绝对值得付出努力。

注意我们陷入了一个紧密的循环：更改代码，得到一个错误，再次更改并得到另一个错误，然后再次更改代码，等等。你会发现自己在玩这个游戏，希望代码最终能编译。

这种策略并不总是有效。这里成功是因为我们只是添加约束和更改类型。但通常情况并非如此，我建议不要盲目地进行更改，希望错误信息会神奇地消失。最好先放慢速度，了解出了什么问题，然后再更改代码。

此时，重新运行测试以确保我们没有破坏任何东西是个好主意。可能性非常小，因为我们只是更改了类型，而编译器就是这些更改的测试。

另一个值得提及的点是，我们最终的类型签名看起来很吓人。但我们并不是第一次就写下了这些吓人的类型签名。我们最初写的是简单的签名，并在泛化的过程中一遍又一遍地重写它们，直到它们变得更复杂。但你看到了过程。它不是魔法。它也不难。它只是从代码的具体版本到非常抽象版本的许多增量更改。

所以，当你在野外看到这种类型签名时，不要惊慌。如果有你不了解的约束，那就去学习它们。如果有你不熟悉的类型，那就去熟悉它们。因为这就是全部，就像你现在所见证的那样。

并且因为我们理解了我们在约束中使用的类型和类，我们可以轻松地证明我们类型签名的每个部分，例如在 some 中：

```
some :: ∀ a f m
  . Unfoldable f
  => Alt m
  => Applicative m
  => Lazy (m (f a))
  => (a -> f a -> f a)
  -> m a
  -> m (NonEmpty f a)
```

① 一个 Unfoldable。这是因为我们在 many 中使用了 none。

② 因为我们调用 many 而它使用了 <|>。

③ 因为我们调用 many 而它使用了 pure。

④ 因为我们需要用 defer 打破无限循环。

⑤ cons-like 函数，这意味着我们期望我们的 Unfoldable 是一个类似列表的结构。

⑥ 我们将利用的原始 Applicative of a’s。 对于 Parsers，这是一个我们会根据需要一遍又一遍使用的单个 Parser。

⑦ 产生 NonEmpty 类似列表结构的新的 Applicative。对于 Parsers，这是一个在运行 Parser 时会产生类似列表结果的 Parser。

如果我们第一次看到这个类型签名，我们可能会觉得它令人望而生畏。如果我们不理解 Unfoldable 或 Lazy 等，就会如此。但既然我们理解了，我们就可以一次看一行，慢慢地理解这个类型签名意味着什么。有时，我们需要查看函数的实现才能获得像我们上面为 some 提供的那种洞察力。

对于像这样复杂的类型签名，这个过程可能需要相当长的时间，所以请确保相应地设定你的期望。不要因为花 20 分钟或更长时间来理解一个而责怪自己。理解复杂的东西需要时间和练习。你做得越多，你就会越快。

