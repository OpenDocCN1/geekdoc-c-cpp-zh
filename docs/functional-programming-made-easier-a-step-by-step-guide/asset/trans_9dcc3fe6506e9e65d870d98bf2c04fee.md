

```purescript
red :: Style
red = "red"

bold :: Style
bold = "bold"

test :: Effect Unit
test = log $ chalk [ red, bold ] "Test" <> chalk [ red ] "Test"
```

虽然这样更好，但它并不能阻止以下情况：

```purescript
test :: Effect Unit
test = log $ chalk [ red, bold ] "Test"
    <> chalk [ red, "crash" ] "Test"
```

① 添加了 "crash"。

我们需要一个不是 String 的 Type，但可以被转换为 String 供 chalk 使用。我们该如何实现？

如果你在考虑使用 newtype，让我们看看它如何工作：

```purescript
newtype Style = Style String

red :: Style
red = Style "red"

bold :: Style
bold = Style "bold"
```

这确实能通过 newtype，即 Style，保护我们免受随意的 String 影响。

但我们如何将一个 Array Style 传递给期望 Array String 的 Javascript 函数呢？

很久以前我们在学习 newtype 时，我提到过编译器可以对 newtype 进行一些优化。其中一个优化是 newtype 在运行时内部表示为底层 Type。

我们可以通过更改测试代码并添加以下内容来看到这一点：

```purescript
import Debug (spy)

newtype Style = Style String

red :: Style
red = Style "red"

test :: Effect Unit
test = do
  let x = spy "red" red
  pure unit
```

① 导入 spy 并将调试添加到 spago.dhall 中。

② 打印 red 的内部表示。

这会输出：

```text
red: 'red'
```

red 被存储为一个 Javascript String。这意味着我们不需要对 Style 做任何特殊处理，因为它只是一个 newtype。这也意味着如果我们传递一个 Array Style，它会将 Array String 传递给我们的 Javascript 函数。

我已在 GitHub Gist 上设置了一个包含所有有效 Styles 的 PureScript 模块。你可以在此链接找到它，ChalkStyles.purs。点击它。

如果你无法访问 GitHub，这里是代码：

```purescript
module ChalkStyles where

newtype Style = Style String

black :: Style
black = Style "black"

red :: Style
red = Style "red"

green :: Style
green = Style "green"

yellow :: Style
yellow = Style "yellow"

blue :: Style
blue = Style "blue"

magenta :: Style
magenta = Style "magenta"

cyan :: Style
cyan = Style "cyan"

white :: Style
white = Style "white"

blackBright :: Style
blackBright = Style "blackBright"

gray :: Style
gray = Style "gray"

grey :: Style
grey = Style "grey"

redBright :: Style
redBright = Style "redBright"

greenBright :: Style
greenBright = Style "greenBright"

yellowBright :: Style
yellowBright = Style "yellowBright"

blueBright :: Style
blueBright = Style "blueBright"

magentaBright :: Style
magentaBright = Style "magentaBright"

cyanBright :: Style
cyanBright = Style "cyanBright"

whiteBright :: Style
whiteBright = Style "whiteBright"

bgBlack :: Style
bgBlack = Style "bgBlack"

bgCyanBright :: Style
bgCyanBright = Style "bgCyanBright"

bgWhiteBright :: Style
bgWhiteBright = Style "bgWhiteBright"

reset :: Style -- Resets the current color chain.
reset = Style "reset"

bold :: Style -- Make text bold.
bold = Style "bold"

dim :: Style -- Emitting only a small amount of light.
dim = Style "dim"

italic :: Style -- Make text italic. (Not widely supported)
italic = Style "italic"

underline :: Style -- Make text underline. (Not widely supported)
underline = Style "underline"

inverse :: Style -- Inverse background and foreground colors.
inverse = Style "inverse"

hidden :: Style -- Prints the text, but makes it invisible.
hidden = Style "hidden"

strikethrough :: Style -- Puts a horizontal line through the center of the text. (Not widely supported)
strikethrough = Style "strikethrough"

visible :: Style -- Prints the text only when Chalk has a color level > 0. Can be useful for things that are purely cosmetic.
visible = Style "visible"
```

将此文件添加到你的项目中。确保将其命名为 `ChalkStyles.purs` 并放在 `src` 下。

然后在继续之前更改你的测试代码以使用它。

首先要做的是从 `Ch27a.purs` 中删除以下内容：

```purescript
type Style = String
```

然后导入 ChalkStyles：

```purescript
import ChalkStyles (Style, bold, red)
```

最后，在我们的测试代码中将 Strings 更改为 Styles：

```purescript
test :: Effect Unit
test = log $ chalk [ red, bold ] "Test" <> chalk [ red ] "Test"
```

现在再次运行它，它应该产生相同的输出。

好，现在以以下方式更改你的程序：

```purescript
import ChalkStyles (Style(..), bold, red)

test :: Effect Unit
test = log $ chalk [ red, bold ] "Test"
    <> chalk [ red, Style "crash" ] "Test"
```

① 包含 Style 的 Data Constructors。

② 添加我们自己的 Style，它不受支持并且会使我们的程序崩溃。

运行测试代码，看看会发生什么。

它崩溃了。

问题是我们有访问 Style Data Constructor 的权限，可以创建任何我们喜欢的 Style，即使 chalk 不支持。

那么，我们如何防止这种情况？

要修复这个问题，我们需要导出 Type 和所有有效的 styles，但 NOT Style Data Constructor：

```purescript
module ChalkStyles
  ( Style
  , black
  , red
  , green
  , yellow
  , blue
  , magenta
  , cyan
  , white
  , blackBright
  , gray
  , grey
  , redBright
  , greenBright
  , yellowBright
  , blueBright
  , magentaBright
  , cyanBright
  , whiteBright
  , bgBlack
  , bgRed
  , bgGreen
  , bgYellow
  , bgBlue
  , bgMagenta
  , bgCyan
  , bgWhite
  , bgBlackBright
  , bgGray
  , bgGrey
  , bgRedBright
  , bgGreenBright
  , bgYellowBright
  , bgBlueBright
  , bgMagentaBright
  , bgCyanBright
  , bgWhiteBright
  , reset
  , bold
  , dim
  , italic
  , underline
  , inverse
  , hidden
  , strikethrough
  , visible
  )
where
```

① 导出 Type 但不导出 Data Constructor。如果这一行是 `Style(..)`，那么 Data Constructors 也会被导出。

我已为此改进设置了另一个 GitHub Gist，链接在此，ChalkStylesExports.purs。

点击链接并将 ChalkStylesExports.purs 的内容复制并粘贴到你的 ChalkStyles.purs 中。

如果你无法访问 GitHub，那么上面代码是唯一更改的内容。

我们现在有了调用 chalk 的类型安全方式。调用 chalk 以导致我们的程序崩溃的方式是 IMPOSSIBLE。

对你的代码进行以下更改：

```purescript
import ChalkStyles (Style, bold, red, dim, strikethrough)
import Data.Array ((:))

test :: Effect Unit
test = do
  let colorful styles = chalk $ red : styles
  log $ colorful [ bold, strikethrough ] "Test"
    <> colorful [] "Test" <> colorful [ dim ] "Test"
```

① 由于我们不再有访问其 Data Constructor 的权限，因此从 Style 中移除了 (..)。

② 添加了 dim 和 strikethrough。

③ 导入 (:)。

④ 提取了公共 styles。

⑤ 将 strikethrough 添加到第一个 "Test"。根据 chalk 文档，strikethrough 并不是广泛支持的。因此，根据你运行的系统，你可能看不到此样式。

⑥ 添加了一个额外的 "Test"，它是 dim 的。

你的输出应该如下所示：

![](img/8c0e9b687c62642e828ccb5481e11313_1241_0.png)

如果 strikethrough 没有显示出来也不用担心。并非所有终端程序都支持此功能。iTerm2 支持此功能。

## 27.2. 在 Javascript 中反转 JSON 键

现在我们知道了如何从 PureScript 调用 Javascript，我们将回到 Echo Server 项目。这次我们将通过使用 Javascript 来反转 Echo Server 发送回给我们的 JSON 中的键。我们将从我们在第 25 章最后所做的事情开始。

所以创建一个名为 Ch27b.purs 的新文件，然后将 Ch25b.purs 中的所有代码复制并粘贴到其中。然后保存它。

现在，关闭 Ch25b.purs 并确保你在 Ch27b.purs 中工作。

编辑模块名使其为 Ch27b。

然后删除所有 Argonaut 导入：

```purescript
import Data.Argonaut (class DecodeJson, JsonDecodeError(..)
    , decodeJson, (..:))

import Data.Argonaut.Decode.Decoders (decodeJObject)
```

然后导入 Decode Typeclass：

```purescript
import Foreign.Generic.Class (class Encode, class Decode)
```

① 将 class Decode 添加到导入列表中。

你现在应该在所有 DecodeJson 实例派生上出现错误，例如：

```purescript
derive newtype instance decodeJsonCentimeters :: DecodeJson Centimeters
```

这可以通过简单地将其更改为以下内容来修复：

```purescript
derive newtype instance decodeCentimeters :: Decode Centimeters
```

① 将 decodeJsonCentimeters 重命名为 decodeCentimeters。

② 将 DecodeJson 重命名为 Decode。

现在，编辑所有其他类似的 derive 声明。

我们接下来要攻击的一批错误是手写的 Argonaut 解码器，例如。

