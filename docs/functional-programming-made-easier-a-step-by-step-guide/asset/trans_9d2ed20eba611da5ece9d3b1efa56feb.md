

```
{-
Welcome to a Spago project!
You can edit this file as you like.
-}
{ name = "my-project"
, dependencies =
  [ "aff"
  , "arrays"
  , "bifunctors" ②
  , "console"
  , "effect"
  , "either"
  , "foldable-traversable"②
  , "foreign-generic"
  , "foreign"
  , "httpure"
  , "identity" ②
  , "maybe"
  , "newtype" ②
  , "node-buffer"
  , "node-fs-aff"
  , "node-process"
  , "parsing"
  , "posix-types"
  , "prelude"
  , "psci-support"
  , "quickcheck" ①
  , "strings" ②
  , "stringutils"
  , "transformers"
  , "unicode" ②
  , "uuid"
  ]
, packages = ./packages.dhall
, sources = [ "src/**/*.purs", "test/**/*.purs" ]
}
```

① 添加了 quickcheck。

② 添加了错误信息中的包。

现在重新构建应该只会产生警告。

接下来，我们将编写一个名为 userNameSeed 的函数：

```
```purescript
import Random.LCG (Seed)

userNameSeed :: String -> Seed
```
```

> 在导入此内容之前，将包 `purescript-quickcheck` 添加到你的 `spago.dhall` 然后构建服务器。

我们将把每个字符转换为数字，然后将它们相乘得到一个 `Int`。然后我们将使用该 `Int` 调用 `mkSeed` 来获取我们的 `Seed`。

在继续阅读之前完成此函数的代码。提示：你在这里需要使用数组。所以将 String 转换为 Array，然后使用 map 和 fold 来完成任务。

最后的提示是去 Pursuit 上查找 `toCharCode`。

完成后或卡住时，继续阅读。

我们从类型签名开始，它已经给出：

```
```purescript
userNameSeed :: String -> Seed
```
```

接下来，我们将编写等号的左侧：

```
```purescript
userNameSeed :: String -> Seed
userNameSeed userName =
  ???
```
```

现在，我们首先将 userName 转换为 Char 的数组：

```
```purescript
import Prelude

import Data.String.CodeUnits (toCharArray)

userNameSeed :: String -> Seed
userNameSeed userName =
  userName
    # toCharArray
    ???
```
```

> 导入 Prelude 以获取 `#`。

> 导入 `toCharArray`。

> 将 `userName` 从 `String` 转换为 `Array Char`。

现在我们想将每个 Char 转换为其 Int 对应值。由于所有 Unicode 字符都只是整数，我们将使用 toCharCode 来转换它们：

```
import Data.Char (toCharCode) ①

userNameSeed :: String -> Seed
userNameSeed userName =
    userName
        # toCharArray
        <#> toCharCode ②
        ???
```

① 导入 toCharCode。

② 注意我们在这里进行映射，这意味着结果是 Array Int。

现在，我们想要将所有的 Int 相乘：

```
import Data.Foldable (foldl) ①

userNameSeed :: String -> Seed
userNameSeed userName =
    userName
        # toCharArray
        <#> toCharCode
        # foldl (\prod n -> prod * n) 1 ② ③
        ???
```

① 导入 foldl。

② 使用乘法单位元作为初始值，即 1。

③ foldl 的 Lambda 中最左边的参数是累加器，即 prod，即运行中的乘积。

你能看出我们如何大大简化我们的 foldl 吗？

我们可以写成 Point-free：

```
userNameSeed :: String -> Seed
userNameSeed userName =
  userName
    # toCharArray
    <#> toCharCode
    # foldl (*) 1
    ???
```

> 写成 Point-free。

如果这不明显，那么这里是我跳过的步骤：

```
\prod n -> prod * n        (给定)
\prod n -> (*) prod n      (中缀表示法)
\prod -> (*) prod          (ETA 归约)
(*)                         (ETA 归约)
```

最后，我们取我们的 `Int`，即乘法的结果，并使用 `mkSeed` 从中制作一个 `Seed`：

```
import Random.LCG (Seed, mkSeed)

userNameSeed :: String -> Seed
userNameSeed userName =
  userName
    # toCharArray
    <#> toCharCode
    # foldl (*) 1
    # mkSeed
```

> 将 `mkSeed` 添加到导入列表。

> 将我们的 `Int` 转换为 `Seed`。

现在，编写一个名为 `userNameSalt` 的函数，它首先接收一个长度，然后接收一个 `userName` 并生成一个随机的 `String`。

使用 `userNameSeed` 生成一个 `Seed` 并将其连同提供的长度一起传递给 `sample` 以生成一个随机的 `Char` 的 `Array`。然后将 `Array Char` 转换为 `String`。

你需要的导入如下：

```
import Test.QuickCheck.Arbitrary (arbitrary)
import Test.QuickCheck.Gen (sample)
```

① 这是你的生成器，即 Gen a，供 sample 使用（参见 sample 的类型签名）。

使用 Pursuit 查找你可能需要的任何类型签名。编写完 userNameSalt 后返回这里并继续阅读。

以下是类型签名：

```
userNameSalt :: Int -> String -> String
```

它将接收一个长度参数和 userName。

接下来，我们将编写实现的左侧：

```
userNameSalt :: Int -> String -> String
userNameSalt saltLength userName =
  ???
```

我们知道 sample 会给我们一个随机值的数组，所以让我们提醒自己它的类型签名：

```
sample :: ∀ a. Seed -> Size -> Gen a -> Array a
```

我们需要一个种子。我们可以从 userNameSeed 得到它。

接下来，我们需要一个 Size。我们可以从 saltLength 得到它。

接下来，我们需要一个生成器。我们可以通过使用 arbitrary 来获取它。然而，编译器在我们对 sample 的结果使用 fromCharArray 之前不会知道使用哪个 arbitrary。由于 fromCharArray 将 Array Char 转换为 String，编译器可以推断 arbitrary 只能是 Char 的那个。

知道所有这些，如果你没有完成编码，现在就停止并尝试一下。然后继续。

以下是实现上述所有步骤的代码：

```
import Data.String.CodeUnits (toCharArray, fromCharArray) ①

userNameSalt :: Int -> String -> String
userNameSalt saltLength userName =
    fromCharArray
      $ sample (userNameSeed userName) saltLength arbitrary ②
```

① 将 fromCharArray 添加到导入列表。

② 编译器知道 sample 返回的 Array a 必须与 Array Char 统一，因为那是 fromCharArray 所期望的。这意味着它将使用 Char 的 arbitrary 版本，因为 a 与 Char 统一。

现在，我们可以编写一个我们将称为 passwordHash 的函数。但在我们这样做之前，我们需要查找 Node.Crypto.Hash 以搜索一个将接收 String 并创建哈希作为 String 的函数。

现在就做，看看你能找到什么。

我找到了 hex 和 base64。如果记得的话，我们之前找到了这些函数并决定使用 hex。这就是我们编写 hex 解析器的原因。

以下是 hex 的定义：

```
hex :: Algorithm -> String -> Effect String
```

为什么 hex 是一个 Effect？我怀疑，这与它在 Node 中的实现方式有关，可能使用操作系统来获取其随机值。稍微搜索一下可以发现 Node 使用 OpenSSL，而进一步搜索可以发现 OpenSSL 使用系统特定的熵源为随机数生成器播种，例如在 Linux 中它从 /dev/urandom 读取。

由于这相当于从文件中读取，我们应该将此函数移动到 Account 处理程序。

因此，将模块 Manager.Account 中的所有代码（减去 Prelude 的导入）提升并放入 Handler.Account。

以下是我的移动内容：

```
```haskell
import Data.Char (toCharCode)
import Data.Foldable (intercalate, foldl)
import Data.String.CodeUnits (toCharArray, fromCharArray)
import Random.LCG (Seed, mkSeed)
import Test.QuickCheck.Arbitrary (arbitrary)
import Test.QuickCheck.Gen (sample)

userNameSeed :: String -> Seed
userNameSeed userName =
  userName
    # toCharArray
    <#> toCharCode
    # foldl (*) 1
    # mkSeed

userNameSalt :: Int -> String -> String
userNameSalt saltLength userName =
  fromCharArray $ sample (userNameSeed userName) saltLength arbitrary
```
```

> 此导入已在 `Handler.Account` 中，因此我只是将 `foldl` 添加到导入列表。

接下来，将 crypto 添加到你的 `spago.dhall` 然后构建服务器忽略预期的警告。

我们得到错误：

```
```
[error] Some of your project files import modules from packages that are not
in the direct dependencies of your project.
To fix this error add the following packages to the list of dependencies in
your config:
- lcg
```
```

将 `lcg` 包添加到 `spago.dhall` 并重新构建。

在模块 `Handler.Account` 中，使用 hex 和 SHA512 的 Algorithm 编写 `passwordHash`。使 `saltLength` 比 `userName` 长 3 倍。由于 hex 在 Effect Monad 中运行，使用 `liftEffect` 在 hex 上返回 `Aff String`。

完成后，回到这里继续阅读。

我们从其类型签名开始：

```
```haskell
passwordHash :: String -> String -> Aff String
```
```

