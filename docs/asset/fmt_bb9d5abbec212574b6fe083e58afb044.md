
① 将 `fromMaybe` 添加到导入列表中。

② 我们在映射之前组合我们的 Functions，并且由于 Functor 的组合律，即 `map (g <<< f) = map g <<< map f`，它是等价的。

现在 `year` 的 Type 是什么？

以下是 `fromMaybe` 的 Type Signature 来帮助你回答这个问题：

```
fromMaybe :: ∀ a. a -> Maybe a -> a
```

由于传递给我们代码中 `fromMaybe` 的第一个参数是 `Int`，`year` 必须是一个 `Int`。

我们离想要的结果很近，但还差一点。让我们看看 `DateParts`，我们的 Parser 返回的 Type：

```
newtype Year = Year Int

newtype Month = Month Int

newtype Day = Day Int

type DateParts =
  { year :: Year ①
  , month :: Month
  , day :: Day
  , format :: DateFormat
  }
```

① 这个 `year` 的 Type 是 `Year`。

我们可以使用 `Year` Data Constructor 将我们的 `Int` 变成一个 `Year`，以便它与构造 `DateParts` 时所需的 Type 相匹配：

```haskell
yearFirst :: ∀ e. ParserError e => Parser e DateParts
yearFirst = do
  year <- Year <<< fromMaybe 0 <<< fromString <$> count' 4 digit
  ???
```

如果你觉得自己可以在此时继续编写 `yearFirst` 的其余部分，那么就停止阅读这里，看看你能做到什么程度。完成后或遇到下一个障碍时，再回来看看如何继续。

下一步是解析字符 `-`。我们可以使用 `satisfy` 来实现。以下是 `satisfy` 的参考：

```haskell
satisfy
  :: ∀ e
  . ParserError e
  => String
  -> (Char -> Boolean)
  -> Parser e Char
satisfy expected pred =
  char >>= \c -> if pred c then pure c else fail $ invalidChar expected
```

`satisfy` 接受 2 个参数。第一个参数是一个 `String`，在失败的情况下告诉我们这个 `Parser` 期望什么字符。第二个是 Predicate，用来确保字符是正确的。

如果你在这里卡住了，值得停下来看看是否能写出下一行。

这里是下一行：

```haskell
yearFirst :: ∀ e. ParserError e => Parser e DateParts
yearFirst = do
  year <- Year <<< fromMaybe 0 <<< fromString <$> count' 4 digit
  void $ satisfy "_" (_ == '-')
  ???
```

+   1. 使用 `void` 丢弃 `Parser` 返回的 `Char`。由于它总是 `-`，我们不需要将其放入变量中。
+   2. Predicate 是通配符 Function，`(_ == '-')`，如果字符等于 `-` 则返回 `true`。
+   3. 注意单引号来定义字符字面量。

这段代码很糟糕。它很丑陋，而且我们将不得不一遍又一遍地使用这段丑陋的代码。让我们通过将其封装到一个 helper Function 中来修复它。

编写一个名为 `constChar` 的 `Parser`，让我们可以把这段丑陋的代码行提取出来。以下是我想写的内容：

```
yearFirst :: ∀ e. ParserError e => Parser e DateParts

yearFirst = do

  year <- Year <<< fromMaybe 0 <<< fromString <$> count' 4 digit

  constChar '-'

  ???
```

这样看起来好多了。

在继续之前尝试编写 `constChar`。

我们将通过编写其 Type Signature 来开始编写 `constChar`：

```
constChar :: ∀ e. ParserError e => Char -> Parser e Char
```

我们将 `e` 约束为 `ParserError`，因为我们最终会调用 `satisfy`，它也有这个约束，因为它可能会失败。

第一个参数是我们期望解析的字符。

接下来，我们将添加实现左侧部分：

```
constChar :: ∀ e. ParserError e => Char -> Parser e Char

constChar c = ???
```

接下来，我们将委托给 `satisfy`：

```
constChar :: ∀ e. ParserError e => Char -> Parser e Char

constChar c = satisfy ??? (\_ == c)
```

需要用 `c` 转换为 `String` 的值替换 `???`。

`satisfy` 的第一个参数的问题是它想要一个 `String`，如果 Predicate 失败时告诉我们期望的是什么。

如何将一个 `Char` 转换为 `String`。我们可以把它放在一个 `Array` 中然后调用 `fromCharArray`。但这感觉像是过度设计。

停止阅读并去 `Pursuit` 搜索 Type Signature `Char -> String`。

当我这样做时，我找到了 `Data.String.CodeUnits` 中的 `singleton`，它完全符合我们的需求。我们将添加它：

```
import Data.String.CodeUnits (uncons, fromCharArray, singleton) ①

constChar :: ∀ e. ParserError e => Char -> Parser e Char

constChar c = satisfy (singleton c) (_ == c)
```

① 将 `singleton` 添加到导入列表中。

确保你在代码中有这个 `constChar` 的实现。

让我们回到 `yearFirst` 并使用 `constChar`：

```
yearFirst :: ∀ e. ParserError e => Parser e DateParts

yearFirst = do

  year <- Year <<< fromMaybe 0 <<< fromString <$> count' 4 digit

  constChar '_'

  ???
```

你觉得自己能完成这个吗？如果可以，就停下来看看你能做到什么程度。

我们需要解析的下一个东西是月份。我们将使用 `range'` 来做到这一点：

```
yearFirst :: ∀ e. ParserError e => Parser e DateParts

yearFirst = do

  year <- Year <<< fromMaybe 0 <<< fromString <$> count' 4 digit

  constChar '_'

  month <- Month <<< fromMaybe 0 <<< fromString <$> range' 1 2 digit

  ???
```

现在，我讨厌重复的代码。让我们停下来并将其提取出来。顺便说一下，完成这个 Function 再提取出来也没什么问题。我喜欢在看到它们时立即提取它们，否则我可能会忘记。当然，中途停止编码感觉有点突兀，但我认为你会看到这会物有所值。

所以，继续编写一个 Function 来提取我们被迫重复的 `fromMaybe` 和 `fromString` 部分。把这个 Function 命名为 `digitsToNum`。然后继续阅读。

`digitsToNum` 的 Type Signature：

```
digitsToNum :: String -> Int
```

记住，我们“知道”我们有一个由数字组成的 `String`，因为我们的 Parsers 使用了 `digit`。如果我们要把它放在一个库中，我建议用适当的警告来记录这个 Function 的有限用途。换句话说，用户自负。

以下是实现的左侧部分：

```
digitsToNum :: String -> Int

digitsToNum s = ???
```

当我们回顾 `yearFirst` 所做的事情时，我们可以看到我们使用了 Function Composition。所以，让我们以 Point-free 的方式编写它：

```
digitsToNum :: String -> Int

digitsToNum = ??? ①
```

① 由于我们采用 Point-free 方式，移除了 `s` 参数。

现在，我们只需复制 `fromMaybe` 和 `fromString` 的组合并将其放在右侧：

```
digitsToNum :: String -> Int

digitsToNum = fromMaybe 0 <<< fromString
```

现在我们可以在 `yearFirst` 中使用它：

```
yearFirst :: ∀ e. ParserError e => Parser e DateParts

yearFirst = do

  year <- Year <<< digitsToNum <$> count' 4 digit

  constChar '_'

  month <- Month <<< digitsToNum <$> range' 1 2 digit

  ???
```

你觉得自己现在能完成这个吗？在继续之前先试试。

下一步是解析第二个 `-` 字符：

```
yearFirst :: ∀ e. ParserError e => Parser e DateParts

yearFirst = do

  year <- Year <<< digitsToNum <$> count' 4 digit

  constChar '-'

  month <- Month <<< digitsToNum <$> range' 1 2 digit

  constChar '-'

  ???
```

最后需要解析的是日：

```
yearFirst :: ∀ e. ParserError e => Parser e DateParts

yearFirst = do

  year <- Year <<< digitsToNum <$> count' 4 digit

  constChar '-'

  month <- Month <<< digitsToNum <$> range' 1 2 digit

  constChar '-'

  day <- Day <<< digitsToNum <$> range' 1 2 digit

  ???
```

最后一步是返回一个 `DateParts`。请尝试完成这最后一部分，但这里有一个提示：不要忘记使用 `pure`。

下面是最后一行代码：

```
yearFirst :: ∀ e. ParserError e => Parser e DateParts

yearFirst = do

  year <- Year <<< digitsToNum <$> count' 4 digit

  constChar '-'                                      -- COMPILER ERROR!!

  month <- Month <<< digitsToNum <$> range' 1 2 digit

  constChar '-'

  day <- Day <<< digitsToNum <$> range' 1 2 digit

  pure { year, month, day, format: YearFirst }
```

最后一行包含了很多内容。首先，我们使用 `pure`，因为我们必须返回一个 `Parser`。

其次，我们不必指定 `year: year`。我们使用了一个快捷方式。如果字段名与某个变量匹配，我们只需指定字段名即可。注意 `format` 字段并非如此。

第三，我们将 `format` 设置为 `YearFirst`。

但是，我们遇到了一个编译器错误：

```
log $ show $ parse' yearFirst "1999-12-31" -- COMPILER ERROR!! ①
```

① 一旦编译通过，它应该打印 `(Right (Tuple "" { day: (Day 31), format: YearFirst, month: (Month 12), year: (Year 1999) }))`。有趣的是，字段是按字母顺序打印的。

当然，我们还有一个编译器错误：

![](img/8c0e9b687c62642e828ccb5481e11313_825_0.png)

嗯，从这里可以清楚地看出，我们缺少一个 Show 实例用于 Year。请修正这个问题，并顺便为 Month、Day 和 DateFormat 各添加一个 Show 实例。

在这里停下来，等编译器错误消失，或者当你遇到问题需要帮助时再回来继续阅读。

以下是让日期类型变为可显示的改动：

```
newtype Year = Year Int

derive instance genericYear :: Generic Year _

instance showYear :: Show Year where

    show = genericShow

newtype Month = Month Int

derive instance genericMonth :: Generic Month _

instance showMonth :: Show Month where

    show = genericShow

newtype Day = Day Int

derive instance genericDay :: Generic Day _

instance showDay :: Show Day where

    show = genericShow

data DateFormat

    = YearFirst

    | MonthFirst

derive instance genericDateFormat :: Generic DateFormat _

instance showDateFormat :: Show DateFormat where

    show = genericShow
```

请注意，我们不需要让 `DateParts` 变为可显示。这是因为 Record 是一种原始类型，因此只要它的每个字段都是可显示的，它就是可显示的。

现在是测试的好时机。运行程序，看看它是否输出了你预期的结果。

此时，你应该能够编写完整的先解析月份的解析器了。试一下，将它命名为 `monthFirst`。以 `yearFirst` 作为编码模板。完成后，继续阅读。

我们可以简单地重新排列 `yearFirst` 中的代码行，将常量字符从 `-` 改为 `/`，并将格式改为 `MonthFirst`：

这些组合子接受一个或多个解析器，并生成一个新的解析器。通常，正如其名称所示，传入的解析器会以某种方式组合以生成新的解析器。

我们创建的组合子包括 `satisfy`、`optional`、`count`、`range`、`atMost` 等等。我们可以想象，我们会把所有这些组合子放到解析器库中的一个独立模块中。

现在我们有了一个可以解析不同格式日期的 `Parser`。

总的来说，我们有了一个快速创建新解析器的平台，这些解析器远比 `\d{1,2}\\{1,2}\\{4}` 更易读。

但即使如此，我们仍然没有办法解析下面这个正则表达式所匹配的内容：

```
\d*[A-Za-z]+
```

它将解析零个或多个数字，然后是一个或多个字母字符。但我们的组合子并不支持这一点。

我们很快就会实现能够让我们做到这一点的解析器组合子，但在那之前，让我们先退一步，盘点一下现状。

# 19.8. 解析器实际上是如何工作的

我们已经使用 `Parser` 有一段时间了，它可能看起来仍然像魔法一样。因此，我想再仔细看看幕后真正发生的事情，希望能消除这种神秘感。

让我们从 `map` 开始：

```
instance functorParser :: Functor (Parser e) where
  map f p = Parser \s -> map f <$> parse p s
```

然后把它与 `Maybe` 的 `map` 进行比较：

```
instance functorMaybe :: Functor Maybe where
  map _ Nothing  = Nothing
  map f (Just x) = Just $ f x
```
