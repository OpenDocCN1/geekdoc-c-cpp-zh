
```
```haskell
class ParserError (e :: Type) where
  eof :: e
```
```

❶ 别忘了添加 `where` 关键字。之前我们不需要它，因为我们没有方法。

❷ 这里 `e` 是我们的应用特定错误类型。

现在，我们通用 `Parser` 的用户创建的任何错误类型，都必须至少支持 `char` 解析器的 `eof`。

```
```haskell
data MyError
  = EOF
  | InvalidThing

instance parserErrorMyError :: ParserError MyError where
  eof = EOF
```
```

❶ 虚构的错误类型。

❷ `EOF` 代表 `char`。

❸ `InvalidThing` 是一个应用特定错误。这很可能是应用开发者编写的更高级别 `Parser` 的错误。

```
```haskell
data ParsingError
  = NoMoreData
  | MissingStuff String
  | IntOutOfRange Int

instance parserErrorParsingError :: ParserError ParsingError where
  eof = NoMoreData
```
```

❶ 另一个虚构的错误类型。

❷ 这个错误类型的设计者决定用 `NoMoreData` 这个值来表示 `String` 耗尽。

❸ 当 `char` 耗尽 `String` 时，它将使用该实例的 `eof`，它返回 `NoMoreData`。

请记住，我们选择的方法允许我们 `Parser` 的用户灵活地为他们自己的错误命名，正如我们在前面这两个例子中所做的那样。

现在，我们将创建自己的错误类型，并将其命名为 `ParseError`，只有一个数据构造函数 `EOF`。

我们还需要为它创建一个 `ParserError` 实例。请参考上面的示例来编写代码。

另外，为 `PError` 添加一个 `Show` 实例，因为稍后编写测试代码时会用到它。

请先完成这些，再继续往下看。

下面是我们定义的错误类型：

```
import Data.Generic.Rep (class Generic)
import Data.Show.Generic (genericShow) ①

data PError
  = EOF
derive instance genericPError :: Generic PError _ ②

instance showPError :: Show PError where ③
  show = genericShow

instance parserErrorPError :: ParserError PError where ④
  eof = EOF
```

① 我们需要导入 `genericShow`，因为我们将在 `Show` 实例中利用它。

② 我们需要派生 `Generic`，以便使用 `genericShow`。

③ 我们的 `Show` 实例。

④ 我们让 `PError` 成为 `ParserError` 的一个实例，以便我们可以将它用于我们正在构建的解析器。

随着需要，我们会给它添加更多的方法。

现在，我们可以回到手头的工作，完成 `char` 的错误处理。请先尝试一下，再继续阅读。

你可能很想写出下面的代码：

```
char :: ∀ e. Parser e Char
char = Parser \s -> case uncons s of
  Nothing        -> Left EOF      -- COMPILER ERROR!! ①
  Just { head, tail } -> Right $ Tuple tail head
```

① 编译器错误，因为它无法将 e0 匹配到 ParserError。

错误如下：

![](img/8c0e9b687c62642e828ccb5481e11313_642_0.png)

即使它能编译通过，也仍然是错误的。因为我们目前只是在学习，所以所有代码都写在单个 Module 中。因此编译器知道 `EOF`。

但如果我们将 Parser 实现提取到它自己的库中，就像在生产代码中那样，我们就不会移动 `PError`。这是因为 `PError` 是一个应用特定的错误类型。这正是创建 `ParserError` 类型类的全部意义所在。

`char` 将是我们库中的一个基础解析器，它无法知道库的用户会将表示字符串数据结束的错误称为什么。因此，上面的代码永远不可能在那个库中编写。

相反，我们需要使用 `eof`，即 `ParserError` 类型类的方法，来为应用特定的错误类型 `e` 获取正确的错误值：

```
char :: ∀ e. Parser e Char
char = Parser \s -> case uncons s of
  Nothing          -> Left eof
  Just { head, tail } -> Right $ Tuple tail head
```

确保你的代码使用的是 `eof` 而不是 `EOF`。

接下来，编写一个名为 `twoChars` 的解析器，它返回 `Tuple Char Char`。在开始之前有一个提示：你将用到 `<$>` 和 `<*>`。请先尝试一下，再继续前进。

类型签名应为：

```
twoChars :: ∀ e. Parser e (Tuple Char Char)
```

顺便提一下，我们不必用 `ParserError` 来约束 `e`。看一看 `Parser` 和 `ParseFunction` 的定义，就知道为什么了：

```
type ParseFunction e a =
  ParserError e => String -> Either e (ParserState a)

newtype Parser e a = Parser e (ParseFunction e a)
```

现在你能看出为什么了吗？

因为当你用 `ParseFunction e a` 的定义替换 `twoChars` 类型签名中的 `ParseFunction e a` 时，你会得到：

```
twoChars :: ∀ e. Parser e (ParserError e =>
                         String -> Either e (ParserState (Tuple Char Char)))
```

在这个定义中，`e` 已经被 `ParseFunction` 定义中的约束所约束，这就是我们不必再指明它的原因。

现在我们将继续编码，从 `char` 开始，它解析单个 `Char`：

```
twoChars :: ∀ e. Parser e (Tuple Char Char)
twoChars = char        -- COMPILER ERROR! ❶
```

> ❶ 类型不匹配，因为我们还没有完成。

现在我们有了一个单独的 `char` 解析器，它会返回单个 `Char`。但我们希望它返回这个 `Char` 作为 `Tuple` 的第一个部分。所以让我们将 `Tuple` 映射到 `Parser` 上：

```
twoChars :: ∀ e. Parser e (Tuple Char Char)
twoChars = Tuple <$> char        -- COMPILER ERROR! ❶
```

> ❶ 类型不匹配，因为我们还没有完成。

现在我们有了 `Tuple` 数据构造函数，它是一个函数，在一个上下文（即 `Parser` 内部）中被部分应用。幸运的是，`Parser` 是一个 `Applicative`，这意味着它也是一个 `Apply`。所以我们可以使用 `<*>` 将一个 `Parser` 中的函数应用到另一个 `Parser` 的结果上。

那么让我们应用另一个 `Parser`，即 `char`：

```
twoChars :: ∀ e. Parser e (Tuple Char Char)
twoChars = Tuple <$> char <*> char
```

当你只看最终解决方案时，这可能会感觉像魔法。但它并非如此。

在继续阅读之前，请重写 `threeChars`，让它返回一个 `String`。

我们的类型签名需要改变：

```
threeChars :: ∀ e. Parser e String
```

现在，我们应该编写一个函数来接收 3 个字符并生成一个 `String`，然后用该函数替换前面示例中的 `Threeple` 数据构造函数。

```
import Data.String.CodeUnits (uncons, fromCharArray) ①

threeChars :: ∀ e. Parser e String
threeChars =
  (\c1 c2 c3 -> fromCharArray [c1, c2, c3]) <$> char <*> char <*> char
```

① 添加了 `fromCharArray`。

我们还没有测试过任何代码。所以让我们移除占位测试代码，并添加以下内容以确保我们没有 bug：

```
log $ show $ parse char "ABC" ①
log $ show $ parse twoChars "ABC" ②
log $ show $ parse threeChars "ABC" ③
```

① 打印 (Right (Tuple "BC" 'A'))。

② 打印 (Right (Tuple "C" (Tuple 'A' 'B')))。

③ 打印 (Right (Tuple "" "ABC"))。

但一旦你添加了这些，你会得到一个错误，这是因为编译器无法推断出错误类型是什么。我们可以像过去那样通过添加显式类型来修复这个问题：

```
log $ show $ (parse char "ABC" :: Either PError _)
log $ show $ (parse twoChars "ABC" :: Either PError _)
log $ show $ (parse threeChars "ABC" :: Either PError _)
```

但这既丑陋又繁琐。所以，我们不如简单地编写一个新的 `parse` 函数，来明确指定错误类型：

```
parse' :: ∀ a. Parser PError a -> ParseFunction PError a ①
parse' = parse
```

① 我们已经用 `PError` 替换了 `parse` 类型签名中的 `e`。

这个函数只能返回 `PError`，而 `parse` 可以返回任何 `e`。

现在我们在测试代码中改用 `parse'`：

```
log $ show $ parse' char "ABC"
log $ show $ parse' twoChars "ABC"
log $ show $ parse' threeChars "ABC"
```

通过运行以下命令来运行你的测试代码：

```
npx spago run
```

然后你会得到以下 spago 错误：

```
[error] Some of your project files import modules from packages that are not in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in your config:
- either
```

将 `either` 添加到 `spago.dhall`，然后再次运行。

这应该输出：

```
(Right (Tuple "BC" 'A'))
(Right (Tuple "C" (Tuple 'A' 'B')))
(Right (Tuple "" "ABC"))
```

它们都返回 `Right` 这一事实告诉我们，在每种情况下我们都成功解析了。

`Tuple` 的第一个元素是 `Parser` 完成后剩下的内容。在第一个结果中，我们可以看到它消耗了 1 个字符，并在剩余的 `String` 中返回了 2 个字符，即元组的第二个元素。

第二个结果消耗了 2 个字符，在 `String` 中留下了 1 个字符。最后一个情况消耗了全部 3 个字符，留给我们的是一段空 `String`。

我们可能应该测试一个失败的情况。所以添加以下测试用例：
