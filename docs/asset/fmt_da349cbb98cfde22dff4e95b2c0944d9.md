
+   1. 将 `char` 添加到导入列表中。
+   2. 使用 `applyFirst`，即 `<*`，丢弃第二个计算的结果。

这里是编译器错误：

![](img/8c0e9b687c62642e828ccb5481e11313_1354_0.png)

你能看出我的错误吗？

它无法将 `Boolean` 与 `comma` 调用的 `String` 相关联。这有帮助吗？

如果没有，那么问问自己 `comma` 的类型是什么。你能写出 `comma` 的类型签名吗？

让我们仔细想想。`comma` 接受类型为 `AccountParserT a` 的解析器。多态类型参数，

a，应该是一个巨大的线索给我们。comma 是一个多态函数。我们需要添加一个显式的类型签名，否则编译器会过度特化其类型。

如果我们的所有解析器都解析字符串，这种过度特化是可以的，但它们不是。temporaryPassword 解析一个布尔值。这些就是编译器抱怨的 2 个类型。

通过为 comma 添加类型签名来修复我的错误，然后返回这里。

这是最终代码：

```
accountParser :: AccountParserT Account

accountParser = do

    userName' <- userName # comma

    passwordHash' <- passwordHash # comma

    temporaryPassword' <- temporaryPassword # comma

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

        comma :: ∀ a. AccountParserT a -> AccountParserT a ①

        comma p = p <* char ','
```

① `comma` 在 a 上是多态的，因此需要显式的类型签名以防止编译器过度特化。

我们现在有一个解析器，可以解析 CSV 文件的单行。

完成之后，我们可以将注意力转回 Handler.Account 中的 loadAccounts。这里是我们停下的地方：

```haskell
loadAccounts :: Aff (Array Account)
loadAccounts = do
  exists <- try $ exists accountsFile
  when (isLeft exists)
    $ writeTextFile ASCII accountsFile bootstrapAccount
  -- COMPILER WARNING!!
  accountLines <- lines <$> readTextFile ASCII accountsFile
  pure []
```

❶ `accountLines` 是来自 Accounts 文件的行。

我们可以将我们的 `accountParser` 应用于文件的每一行，即 `accountLines` 的每个条目。

为此，我建议你将这段代码孵化在一行单独的代码中，如下所示：

```
loadAccounts :: Aff (Array Account)
loadAccounts = do
  exists <- try $ exists accountsFile
  when (isLeft exists)
    $ writeTextFile ASCII accountsFile bootstrapAccount
  accountLines <- lines <$> readTextFile ASCII accountsFile
  let x = accountLines :: ?x
  pure []
```

❶ 这是我们的孵化行。一旦类型孔给出我们想要的类型，我们就会将其整合到我们的函数中。

❷ 类型孔是 `Array String`。

注意类型孔在那里帮助我们，因为我们慢慢构建这行的代码。

现在，我们想用 `accountParser` 解析每一行。但我们如何运行解析器呢？

去 Pursuit 搜索 runParserT 看看你得到什么。

我得到的是：

![](img/8c0e9b687c62642e828ccb5481e11313_1356_0.png)

我们可以看到 runParserT 接受一个要解析的字符串和一个 ParserT。我们都有这两样东西。我们有来自 Accounts 文件的行，我们有 accountParser。

继续在孵化行中添加代码，以在 Array，即 accountLines 中的每一行上运行 accountParser。然后继续阅读。

我们将通过在 accountLines 上映射 runParserT 来实现这一点：

```
import Parser.Account (accountParser) ①

import Text.Parsing.Parser (runParserT)

loadAccounts :: Aff (Array Account)

loadAccounts = do

  exists <- try $ exists accountsFile

  when (isLeft exists)

    $ writeTextFile ASCII accountsFile bootstrapAccount

  accountLines <- lines <$> readTextFile ASCII accountsFile

  let x = flip runParserT accountParser <$> accountLines :: ?x ② ③ ④

  pure []
```

① 添加这些导入。

② 我们翻转了 runParserT，以便在字符串解析之前提供解析器参数。

③ 我们映射每个 Array 中的行。

④ 类型孔是 Array (Identity (Either ParseError Account))。

我们现在有一个 Identity 的 Array，所以继续添加代码来解包元素，然后再继续阅读。

我们将简单地将 unwrap 与 runParserT 组合。我们可以通过 Functor 定律做到这一点，而无需再次调用 map：

```
import Data.Newtype (unwrap) ①

loadAccounts :: Aff (Array Account)

loadAccounts = do

  exists <- try $ exists accountsFile

  when (isLeft exists)

    $ writeTextFile ASCII accountsFile bootstrapAccount

  accountLines <- lines <$> readTextFile ASCII accountsFile

  let x = unwrap

        <<< flip runParserT accountParser <$> accountLines :: ?x ② ③

  pure []
```

① 导入 unwrap。

② 将 unwrap 与 flip runParserT accountParser 组合以消除 Identity。请记住 Identity 有一个 Newtype 实例，这就是为什么我们可以调用 unwrap。

③ 类型孔是 Array (Either ParseError Account)。

现在，我们在外部有一个 Array，内部有一个 Either。但我们实际上希望它们是相反的。你还记得如何交换它们吗？

你还记得一个函数，它接受类型为 t (m a) 的 Traversable 并返回 m (t a) 吗？如果不记得，去 Pursuit 查找 t (m a) -> m (t a) 看看你能找到什么。

当我这样做时，我找到了 sequence。所以继续在 Either 的 Array 上添加 sequence 的调用，看看类型孔会给你什么。然后返回这里。

这里是更改：

```
import Data.Traversable (sequence) ①

loadAccounts :: Aff (Array Account)

loadAccounts = do

  exists <- try $ exists accountsFile

  when (isLeft exists)

    $ writeTextFile ASCII accountsFile bootstrapAccount

  accountLines <- lines <$> readTextFile ASCII accountsFile

  let x = sequence $ unwrap

      <<< flip runParserT accountParser <$> accountLines :: ?x ②

  pure []
```

① 导入 sequence。

② 类型孔是 Either ParseError (Array Account)。

我们在这里孵化的这行代码的类型几乎是我们希望从这个函数返回的类型。

但我们有一个 Either 的事实应该提醒我们我在为 loadAccounts 编写类型签名时目光短浅。我忘记了它可能失败的事实。

通过更改类型签名来反映我们可以用 ParseError 失败来修复我的错误。不要忘记也更改返回值以匹配我们新的返回类型。在阅读进一步内容之前完成此操作。

这里是类型签名更改：

```
import Data.Either (Either, isLeft) ①

import Text.Parsing.Parser (ParseError, runParserT) ②

loadAccounts :: Aff (Either ParseError (Array Account)) ③

loadAccounts = do

    exists <- try $ exists accountsFile

    when (isLeft exists)

        $ writeTextFile ASCII accountsFile bootstrapAccount

    accountLines <- lines <$> readTextFile ASCII accountsFile

    let x = sequence $ unwrap

        <<< flip runParserT accountParser <$> accountLines :: ?x

    pure $ pure [] ④
```

① 将 `Either` 添加到导入列表中。

② 将 `ParseError` 添加到导入列表中。

③ 更改了类型签名，以反映我们可能会因 `ParseError` 而失败。

④ 不得不将空数组包装在 `Right` 中，以匹配新的类型签名。这行代码目前只是为了暂时让编译器满意。

现在再看一下类型洞 `Either ParseError (Array Account)`，我们距离这个函数现在返回的类型只有一步之遥，即 `Aff (Either ParseError (Array Account))`。

取出我们的孵化行，并用它替换最后一行。别忘了它仍然需要用 `Aff` 包装。

以下是最终的修改：

```
loadAccounts :: Aff (Either ParseError (Array Account))

loadAccounts = do

    exists <- try $ exists accountsFile

    when (isLeft exists)

        $ writeTextFile ASCII accountsFile bootstrapAccount

    accountLines <- lines <$> readTextFile ASCII accountsFile

    pure $ sequence ①

        $ unwrap <<< flip runParserT accountParser <$> accountLines ②
```

① 添加了 `pure`，将其包装在 `Aff` 中。

② 用孵化行替换了最后一行，去掉了 `let x=` 和 `:: ?x` 部分。

既然我们已经完成了 `loadAccounts`，让我们回顾一下 Account Handler 应该做的事情清单：

- 创建一个初始账户文件，其中包含一个带有临时密码的引导账户（Bootstrap Account）
- 从文件中加载所有账户
- 向账户文件追加一个新账户

我们已经完成了清单上的前两项。剩下的就是向账户文件追加一个新账户。

这个操作有哪些技术障碍？思考需要完成的操作，然后想想哪些是你知道怎么做的，哪些是你不知道的。

在阅读下一节之前，先在脑海中列出你必须克服的障碍。

## 28.6.2. 编写 `createAccount` 代码

我首先想到的是追加操作。我们如何向现有文件的末尾追加内容？这是第一个技术障碍。

接下来，我们需要一种方法，将一个 `Account` 转换为一行 CSV（逗号分隔值）文件。与其说这是一个技术障碍，不如说是一个我们需要编写的函数。

我们需要做以下几件事：

- 弄清楚如何向现有文件追加内容
- 取一个 `Account` 并生成一个 `String`，该字符串是 CSV 账户文件中的一行

让我们从向现有文件追加内容开始。

因为我们在 Node 环境下运行，让我们先看看在 Node 中如何做到这一点。用类似 `Node API append file` 或 `Node append` 之类的搜索词在 Google 上搜索 Node API。

一旦你找到了该函数的名称，然后前往 `Pursuit` 查找相同的名称，看看能否在 `Node.FS.*` 模块中找到相关内容。然后回到这里。

以下是我找到的内容：

![](img/8c0e9b687c62642e828ccb5481e11313_1360_0.png)

当我在 Pursuit 中搜索 `appendFile` 时，我找到了 3 个不同的版本，但我感兴趣的是来自 `Node.FS.Aff` 的以下这个：

```
appendFile

appendFile :: FilePath -> Buffer -> Aff Unit

Appends the contents of a buffer to a file.

purescript-node-fs-aff Node.FS.Aff
```

点击这个链接会跳转到：

```
# appendFile

Source

appendFile :: FilePath -> Buffer -> Aff Unit

Appends the contents of a buffer to a file.

# appendTextFile

Source

appendTextFile :: Encoding -> FilePath -> String -> Aff Unit

Appends text to a file using the specified encoding.
```

现在，`appendFile` 需要的是一个 `Buffer`，如果你试图弄清楚如何把一个 `String` 变成 `Buffer`，你最终会钻进一个兔子洞。但是，如果我们看看 `appendFile` 的正下方，就会发现 `appendTextFile`：

```
appendTextFile :: Encoding -> FilePath -> String -> Aff Unit
```

这正是我们需要的。

现在，我们已经克服了技术障碍，可以编写一个函数来创建账户了。我们打算将其命名为 `createAccount`，并放在 `Handler.Account` 模块中。

我们打算把将 `Account` 转换为 CSV 字符串这一过程委托给另一个函数，我们将其命名为 `accountToCSV`。我们之后会编写这个函数，但现在先写一个临时替代：

```
accountToCSV :: Account -> String

accountToCSV = const ""
```

添加这个临时替代，然后在 `Handler.Account` 中编写 `createAccount`。当你完成或遇到困难时，回到这里继续阅读。

以下是 `createAccount` 的类型签名：

```
createAccount :: Account -> Aff (Either String Unit) ①
```

① 因为 `appendTextFile` 在 `Aff` 中运行，所以这里也在 `Aff` 中运行。

我们接收一个 `Account`，在成功时返回空值，在出错时返回一个文件 I/O 错误（即一个 `String`）。这明显表明我们的函数具有副作用，确实如此。它的副作用是写入文件。

我们需要做的一件事是修改 `CreateUserFailureReason`，让它包含这个文件 I/O 错误。这样我们就能向客户端反馈为什么无法写入账户文件。

让我们对 `CreateUserFailureReason` 做如下修改：

```
data CreateUserFailureReason

  = NotAuthorized

  | NotAuthenticated

  | AlreadyExists
```
