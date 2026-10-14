

尽量在阅读后续内容之前写出尽可能多的右侧内容。

就像我们的 Functor 实例一样，我们知道我们将返回一个 Parser，它有一个函数接收一个 String，我们称之为 s。所以让我们写下这么多：

```
instance applyParser :: Apply (Parser e) where
  apply :: ∀ a b. Parser e (a -> b) -> Parser e a -> Parser e b
  apply (Parser f) (Parser g) = Parser \s -> ???
```

如果我们在此停止并确定 f 和 g 的类型，这将极大地帮助我们在等号右侧编写代码。

如果你想在阅读我的方法之前自己尝试一下，现在就可以随意尝试。

让我们从 Parser f 和 Parser g 类型开始：

```
Parser f :: Parser e (a -> b)
Parser g :: Parser e a
```

g 看起来更容易确定，所以让我们先处理 g。我们知道解析器包含 ParseFunction，所以让我们将解析器定义和 ParseFunction 定义都加入进来：

```
type ParseFunction e a =
  ParserError e => String -> Either e (ParserState a)
newtype Parser e a = Parser (ParseFunction e a)

Parser f :: Parser e (a -> b)
Parser g :: Parser e a
```

所以让我们仅使用 Parser 和 ParseFunction 定义作为参考来写出 g 的类型：

```
type ParseFunction e a =
  ParserError e => String -> Either e (ParserState a)
newtype Parser e a = Parser (ParseFunction e a)

Parser f :: Parser e (a -> b)
Parser g :: Parser e a

g :: String -> Either e (ParserState a)
```

现在我们可以简单地将 g 的类型签名中的 a 替换为 a -> b 来得到 f 的类型签名，因为这是 `Parser g` 和 `Parser f` 的类型签名之间唯一的差异：

```
Parser f :: Parser e (a -> b)
Parser g :: Parser e a

f :: String -> Either e (ParserState (a -> b))
g :: String -> Either e (ParserState a)
```

我们现在可以回到我们的代码：

```
instance applyParser :: Apply (Parser e) where
  apply :: ∀ a b. Parser e (a -> b) -> Parser e a -> Parser e b
  apply (Parser f) (Parser g) = Parser \s -> ???
```

此时，让我们退一步仔细看看我们有什么。我们有 2 个解析器。我们显然想要构建一个最终的解析器来调用它们两者。但顺序是什么？最左边的解析器应该先调用还是后调用？

记住 apply 的二元运算符的定义：

```
infixl 4 apply as <*>
```

所以，apply 将被用作：

```
parser1 <*> parser2 <*> parser3
```

并且，由于 `<*>` 是左结合的，上面的表达式等价于：

```
((parser1 <*> parser2) <*> parser3) ❶
```

❶ 添加了隐含的括号。

应该很清楚解析器是从左到右应用的。换句话说，我们希望先执行最左边的。

继续调用第一个解析器函数 f，它返回一个 Either。然后使用 case 表达式检查其返回值。在阅读任何进一步内容之前尽可能进行下去。

这里我们调用 f：

```
```haskell
instance applyParser :: Apply (Parser e) where
  apply :: ∀ a b. Parser e (a -> b) -> Parser e a -> Parser e b
  apply (Parser f) (Parser g) = Parser \s -> f s        -- COMPILER ERROR!!
```
```

现在添加 `case` 表达式：

```
```haskell
import Data.Either (Either(..))
import Data.Tuple (Tuple(..))

instance applyParser :: Apply (Parser e) where
  apply :: ∀ a b. Parser e (a -> b) -> Parser e a -> Parser e b
  apply (Parser f) (Parser g) = Parser \s -> case f s of
    Left err -> Left err
    Right (Tuple s1 h) -> ???
```
```

+   1. 添加 `(..)` 以导入数据构造函数，`Left` 和 `Right`。
+   2. 如果第一个 `Parser` 失败，我们简单地返回一个错误。
+   3. 记住，`ParserState` 是一个 `Tuple`。
+   4. 如果它成功，`s1` 是第一个 `Parser` 完成后的剩余 `String`。另外，`h` 是从 `f :: String -> Either e (ParserState (a -> b))` 返回的 `Function`。

我们基本上只需要机械地重复我们对第一个 `Parser` 所做的事情，唯一的区别是 `g` 将返回一个值而不是一个函数。我们将使用 `h` 对这个值进行映射。

在阅读解决方案之前先自己做这一步。

这里是解决方案：

```
```haskell
instance applyParser :: Apply (Parser e) where
  apply :: ∀ a b. Parser e (a -> b) -> Parser e a -> Parser e b
  apply (Parser f) (Parser g) = Parser \s -> case f s of
    Left err -> Left err
    Right (Tuple s1 h) -> case g s1 of
      Left err -> Left err
      Right (Tuple s2 x) -> ???
```
```

+   1. 如果我们的第二个 `Parser` 失败，我们返回一个错误。
+   2. 注意我们在这里将变量命名为 `x`，以提醒我们 `g` 在 `Tuple` 中返回一个值。
+   3. 这里 `s2` 是第二个 `Parser` 处理完之后 `String` 的剩余部分。

先自己编写这最后一步，然后再继续阅读。

最后一步：

```
instance applyParser :: Apply (Parser e) where
  apply :: ∀ a b. Parser e (a -> b) -> Parser e a -> Parser e b
  apply (Parser f) (Parser g) = Parser \s -> case f s of
    Left err -> Left err
    Right (Tuple s1 h) -> case g s1 of
      Left err -> Left err
      Right (Tuple s2 x) -> Right $ Tuple s2 (h x) ①
```

① 我们将 h :: a -> b 应用于 x :: a，产生一个类型为 b 的值。这是 apply 方法的全部目的，将 Parser e a 更改为 Parser e b。

请注意，我们不得不处理错误情况，两次。如果这段代码看起来很冗长，那是因为它确实很冗长。我们在学习了 Monad 之后就可以回来简化它。事实证明 Either 是一个 Monad，Monad 类型类中的方法将使这段代码更漂亮。但现在，这段代码是可行的。

注意一下，我们写了多少代码。它并不多。但很密集。涉及了大量的思考来弄清楚我们的类型并确保我们按正确的顺序做事。

虽然思考很困难，尤其是第一次，但编码本身并不算太难。我们以前经历过这种情况，也会继续这样做。这就是我开玩笑说在 Haskell（或 PureScript）中，你思考 2 小时，编码 2 分钟时所指的情况。

最后，我们应该让我们的解析器成为一个 Applicative。为此，查找 Pursuit 上的 Applicative。在阅读后续内容之前，先自己编写 Applicative 实例。

正如 always，实例定义首先是：

```
instance applicativeParser :: Applicative (Parser e) where
```

然后是方法，这里只有 pure：

```
instance applicativeParser :: Applicative (Parser e) where
  pure x = Parser \s -> ???
```

所以接下来我们只需要返回 x 的成功解析，而不从 String s 中消耗任何字符。如果你在这里卡住了，尝试应用这种策略，看看是否能完成它。然后再继续阅读。

这是完成的类定义：

```
instance applicativeParser :: Applicative (Parser e) where
  pure x = Parser \s -> pure $ Tuple s x ①
```

① 注意，最右边的 pure 是 Either 的 pure。

我们从 s 中消耗零个字符，只是简单地原样返回它。我们还返回 x，就好像我们确实解析了某些东西一样。这有点像 const，但针对解析器。

我们现在拥有了一个 Applicative 解析器。

## 17.10. 深入了解我们的解析器

在为我们的解析器编写了 Apply 实例之后，你可能或多或少会想知道我们如何能有一个解析器，它有一个函数接收一个 String 并返回一个函数 a -> b。似乎很荒谬。我们调用一个解析函数，它可能消耗一个 String 的全部或部分，并返回一个函数。返回一个 Int 或一个 Boolean 或其他值是有意义的，但一个函数呢？

虽然这听起来很奇怪，但实际上并非如此。让我们看看解析器可以从中返回函数的 2 种情况。

第一种情况是当我们使用 pure 时：

```
instance applicativeParser :: Applicative (Parser e) where
  pure x = Parser \s -> pure $ Tuple s x
```

我们可以看到 String s 根本没有被消耗，而是简单地原样返回。如果 x 是一个函数，那么我们可以看到一个解析器如何接收一个 String 并返回一个函数。它不消耗 String 的任何部分，而是连同函数一起返回它。所以这种情况是有意义的。

第二种情况是当我们调用 map 时：

```
instance functorParser :: Functor (Parser e) where
  map f (Parser g) = Parser \s -> map f <$> g s
```

在这种情况下，String 由 g 我们的原始解析器消耗，然后我们对 g s 的输出值进行映射。但这种情况下如何返回一个函数？

记住 f 的类型是 a -> b。但 b 可以是任何东西，并且由于柯里化，b 可以是一个函数，例如 c -> d -> e。所以如果我们用一个仅部分应用的函数来映射一个解析器，那么该结果解析器将返回一个函数。

现在，让我们检查 apply，在这里我们期望左侧是一个返回函数的解析器：

