

在继续阅读之前，先试一试。

`count'` 是一个简单的辅助函数，它接受与 `count` 完全相同的参数，但返回一个 `String`，因此下面就是它的类型签名：

```
count' :: ∀ e. Int -> Parser e Char -> Parser e String ①
```

① 注意，我们现在期望的是 `Parser e Char`，而不是 `count` 所接受的那种 `Parser e a`。这是因为我们要调用 `count`，并希望它返回一个 `Parser e (Array Char)`，这样我们就能把 `Array Char` 转换为 `String`。

`count'` 返回一个 `Parser e String`，这是一个在成功解析时返回 `String` 的解析器。

接下来，我们只需调用 `count`，然后使用 `fromCharArray` 将 `Array Char` 转换为 `String`：

```
count' :: ∀ e. Int -> Parser e Char -> Parser e String
count' n p = fromCharArray <$> count n p
```

请记住，这里我们使用 `<$>` 进行映射，因为 `Array Char` 位于一个上下文中，也就是位于一个 `Parser` 中。

现在，你可以将以下内容添加到你的测试代码中：

```
log $ show $ parse' (count' 3 digit) "123456" ①
log $ show $ parse' (count' 3 digit) "abc456" ②
log $ show $ parse' (count' 4 letter) "Freddy" ③
log $ show $ parse' (count' 10 alphaNum) "a1b2c3d4e5" ④
log $ show $ parse' (count' 10 alphaNum) "######" ⑤
```

① 输出为 (Right (Tuple "456" "123"))。

② 输出为 (Left (InvalidChar "digit"))。

③ 输出为 (Right (Tuple "dy" "Fred"))。

④ 输出为 (Right (Tuple "" "a1b2c3d4e5"))。

⑤ 输出为 (Left (InvalidChar "alphaNum"))。

运行测试，确保我们的代码能正常工作。

但事实并非如此：

```
```text
[error] Some of your project files import modules from packages that are not
in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in
your config:
- control
```
```

将 `control` 添加到 `spago.dhall` 中，然后重新运行程序。

## 19.7. 编写日期解析器

当我们刚开始讨论解析器时，我举了一个可用于解析日期的正则表达式的例子：

```
```text
\d{1,2}\/\d{1,2}\/\d{4}
```
```

我想你能明白，与我们目前构建的 `Parser` 类型和单子解析器相比，这是一段难以维护的糟糕代码。

所以，我们要做的是为日期编写一个 `Parser`。我们将接受两种格式：

```
```text
10/2/1962
1962-10-02
```
```

这些就是我们的规格说明。现在，我们要做一次所谓的*差距分析*，看看我们还缺少什么。也就是说，基于这些规格以及我们目前已经编写的内容，看看缺少哪些部分。

首先，我们已经有了一个针对以下内容的 `Parser`：

```
```text
\d{4}
```
```

它的意思是我们可以解析 4 位数字，并且我们有 `count` 来实现这一点。但我们还没有一个用于以下内容的 `Parser`：

```
```text
\d{1,2}
```
```

它的意思是我们将解析 1 到 2 位数字。我们需要编写一个接受计数范围的 `Parser`。我们将其命名为 `range`。

接下来，我们希望为解析出的日期建立模型，因为它是一个复杂结构，不同于我们目前解析过的那些类型，例如 `Array Char`、`String`、`Char`。我们将这个类型命名为 `DateParts`。

最后，我们需要 2 个 `Parser`，分别处理我们支持的每种格式。

这似乎就是实现我们的日期解析目标所需的全部内容。那么，让我们开始吧。

首先要做的是为类型建模。在继续阅读之前，请编写一个能够为解析出的日期建模的类型。

建模总是很困难，因为总有太多方式可以完成。我们的目标应该是为当前情况找到最佳模型。在现实世界中这很难做到，但我们在学习时所处的这种人工环境中更难。

所以，我要梳理几种可能性，然后基于一些完全人为的标准来选择一个。

下面是最天真的做法：

```
data DateParts = DateParts Int Int Int
```

看到这 3 个 `Int`，我们无法分辨哪个是年、哪个是日或月。让我们修复这个问题：

```
newtype Year = Year Int
newtype Month = Month Int
newtype Day = Day Int

data DateParts = DateParts Year Month Day
```

请记住，这些是我们从 `String` 中解析出的各个部分，并不能保证是有效日期。这超出了本问题的范围。在现实世界中，我们通常会先解析日期，然后使用日期库为我们完成验证这一艰巨工作。

你能看出我们还能对模型做哪些改进吗？我只能看出一个。

如果能知道解析日期时最初遇到的是哪种格式，那就太好了，以防我们想以原始格式将其重新打印出来。

为此，我们将创建一个和类型（Sum Type）：

```
data DateParts
  = YearFirstDate Year Month Day
  | MonthFirstDate Year Month Day
```

既然我们已经完成了这个，让我们换个策略重新开始。我们从以下内容开始：

```
type DateParts =
  { year :: Int
  , month :: Int
  , day :: Int
  }
```

现在，我们要出于另一个原因替换这里的 `Int`。之前我们这样做是为了帮助理解哪个 `Int` 对应哪个字段。但使用 Record 时我们不会有这种困惑，因为我们有带名字的字段。

当我们为年、月、日创建类型时，使用了 newtype。这带来一个额外好处：可以防止开发者（包括我们自己）以错误的顺序向 `DateParts` 数据构造器传入参数。

在这里顺序不那么重要，除非我们编写一个函数来构建这个 Record，否则参数可能会乱序。但即使我们不这样做，仍然值得对年、月、日进行建模，以免我们搞混，例如把 12 传给年份，或把 1973 传给月份：

```
newtype Year = Year Int
newtype Month = Month Int
newtype Day = Day Int

type DateParts =
  { year :: Year
  , month :: Month
  , day :: Day
  }
```

这个模型与我们之前的模型是同构的，只是没有跟踪原始格式。让我们加上这一点：

```
data DateFormat = YearFirst | MonthFirst

type DateParts =
  { year :: Year
  , month :: Month
  , day :: Day
  , format :: DateFormat
  }
```

这两个模型现在是同构的，也就是说，我可以编写一组函数在这两个模型之间进行转换，而不会丢失任何信息。

哪一个更好？你认为哪一个更好？为什么？为什么这部分是最需要回答的。

决定你更喜欢哪一个，并说明原因。要小心，避免为你直觉上的选择进行事后合理化，这是一个容易陷入的陷阱。

例如，也许我们不喜欢 Record，因为我们用得不多，所以另一种模型对我们更有吸引力。而现在，为了证明那个主观决定是合理的，我们会编造一个理性的、看似客观的理由来支持我们的选择。我们都是人，都容易受到这种影响。因此，意识到这一点非常重要，以便我们能对抗它。

因此，带着所有这些考虑，你的选择是什么？为什么？请在继续阅读之前好好思考。

好了，既然你已经有了自己的选择，我来告诉你我的选择。

我决定的方式是把这些模型推向极限。让我们想象一下，我们有几十种格式要支持。在这种情况下，每种模型的表现如何？

让我们用第一种模型来想象这个场景：

```
data DateParts
  = YearFirstDate Year Month Day
  | MonthFirstDate Year Month Day
  | DayFirstDate Year Month Day
  | SomeOtherFormat Year Month Day
  | AndYetAnotherFormat Year Month Day
  | SomeEsotericFormat Year Month Day
  | UghYetAnotherFormat Year Month Day
  | KillMeFormat Year Month Day
```

注意，我们必须为所有这些情况重复 `Year Month Day`。这不太优雅。

让我们看看我们的第二种模型在相同条件下表现如何：

```
data DateFormat
  = YearFirst
  | MonthFirst
  | DayFirst
  | SomeOther
  | AndYetAnother
  | SomeEsoteric
  | UghYetAnother
  | KillMe

type DateParts =
  { year :: Year
  , month :: Month
  , day :: Day
  , format :: DateFormat
  }
```

这个模型似乎比我们的第一个模型能更好地处理额外格式。这不是一个巨大的胜利，但确实是一个胜利。

但是，第二种模型相比第一种有一个巨大的优势，那就是对 case 表达式的需求。当我们使用第一种模型时，我们总是必须编写一个 case 表达式来访问年、月和日：

```
getYear :: DateParts -> Year
getYear = case _ of
  YearFirstDate year _ _ -> year
  MonthFirstDate year _ _ -> year
  DayFirstDate year _ _ -> year
  SomeOtherFormat year _ _ -> year
  AndYetAnotherFormat year _ _ -> year
  SomeEsotericFormat year _ _ -> year
  UghYetAnotherFormat year _ _ -> year
  KillMeFormat year _ _ -> year
```

而 `getMonth` 也会有类似的实现，`getDay` 也是如此。这会产生大量样板代码。

现在，我们可以编写一个单独的函数，将日期转换为 Record：

