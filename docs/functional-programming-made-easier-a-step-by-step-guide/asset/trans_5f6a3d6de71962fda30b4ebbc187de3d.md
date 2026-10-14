

可以确保在调用 `stringify` 和类似期望 Json 的函数时，我们不会传递无效的东西，例如一个函数。

现在，我们已经回答了这个问题，让我们回到 Dessert 的编码器：

```
instance encodeJsonDessert :: EncodeJson Dessert where
  encodeJson IceCream = ???
```

我们希望将 IceCream 编码为 "Ice Cream"，因此我们可能会诱惑地写成：

```
instance encodeJsonDessert :: EncodeJson Dessert where
  encodeJson IceCream = "Ice Cream"
  ???
```

但正如我们刚刚学到的，String 不是 Json，但如果我们调用其 encodeJson 实例，它就可以是 Json：

```
instance encodeJsonDessert :: EncodeJson Dessert where
  encodeJson IceCream = encodeJson "Ice Cream"
  ???
```

现在我们可以只写另外 2 个 case：

```
instance encodeJsonDessert :: EncodeJson Dessert where
  encodeJson IceCream = encodeJson "Ice Cream"
  encodeJson Cake = encodeJson "Cake"
  encodeJson Pie = encodeJson "Pie"
```

而这里是对比的解码器：

```
instance decodeJsonDessert :: DecodeJson Dessert where
  decodeJson json = do
    s <- decodeJson json
    case s of
      "Ice Cream" -> pure IceCream
      "Cake" -> pure Cake
      "Pie" -> pure Pie
      _ -> Left $ UnexpectedValue json
```

重要的是要查看解码器和编码器，以确保它们将是彼此的逆函数，除了解码器可以用 Either 失败的事实。

所有编码器和解码器都应遵循以下定律：

```
decodeJson <<< encodeJson = pure
```

记住，`pure` 是 Kleisli 范畴中的恒等。 这里的 `Monad` 是 `Either`，因为 `decodeJson` 可能失败。 在这种情况下，它不会失败，因为 `encodeJson` 先被调用，假设我们编写了正确的解码器。

检查我们的编码器和解码器，确保我们可以通过它们往返数据并取回我们开始的内容。

下面的代码是对往返的测试，尽管不完整：

```
log $ show $ (decodeJson $ encodeJson Pie :: Either _ Dessert) ① ②
```

+   ① 应该打印 `(Right Pie)`，即等价于 `pure Pie`。
+   
+   ② 我们必须添加显式的类型定义，让编译器知道 `decodeJson` 应该产生什么类型。 这是因为它无法弄清楚，因为它只是得到一些 Json 值，可能是任何东西。

现在，我们应该为 `Meal` 编写编码器和解码器。 这里再次给出它的定义：

```
data MainDish = Steak | Chicken

data SideDish = Rice | Asparagus

type Meal =
  { main :: MainDish
  , side :: SideDish
  , dessert :: Dessert
  }
```

但在我们能做到之前，我们必须为 `MainDish` 和 `SideDish` 两者都有编码器。 这些几乎与 `Dessert` 相同，所以我直接给你完整的版本：

```
instance encodeJsonMainDish :: EncodeJson MainDish where
    encodeJson Steak = encodeJson "Steak"
    encodeJson Chicken = encodeJson "Chicken"

instance decodeJsonMainDish :: DecodeJson MainDish where
    decodeJson json = do
        s <- decodeJson json
        case s of
            "Steak" -> pure Steak
            "Chicken" -> pure Chicken
            _ -> Left $ UnexpectedValue json

instance encodeJsonSideDish :: EncodeJson SideDish where
    encodeJson Asparagus = encodeJson "Asparagus"
    encodeJson Rice = encodeJson "Rice"

instance decodeJsonSideDish :: DecodeJson SideDish where
    decodeJson json = do
        s <- decodeJson json
        case s of
            "Asparagus" -> pure Asparagus
            "Rice" -> pure Rice
            _ -> Left $ UnexpectedValue json
```

确保你花点时间查看它们，看看它们与我们为 Dessert 编写的几乎相同。

在排除这个问题后，我们可以将注意力转向 Meal 的编码器。 但是等等。 Meal 不是一个类型。 它是记录的类型别名。

事实证明，Record 已经有一个 encodeJson 和一个 decodeJson 实例。 所以我们不必编写它们。

但是，如果 Meal 是一个真正的类型会怎样：

```
newtype Meal = Meal ①
    { main :: MainDish
    , side :: SideDish
    , dessert :: Dessert
    }
```

① 使用 newtype 因为只有一个数据构造函数并且它只有一个参数，即记录。

现在，我们必须手动编写编码器和解码器。

在这一点上，你可能会：

```
type GetPostRes =
  { id :: Int
  , title :: String
  , body :: String
  , userId :: Int
  }
```

注意我们从类型别名开始。 我们可能需要稍后将其设为真正的类型，例如，如果我们希望为此类型提供 Eq 实例。 我们会在需要时稍后转换它，但现在，我们将保持原样。

由于我们此请求的全部类型都是 JSON 类型，我们应该能够通过

使用 Generics 的 Foreign 库。

由于记录已经有 Encode 和 Decode 实例，所以我们无需再做任何事情。

现在，我们准备好进行 Ajax 调用以发出 GET 请求。 当我们浏览 affjax 包时，我们发现 Affjax 模块有以下函数：

```
get :: ∀ a. ResponseFormat a -> URL -> Aff (Either Error (Response a))
```

一个名为 get 的函数似乎是进行 HTTP GET 调用的有力候选者。 读完文档后还有更多内容：

```
Makes a `GET` request to the specified URL.
```

现在，我们必须弄清楚其参数的类型。 我们将从 ResponseFormat 开始。 在 Pursuit 文档中点击 ResponseFormat 会产生：

![](img/8c0e9b687c62642e828ccb5481e11313_1098_0.png)

从中我们可以看出，有很多不同的响应格式。 但其中有一个看起来是我们想要的，那就是 Json。

另一个需要注意的是，Json 数据构造函数接受一个函数，该函数接受看起来像带有 Json 的函子，即 f Json，并产生同一个函子带有 a，即 f a，。 这可能与某种从 JSON 转换到适当的 PureScript 类型有关。

我们稍后再担心这个问题，如果需要的话。

接下来要理解的是 Response。 在浏览器上点击后退箭头并点击 Response 会给我们：
