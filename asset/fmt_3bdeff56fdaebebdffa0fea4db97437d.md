
`randomGenerator` `valueType` `pred`

```
① 这会通过 JavaScript 调度一个回调，这意味着在本次调用返回之前，我们的代码不会退出。
```

注意对 `delayRandom` 的调用。在 `delayRandom` 中，我们调用了 `delay`，而 `delay` 最终会调用 JavaScript 的 `setTimeout`。这会让我们有一个 JavaScript 知道的未完成回调，从而让程序保持存活。

一旦我们从 `delayRandom` 返回，就会递归，要么退出，要么再次调用 `delayRandom`，从而继续让程序存活。

在 `logger` 的情况下，存在一个只有 `AVar` 库才知道的待处理回调。JavaScript 对此毫不知情。所以，当所有 Publishers 都退出时，JavaScript 运行时发现没有未完成的请求，便立即退出了。

对于这类古怪的问题，我并不太喜欢在后端使用 PureScript。如果有机会，我几乎总会选择用 Haskell 编写后端。但如果你打算用 PureScript 编写并在 Node 下运行，就需要把这类问题牢记在心。

## 第 24 章 JSON 与 Ajax

在许多与后端服务器通信的浏览器应用中，JSON 被用作调用 API 的格式。这通常通过 HTTP POST 完成，而这也是我们在接下来的章节中开发应用时要采用的方式。

PureScript 中有一个用于 HTTP 请求的权威库，名为 `purescript-affjax`。JSON 编码和解码有两大主要方式。

第一种方式是使用 PureScript 的泛型表示（Generic Representation），将 PureScript 类型直接映射到 JavaScript 类型。这是使用起来最简单的库，内置于 `Foreign.Generic` 模块中。它的简单性既是优点也是缺点，例如，你无法对 `Either` 或 `Tuple` 进行编码。

另一种方式是使用一个灵活得多的库，名为 *Argonaut*，它可以在 `purescript-argonaut` 包中找到。由于我们已经编写了自己的 `Parser`，JSON 解码对我们来说会非常熟悉。我们可以使用 Applicative 和 Monadic 代码来编写解码器，这与我们编写 Applicative 和 Monadic 解析器的方式非常相似。

### 24.1. 泛型 JSON 的编码与解码

泛型 JSON 编码和解码意味着我们不必编写代码来显式地编码和解码类型。虽然这听起来好得令人难以置信，但它实际上在许多情况下都是可行的。不过，它确实有自己的局限性。

你只能对以下类型进行编码：

```
Void ①

Unit

Foreign ②

String

Char

Boolean

Number

Identity a

Array a

Maybe a

Object v

Record r
```

① 实际上永远无法被创建。

② `Foreign` 表示一个 JSON 数据块，也就是某些我们不想显式编码或解码的 JSON 数据。

注意 `Either` 并不在其中。因此，如果你的类型中包含 `Either`，就无法使用泛型 JSON 编码或解码。这时就该 `Argonaut` 登场了。

你也可以创建一个与 Either 同构的 Type，只要它的 Types 在上述列表中即可。另一种实现方式是使用 newtype，因为我们可以在 Either 中正常找到的所有底层行为上派生。

此外，如果你需要完全控制表示你的 Type 的 JSON 对象的构造，例如你正在与遗留系统或你无法控制的系统交互，那么你很可能将无法使用 Generic JSON 编码和解码。

这是因为 Generic JSON 编码使用非常特定的 JSON 结构，很可能与你的遗留系统的 API 不匹配。

再次，这就是 Argonaut 派上用场的地方。但对于所有其他情况，这个库可以大大消除样板代码。

并且在库能够覆盖你需要编码或解码的 90% 的 Types 的情况下，你可以使用 Argonaut 来处理剩下的 10%。因此，你的负担仍然大大减轻。

Generic JSON 编码和解码可以在以下模块中找到：

- `Foreign`
- `Foreign.Generic`
- `Foreign.Generic.Class`

让我们一次看一个这些模块，从 Foreign 开始。

#### 24.1.1. Foreign Module

关于 Foreign 模块包含内容的解释是：

```
This module defines types and functions for working with foreign data.
```

但什么是 foreign data？

由于 PureScript 使用 Javascript，所以 foreign data 指的就是这个。

从这个模块中，我们马上关心的只有一件事，那就是 Type 别名，`F`。它代表在处理 Javascript 数据时一个或多个错误。

以下是它的定义：

```
type F = Except MultipleErrors
```

记住 `Except` 是由 `ExceptT` 和 `Identity` Monad 构建的。有一个名为 `runExcept` 的函数可以运行这个迷你 Stack。它会为我们解包 Identity Context 中的值。

以下是 `MultipleErrors` 的 Type 别名定义：

```
type MultipleErrors = NonEmptyList ForeignError
```

这是一个至少包含 1 个 `ForeignError` 的列表。但什么是 `ForeignError`？

以下是它的定义：

```
data ForeignError
  = ForeignError String
  | TypeMismatch String String
  | ErrorAtIndex Int ForeignError
  | ErrorAtProperty String ForeignError
```

这些是你从 JSON 解码中可以期望得到的错误。`ForeignError` 有一个 `Show` 实例，允许我们将 JSON 解码错误写入日志。

#### 24.1.2. Foreign.Generic Module

该模块包含 Generic JSON 编码器和解码器，允许我们在无需编写一行代码的情况下将我们 Types 的编码和解码委托出去。

它还包含用于将 Types 编码为字符串的函数，即 `encodeJSON`，以及用于将字符串解码为 Types 的函数，即 `decodeJSON`。

请记住，如果你在 Pursuit 中搜索这些函数，你会找到 2 个版本。我们在这里关心的版本全部使用大写的 JSON。

另一个版本是 `encodeJson` 和 `decodeJson`。它们是 Argonaut 库的一部分，我们稍后会深入研究。

#### 24.1.3. Foreign.Generic.Class Module

从该模块中，有 2 个 Typeclasses 特别重要，即 `Encode` 和 `Decode`。如果我们需要创建一个想要为我们编码或解码为 JSON 的 Type，我们需要为这些 Typeclasses 创建实例。

Generics 的美妙之处在于它允许我们委托给 `Foreign.Generic` 模块中的 `genericEncode` 和 `genericDecode`。

让我们想象我们有一个 Type：

```
data Portion = Bit | Chunk | Part
```

接下来，我们可以为我们的 Type 派生 Generic：

```
data Portion = Bit | Chunk | Part
derive instance genericPortion :: Generic Portion _
```

现在，我们可以利用 Generic JSON 编码和解码器为我们的 Type 创建一个 Encode 和 Decode 实例：

```
import Foreign.Generic (genericEncode, genericDecode, defaultOptions)

instance encodePortion :: Encode Portion where
    encode = genericEncode defaultOptions ①

instance decodePortion :: Decode Portion where
    decode = genericDecode defaultOptions ①
```

① 我们正在使用默认的 Options。稍后会详细介绍。

让我们编码我们的 Sum Type，`Portion`：

```
test :: Effect Unit
test = log $ encodeJSON Part ①
```

① 打印 `{"tag":"Part"}`。

注意键 `tag`。这种标记让解码器知道要调用哪个数据构造函数。

该模块中还有另一个重要元素，那就是 `Options` 类型和 `defaultOptions`。你可以看到我们在 `encodePortion` 和 `decodePortion` 中使用了 `defaultOptions`。

让我们详细查看它们。首先，让我们查看 `Options` 类型：

```
type Options =
    { sumEncoding :: SumEncoding ①
    , unwrapSingleConstructors :: Boolean ②
    , unwrapSingleArguments :: Boolean ③
    , fieldTransform :: String -> String ④
    }
```

① 这控制 Sum Types 的编码方式。我们稍后会深入探讨。

② 如果为 true，则具有单个数据构造函数的 Type 不会被标记。

③ 如果为 false，则具有单个类型参数的数据构造函数的 Type 将具有其参数

下面是一个测试程序，看看默认情况下我们得到什么：

```
test :: Effect Unit
test = log $ encodeJSON $ Single true ①
```

① 打印 `{"contents":true,"tag":"Single"}`

注意 `tag` 的使用。这很常见，也是 Haskell 的 Aeson 库的做法。有趣的事实：Aeson 在希腊神话中是 Jason 的父亲。

那么为什么要标记？

那是因为 Sum Types 也被称为 Tagged Unions。这里的标签是数据构造函数名称。正是这些标签帮助编译器进行模式匹配。

现在，让我们将 `unwrapSingleConstructors` 从默认的 false 改为 true：

```
instance decodeSingle :: Decode a => Decode (Single a) where
    decode = genericDecode defaultOptions
        { unwrapSingleConstructors = true } ①

instance encodeSingle :: Encode a => Encode (Single a) where
    encode = genericEncode defaultOptions
        { unwrapSingleConstructors = true } ①

test :: Effect Unit
test = log $ encodeJSON $ Single true ②
```

① 这是使用 Record Update 语法。注意使用 = 而不是 :。因此，我们想要所有默认值，但我们想要覆盖 `unwrapSingleConstructors`。

② 打印 `true`。

这个程序只是简单地打印 `true`，因为 `Single` 有一个单一的数据构造函数。

接下来，我们将 `unwrapSingleArguments` 从 true 改为 false：

```
data SumEncoding
  = TaggedObject
    { tagFieldName :: String ①
    , contentsFieldName :: String ②
    , constructorTagTransform :: String -> String ③
    }
```

① 这是标签字段的名称。在 `defaultOptions` 中，它被设置为 `"tag"`。

② 这是内容字段名称。在 `defaultOptions` 中，它被设置为 `"contents"`。

③ 这是一个转换函数，用于更改数据构造函数标签名称，默认为恒等函数。

### 24.2. Argonaut JSON 编码和解码

Argonaut 库让你完全控制编码和解码过程。如果你记得我们编写 Parser 时所做的事情，这是一个更简单、但类似的过程。

让我们创建一个简单的 Type，看看我们如何手动编写编码器和解码器。

这里是一个用于 Desserts 的简单 Type：

```
data Dessert = IceCream | Cake | Pie
```

现在我们想要为测试目的打印这个 Type：

```
data Dessert = IceCream | Cake | Pie
derive instance genericDessert :: Generic Dessert _
instance showDessert :: Show Dessert where
  show = genericShow
```

现在我们需要决定这个 Type 在 JSON 中如何表示。使用 `Foreign.Generic` 库，它将被表示为：

```
{"tag":"IceCream"}
{"tag":"Cake"}
{"tag":"Pie"}
```

标签将是数据构造函数名称。

但我们希望它是一个字符串。我们知道可以通过覆盖 Generic JSON 库中的 `defaultOptions` 来实现。现在，我们将看到如何在 Argonaut 中实现这一点。

我们希望 `Dessert` 编码为字符串的原因是，如果我们有以下 Types：

```
data MainDish = Steak | Chicken
data SideDish = Rice | Asparagus
type Meal =
  { main :: MainDish
  , side :: SideDish
  , dessert :: Dessert
  }
type Meals = { meals :: Array Meal }
```

那么 `Meals` 将被编码为：

```
{
  "meals": [
    {
      "main": "Steak",
      "side": "Asparagus",
      "dessert": "Ice Cream"
    },
    {
      "main": "Chicken",
      "side": "Rice",
      "dessert": "Pie"
    }
  ]
}
```

注意我们也希望 `SideDish` 编码为字符串。

因此我们将一行一行地为 `Dessert` 编写解码器，从实例定义开始。但首先这里是 Typeclass：

```
class DecodeJson a where
  decodeJson :: Json -> Either JsonDecodeError a
```

现在我们可以编写实例定义：

```
import Data.Argonaut.Decode (class DecodeJson) ①
instance decodeJsonDessert :: DecodeJson Dessert where
```

① 必须包含该类型类。

现在我们可以编写左侧代码：

```
instance decodeJsonDessert :: DecodeJson Dessert where
  decodeJson json = ???
```

由于我们正在 `DecodeJson` Monad 中工作，我们将添加一个 do 块：

```
instance decodeJsonDessert :: DecodeJson Dessert where
  decodeJson json = do
    ???
```

现在我们需要一种方法来解码我们传入的 JSON String。去 Pursuit 上查找 `DecodeJson`，看看是否有 `String` 的实例。然后返回这里。

事实证明确实有这样的实例：

## DecodeJson

Source

```
class DecodeJson a where
