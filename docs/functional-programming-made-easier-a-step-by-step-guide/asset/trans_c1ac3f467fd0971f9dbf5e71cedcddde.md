

解析器，让我们开始建模我们的 Types。

首先，我们谈到每个 Parser 接受一个 State 并返回该 State。在不考虑它如何工作之前，让我们简单地设计我们的 Parser State。我们知道我们将从字符串中解析字符并返回某些内容。在我们日期示例的情况下，我们需要解析 String 并返回一个 Int。

我们希望该 Parser 返回一个 Int。但并非每个 Parser 都会将数字解析为 Int。因此，我们希望我们的 Parser 返回多态参数 a。而 a 没有任何约束。a 可以是任何 Type。

我们需要的另一件事是要解析的 String。我们将从该 String 中消费我们需要的部分并返回剩余的部分。

在开始编码之前，创建一个名为 Parser.purs 的新 Module 并添加以下内容：

```
module Parser where

import Prelude

import Effect (Effect)
import Effect.Console (log)

test :: Effect Unit
test = do
  log "placeholder"
```

并将你的 Main module 改为：

```
module Main where

import Prelude
import Effect (Effect)

import Parser as P

main :: Effect Unit
main = P.test
```

并使用以下命令运行它：

```
npx spago run
```

这应该会显示：

```
Compiling Main
[info] Build succeeded.
placeholder
```

继续并建模一个名为 `ParserState` 的 Type 或 Type Alias，它同时包含 Type `a` 的解析值和一个 `String`。在继续阅读之前先做这件事。

因此，建模这个 Type 并不是很直接，因为有很多方法可以做到这一点。我会展示几种：

```
type ParserState a = Tuple String a

data ParserState a = ParserState String a

newtype ParserState a = ParserState (Tuple String a)
```

虽然 `data` 和 `newtype` 是正确的类型，但我看不出有什么比一个简单的 Type Alias 更需要的，至少在这一点上是这样。我可能会后悔这个决定，但现在，我认为它足够好了。它让我们能够利用为 `Tuple` 编写的代码，例如 `Functor`、`Bifunctor`、`Applicative` 等。

请注意，我们将多态参数 `a` 放在第二位。那样我们就可以利用 `Tuple` 的 `Functor` 实例。不确定我们是否需要它，但现在没有损失，所以我们最好把它放在第二位。

因此更改你的代码以使用 Type Alias：

```
import Data.Tuple (Tuple) ❶

type ParserState a = Tuple String a ❷
```

❶ 我们需要导入 `Tuple`。

❷ 我们将 `a` 类型参数放在第二位，以防有一天我们想映射它。

接下来，在建模我们的 Parser 时，要建模错误 Type。有 3 种可能性来建模它。首先，只是使用 Type Alias 使其成为人类可读的 `String`：

```
type ParserError = String
```

第二种方法是使用 Sum Type 或 Coproduct 使其计算机可读：

```
data ParserError
  = EOF
  | SomeOtherError
  | AnotherErrorWithReason String
```

最后，我们可以将其作为我们 Parser 的一个参数。这将要求我们创建一个 Typeclass 来允许我们的通用 Parser 设置错误。这是<|message|> 最复杂但也是最灵活的。这允许应用程序使用自己的错误 Type 和自己的错误。

我们正在构建的 `Parser` 通常会在库中。库开发者无法知道应用程序的错误是什么。但是，Typeclass 可以规定库将从其基础 `Parsers` 返回的错误。而应用程序可以在库之上编写自己的 `Parsers` 并从这些 `Parsers` 返回其应用程序特定的错误。

我们将采用这种方法，原因仅仅是我认为你会从中学习最多。记住，根据你的需求，Sum Type 甚至 `String` 也可以工作。但 Parser 是一个相当通用的工具，因此我们构建的灵活性越多，就能从中获得越多。

我们还没有完全准备好建模我们的 Parser。然而，我们可以写下以下内容：

```
newtype Parser a e = Parser ???
```

- `a` 是我们的返回 Type。
- `e` 是我们的错误 Type。它将由我们 `Parser` 的使用者指定。它代表应用程序特定的错误 Type。

真正的问题是我们的 Parser 包含什么。嗯，从我们所知道的来看，它可能包含一个值或一个函数。你认为它应该包含什么？

如果它只包含一个值，例如 `10` 或 "abc"，那似乎没什么用。但如果它包含一个函数，我们可以调用它来做有用的事情，例如解析一个 `String`。

因此，现在我们知道我们想要一个函数。但这个函数应该做什么？它应该 PARSE。由于我们正在解析 `Strings`，那么它将需要一个 `String`，并且由于它将与其他 Parsers 组合，它应该返回 `ParserState`，它至少应包含剩余的 `String`。

在 ParserState 中，我们有两个有用的数据。第一，解析后的值，第二，未被解析函数使用的 `String` 的部分。剩余的 `String` 然后可以传递给下一个 Parser。

你现在准备好编写一个名为 `ParseFunction` 的定义了。这个定义应该是 Parser 中函数的类型签名。请在不往前看的情况下尝试一下。

我们的 Type Alias 只是解析函数的类型签名：

```
type ParseFunction a = String -> ParserState a
```

这个类型签名缺少什么？

这个函数不能失败。因此在继续之前，先更改它以允许使用名为 `e` 的错误类型参数失败。

你可能想到的第一个想法是使用 `Maybe`，但我们不能，因为 `Maybe` 没有错误参数。它只有 `Nothing` 表示错误，而 `Nothing` 只告诉我们它失败了，而不是为什么失败。

你可能想到的下一个想法是使用我们漂亮的新 `Validation` 类型，但我们不会使用它，因为我们不想处理多个 Parser 错误的复杂性，这比你想象的要难。

要做到这一点，我们将使用 `Either`：

```
import Data.Either (Either)

type ParseFunction a e = String -> Either e (ParserState a)
```

❶ 我们需要导入 `Either`。

❷ 我们添加了 `e` 类型参数。

这样更好，但我们还需要一件事。我们需要 `e` 受一个具有设置解析器错误的方法的 Typeclass 约束。这个要求并不明显，但在编写了几个解析器之后，我知道我们需要在我们的 `Parser` 实例中指定错误。相信我。

停止阅读并为现在编写一个名为 `ParserError` 的 Typeclass 且没有任何方法。我们会在需要时添加它们。

没有方法的 Typeclass 只是：

```
class ParserError (e :: Type)
```

❶ 我们省略 `where` 关键字，因为我们没有任何方法。

❷ 我们明确告诉编译器 `e` 的 Kind 是 `Type`，因为定义右侧没有任何内容可以让它知道它不是只是任何 Kind，例如 `Symbol`、`Row Type` 或 `Constraint`。

在继续阅读之前，将 `ParseFunction` 约束为返回类型为 `ParserError` 的错误。

要约束 `ParseFunction`，我们只需将约束添加到等式的右侧：

```
type ParseFunction a e =
  ParserError e => String -> Either e (ParserState a)
```

当我们无法解析 `String` 时，我们将返回 `Left e`，否则我们将返回 `Right (ParserState a)`。

例如，假设我们有一个解析一个或多个数字的 Parser。我们有以下 `String`：

```
"123abc"
```

调用 `ParseFunction` 后，我们将得到以下返回值：

```
Right (Tuple "abc" 123)
```

现在我们可以完成编写我们的 `Parser` 类型：

```
newtype Parser a e = Parser (ParseFunction a e)
```

将此定义添加到你的代码中。

此时，你的代码应如下所示：

```
module Parser where

import Prelude

import Data.Either (Either)
import Data.Tuple (Tuple)
import Effect (Effect)
import Effect.Console (log)

type ParserState a = Tuple String a

class ParserError (e :: Type)

type ParseFunction a e =
    ParserError e => String -> Either e (ParserState a)

newtype Parser a e = Parser (ParseFunction a e)

test :: Effect Unit
test = do
    log "placeholder"
```

我们还没有写很多。我们花了很多时间思考我们想要什么并比较替代方案。一旦我们对初始选择感到满意，我们就可以继续了。

我说初始选择是有原因的。很多时候，你认为你已经正确地建模了某些东西，但后来发现你的初始评估是错误的。在这种情况下，你需要修改你的模型。我们可能以后必须这样做，但现在，这看起来不错。

那么你认为我们下一步应该做什么？如果你不确定，那就问问自己，我们的目标是什么。

答案是创建一个 Applicative Parser。因此，如果这是真的，那么我们最好为我们的 Parser 编写一个 Applicative 实例。让我们看看 Applicative 的定义，看看如何做到这一点：

```
class Apply f <= Applicative f where
    pure :: ∀ a. a -> f a
```

现在，我们正在查看 Applicative，我们可以看到我们首先需要一个 Apply 实例。因此让我们看看该定义的定义：

