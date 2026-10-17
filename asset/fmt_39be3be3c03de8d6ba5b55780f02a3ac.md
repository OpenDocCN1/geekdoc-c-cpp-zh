
① 从 `Data.Array` 导入 `many`。

② 将 `isAlphaNum` 添加到导入列表。

③ `alphaNums` 的类型是 `Array Char`。

现在，我们返回 `alpha` 拼接上 `alphaNums` 的结果：

```
import Data.Array (many, (:)) ①

import Data.String.CodeUnits (fromCharArray) ②

userName :: AccountParserT String

userName = do

  alpha <- satisfy (isAlpha <<< codePointFromChar)

  alphaNums <- many $ satisfy (isAlphaNum <<< codePointFromChar)

  pure $ fromCharArray $ alpha : alphaNums ③
```

① 已将 `( : )` 添加到导入列表。

② 导入 `fromCharArray`。

③ 我们将 `alpha` cons 到 `alphaNums` 前面。

现在，继续编写 `passwordHash`。

看一下 `Node.Crypto.Hash`，看能否找到一种方法计算 Hash，然后将其表示为 `String`。做的时候，准备好说明你为什么做出这样的选择。然后继续阅读，看看我的做法。

对于我们的需求，`hex` 或 `base64` 都可以。但是，我们打算使用 `hex`，因为解析 `Hex String` 比解析 `Base-64 String` 更容易。这和你的选择一致吗？

所以，既然我们已经完成了这个分析，就可以编写一个名为 `passwordHash` 的解析器了。

但首先，为了让这项工作更简单，我们需要编写一个解析 `Hex String` 的解析器。它将接受 `a` 到 `f`（含）以及 `0` 到 `9`。注意我把它们写成小写，因为 `node` 会以小写形式渲染 `hex`。

编写这个解析器，命名为 `hex`，当你遇到障碍或完成时回到这里。

代码如下：

```
import Data.Array (many, some, (:)) ①

hex :: AccountParserT String

hex = fromCharArray <$> (some $ satisfy isHex) ② ③

  where isHex c = (c >= '0' && c <= '9') || (c >= 'a' && c <= 'f') ④
```

① 已将 `some` 添加到导入列表。

② 将 `fromCharArray` 映射到 `Array Char` 上以获得 `String`。

③ 我们期望至少 1 个 `Hex` 值，这就是为什么我们使用 `some`。

④ `isHex` 是一个谓词，用于检查 `c` 是否在 `['0', '9']` 或 `['a', 'f']` 之间（含端点）。

在继续阅读之前，请编写 `passwordHash` 解析器，使其使用 `hex` 解析器。

代码如下：

```
passwordHash :: AccountParserT String

passwordHash = hex
```

接下来，编写一个名为 `boolean` 的解析器，它将解析 `"true"` 或 `"false"` 并返回 `Boolean`。完成后再继续阅读。

首先，类型签名：

```
boolean :: AccountParserT Boolean
```

接下来，我们解析 1 个或多个字符：

```
import Text.Parsing.Parser.String (satisfy, anyChar) ①

boolean :: AccountParserT Boolean

boolean = do

  bool <- fromCharArray <$> some anyChar ②
```

① 已将 `anyChar` 添加到导入列表。

② 使用 `some` 获取包含任意类型字符的 `String`，1 个或多个。

现在，我们将检查 `bool` 是否为有效值：

```
boolean :: AccountParserT Boolean

boolean = do

  bool <- fromCharArray <$> some anyChar

  case bool of

    "true" -> pure true ①

    "false" -> pure false ①

    _ -> ???
```

① 检查有效的 `Boolean` 字符串表示。

对于其余所有情况，我们将 `fail`：

```
import Text.Parsing.Parser (ParserT, fail) ①

boolean :: AccountParserT Boolean

boolean = do

  bool <- fromCharArray <$> some anyChar

  case bool of

    "true" -> pure true

    "false" -> pure false

    _ -> fail "Invalid Boolean" ②
```

① 已将 `fail` 添加到导入列表。

② 否则失败。

现在，编写解析器 `temporaryPassword` 和 `admin`，它们返回值是 `Boolean`，然后继续阅读。

这是它们的简单实现：

```
temporaryPassword :: AccountParserT Boolean

temporaryPassword = boolean

admin :: AccountParserT Boolean

admin = boolean
```

接下来，编写一个名为 `properName` 的解析器，它接受一个大写字母 `alpha` 和零个或多个小写字母 `alpha`。然后继续阅读。

解析器如下：

```
import Data.CodePoint.Unicode (isAlpha, isAlphaNum, isUpper, isLower) ①

properName :: AccountParserT String

properName = do

  first <- satisfy (isUpper <<< codePointFromChar) ②

  rest <- many $ satisfy (isLower <<< codePointFromChar) ③

  pure $ fromCharArray (first : rest) ④
```

① 已将 `isUpper` 和 `isLower` 添加到导入列表。

② 获取第一个 `alpha` 字符，要求是大写。

③ 获取其余的小写 `alpha` 字符，即零个或多个，这就是为什么我们使用 `many`。

④ 将它们组合起来，并将 `Array Char` 转换为 `String`。

现在，编写 `firstName` 和 `lastName` 解析器。

它们是：

```
firstName :: AccountParserT String

firstName = properName

lastName :: AccountParserT String

lastName = properName
```

在继续之前，我想知道你是否和我有同感？这个模块里有大量解析逻辑。似乎值得拆分一下。

继续在 `src` 下创建一个名为 `Parser` 的文件夹，然后在 `Parser` 下创建一个名为 `Account.purs` 的文件，并在继续阅读之前把所有解析函数都提取到那个文件中。

重构后的代码如下：

```
module Parser.Account where ①

import Prelude

import Data.Array (many, some, (:))

import Data.CodePoint.Unicode (isAlpha, isAlphaNum, isUpper, isLower)

import Data.Identity (Identity)

import Data.String.CodePoints (codePointFromChar)

import Data.String.CodeUnits (fromCharArray)

import Text.Parsing.Parser (ParserT, fail)

import Text.Parsing.Parser.String (satisfy, anyChar)

type AccountParserT a = ParserT String Identity a

userName :: AccountParserT String

userName = do

  alpha <- satisfy (isAlpha <<< codePointFromChar)

  alphaNums <- some $ satisfy (isAlphaNum <<< codePointFromChar)

  pure $ fromCharArray $ alpha : alphaNums

hex :: AccountParserT String

hex = fromCharArray <$> (some $ satisfy isHex)

  where isHex c = (c >= '0' && c <= '9') || (c >= 'a' && c <= 'f')

passwordHash :: AccountParserT String

passwordHash = hex

boolean :: AccountParserT Boolean

boolean = do

  bool <- fromCharArray <$> some anyChar

  case bool of

    "true" -> pure true

    "false" -> pure false

    _ -> fail "Invalid Boolean"

temporaryPassword :: AccountParserT Boolean

temporaryPassword = boolean

admin :: AccountParserT Boolean

admin = boolean

properName :: AccountParserT String

properName = do

  first <- satisfy (isUpper <<< codePointFromChar)

  rest <- many $ satisfy (isLower <<< codePointFromChar)
```

```
pure $ fromCharArray (first : rest)

firstName :: AccountParserT String

firstName = properName

lastName :: AccountParserT String

lastName = properName
```

① 确保模块名正确。

现在，我们可以编写一个名为 `accountParser` 的函数，它将解析每个元素，后面跟一个逗号。试一试，看看在继续阅读之前你能完成多少。

下面是我们作为参考的 `bootstrapAccount`：

```
-- userName,passwordHash,temporaryPassword,admin,firstName,lastName

bootstrapAccount :: String

bootstrapAccount = "admin,placeholder,true,true,Joe,Admin"
```

如果你卡住了，这是第一部分：

```
accountParser :: AccountParserT Account

accountParser = do

  userName' <- userName # comma ① ② ③

  ???
```

① 这里的 `comma` 将是一个我们尚未编写的解析器，它会接收一个 `AccountParserT`，并将其与一个解析单个逗号的解析器组合。但是，`comma` 不会返回逗号本身，而是返回传入的解析器所解析的内容。

② 使用带撇号的方式为解析结果命名，即 `userName'`，因为解析器本身也叫 `userName`，我们不想遮蔽它。

③ 在末尾使用 `#` 调用 `comma`，因为代码读取的顺序与我们解析的顺序一致，即先解析 `userName`，再解析逗号。

先停在这里，看看你能完成多少再回来。

下面是其余各列的代码：

```
accountParser :: AccountParserT Account

accountParser = do

    userName' <- userName # comma

    passwordHash' <- passwordHash # comma

    temporaryPassword' <- temporaryPassword # comma

    admin' <- admin # comma

    firstName' <- firstName # comma

    lastName' <- lastName ①

    ???
```

① 注意这里没有调用 `comma`。因为这是这一行的末尾。

现在，添加代码返回一个 `Account`。在继续阅读之前，请查看 `Account` 数据构造器，了解如何实现这一点。

`Account` 的构造代码如下：

```
import Entity.Account (Account(..)) ①

accountParser :: AccountParserT Account

accountParser = do

    userName' <- userName # comma

    passwordHash' <- passwordHash # comma

    temporaryPassword' <- temporaryPassword # comma

    admin' <- admin # comma

    firstName' <- firstName # comma

    lastName' <- lastName

    pure $ Account ②

        { userName: userName'

        , passwordHash: passwordHash'

        , temporaryPassword: temporaryPassword'

        , admin: admin'

        , firstName: firstName'

        , lastName: lastName'

        }

where

    comma p = ???
```

① 引入 `Account` 数据构造器。

② 这里不得不使用详细语法，因为局部名称和字段名与解析器名称冲突。我们可以重命名解析函数来精简代码，但可能只是半斤八两。

现在，编写 `comma` 解析器组合子，即一个接受解析器并返回另一个解析器的函数。

提示：它将获取给定的解析器，即 `p`，并调用该解析器然后解析逗号，返回原始解析器的结果。查看 `Text.Parsing.Parser.String` 以找到一个解析特定字符的解析器。

在继续之前先试试。

让我们一行一行地写逗号部分：

```
where

    comma p = do

        v <- p

        ???
```

在这里我们将解析器 `p` 的结果捕获到 `v` 中。

现在，我们需要解析一个特定字符，即逗号。我们可以使用 `Text.Parsing.Parser.String` 中的 `char` 来实现：

```
where

    comma p = do

        v <- p

        void $ char ','

        ???
```

1 单引号是 `Char` 字面量。

我们丢弃这个第二个解析结果。

最后，我们返回第一个解析器的结果：

```
where

    comma p = do

        v <- p

        void $ char ','

        pure v
```

现在，这可行但过于复杂。我们想要应用第一个。你还记得 `applyFirst` 的运算符吗？

如果不记得，在 Pursuit 中查找并使用 `applyFirst` 的运算符重写我们的 `do` 块。然后继续阅读。

这里是使用 `applyFirst` 运算符的最终结果：

```haskell
import Text.Parsing.Parser.String (satisfy, anyChar, char)

accountParser :: AccountParserT Account
accountParser = do
  userName' <- userName # comma
  passwordHash' <- passwordHash # comma
  temporaryPassword' <- temporaryPassword # comma -- COMPILER ERROR!!
  admin' <- admin # comma
  firstName' <- firstName # comma
  lastName' <- lastName
  pure $ Account
    { userName: userName'
    , passwordHash: passwordHash'
    , temporaryPassword: temporaryPassword'
    , admin: admin'
    , firstName: firstName'
    , lastName: lastName'
    }
  where
    comma p = p <* char ','
```
