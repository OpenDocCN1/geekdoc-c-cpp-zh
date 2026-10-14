

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
  | FileIOError String ①
```

① 带有一个原因字符串的文件 I/O 错误。

需要指出非常重要的一点：这个函数返回的是 `String`，而不是 `CreateUserFailureReason`。这是关注点分离的一个典型例子。

Account Handler 不应该知道关于 API 或 API Handler 的任何事情。然而，API Handler 必须知道 Account Manager，因为它会调用 `createAccount`。

所以，API Handler 间接耦合到 Account Handler，但 Account Handler 在我们的设计中不依赖于任何东西，我们希望保持这种状态。

从 `createAccount` 返回的 `String` 将由 API Handler 使用我们新的数据构造器 `FileIOError` 转换为 `CreateUserFailureReason`。

好的，现在我们准备好继续编写 `createAccount`：

```
import Node.FS.Aff (exists, writeTextFile
, readTextFile, appendTextFile)

createAccount :: Account -> Aff (Either String Unit)
-- COMPILER ERROR!!
createAccount account
  = appendTextFile ASCII accountsFile $ accountToCSV account
```

① 将 `appendTextFile` 添加到导入列表中。

② 追加到 CSV。

编译器报错是意料之中的，因为我们还没完成，但这个错误也很有帮助：

![](img/8c0e9b687c62642e828ccb5481e11313_1363_0.png)

所以，`appendTextFile` 返回的是 `Aff Unit`，但 `createAccount` 应该返回 `Aff (Either String Unit)`。

为了修复这个问题，我们将添加 `try` 来捕获异常并将其转换为 `Either`：

```
try :: ∀ e m a. MonadError e m => m a -> m (Either e a)
```

以下是相应的修改：

```
createAccount :: Account -> Aff (Either String Unit)
-- COMPILER ERROR!!
createAccount account
  = try $ appendTextFile ASCII accountsFile $ accountToCSV account
```

以及新的编译器错误：

![](img/8c0e9b687c62642e828ccb5481e11313_1364_0.png)

你觉得编译器现在在抱怨什么？如果你不知道，那就添加一个类型洞，以便我们能够看出我们写的是什么类型。

完成后或卡住时再回到这里。

以下是修改：

```
createAccount :: Account -> Aff (Either String Unit)
createAccount account =
  let x = try $ appendTextFile ASCII accountsFile
    $ accountToCSV account :: ?x ①
  in pure $ pure unit ② ③
```

① 将我们的代码设置为一个带类型洞的哑元变量 `x`，以便我们能看到这是什么类型。

② 注意 `in` 关键字。那是因为我们不在 `do` 代码块中。

③ `pure $ pure unit` 是一个类型正确的哑元返回值。

类型洞如下：

![](img/8c0e9b687c62642e828ccb5481e11313_1364_1.png)

由此应该可以清楚地看出编译器之前抱怨的是什么。我们编写的代码类型是 `Aff (Either Error Unit)`，但 `createAccount` 应该返回 `Aff (Either String Unit)`。

这就是为什么我们在 `Error` 和 `String` 之间出现类型不匹配。那么，我们如何将 `Error` 转换为 `String` 呢？

