
⑤ 当文件成功读取时，使用 put 将数据写入 AVar。

⑥ processFile 接收一个 AVar，它会从中取出 File 数据。注意 AVar 类型接受一个类型参数。这是可以从中取出的数据的类型。在此例中，它是 String。

⑦ 这里是从 AVar 中读取数据的位置。这会阻塞 Fiber 直到数据可用，在本程序中，由于 readAFileAfterTwoSeconds 的延迟，这至少需要 2 秒。

⑧ 这是如何创建一个初始为空的 AVar。要创建带有初始数据的 AVar，请使用 AVar.new 并传入初始值。

⑨ 两个 Fiber 都被传入 fileAVar 以实现 Fiber 间通信。

此程序的输出是：

```
This is a test.
```

AVar 可用作简易队列，其中多个 Fiber 写入同一个 AVar。在这种情况下，尝试向非空 AVar 执行 put 会阻塞生产者，直到消费者通过 take 将 AVar 掏空。

而尝试从空 AVar 取值会阻塞消费者，直到生产者通过 put 向其写入。

AVar 可以作为通过 ReaderT 传递的只读 Record 的一部分。这是因为 AVar 本身从未被变异。

如果这不够直观，请将 AVar 视为常量引用。表示 AVar 的数据结构是不可变的，而 AVar 所引用的数据结构则可通过 AVar API 进行变异。

你可能会想知道 AVar 是否只是全局共享状态的例子。它不是。AVar 仍需像其他不可变值一样被传递。但由于底层存储是可变的，对该底层数据的访问由保证一致性的 API 控制。

AVar 可用于具有单个生产者和多个消费者的程序，但前提是所有消费者地位平等。

例如，想象你有一个单个生产者，它为多个消费者中的一个产生对 Web 服务的 Ajax 调用请求。

所有消费者都会调用 take，这会使它们阻塞直到有数据写入 AVar。一旦生产者调用 put，其中一个且仅一个消费者会开始处理请求。其他所有消费者仍会阻塞。使用单个 AVar 时，没有办法区分哪些消费者会获得某些值。

并且没有办法让所有消费者消费一次对 AVar 的 put。

但如果我们想要一个或多个生产者和一个或多个消费者，使得从任何生产者产生的单个值会被所有消费者消费呢？

## 22.2.4. Busses

Bus 是 PureScript 实现的 *数据总线* 类型，它是一个数据结构及其关联的 API，可促进由一个或多个发布者写入数据。此数据将被广播给一个或多个订阅者，每个订阅者都会获得数据的副本。

总线可以是只读、只写或读写。

让我们编写一个使用 Bus 的简单程序：

```
import Prelude

import Control.Monad.Error.Class (try)
import Data.Either (Either(..))
import Data.String.Common (toUpper, toLower) ①
import Data.Tuple (Tuple(..))
import Effect (Effect)
import Effect.Aff.Bus (BusR, BusW) ②
import Effect.Aff.Bus as Bus ③
import Effect.Aff (Aff, launchAff_, forkAff)
import Effect.Class.Console (log)
import Node.Encoding (Encoding(..))
import Node.FS.Aff (readTextFile)

readAFile :: BusW String -> Aff Unit ④
readAFile fileBus = do
  result <- try $ readTextFile ASCII "test.txt"
  case result of
    Right text -> Bus.write text fileBus ⑤
    Left err -> log $ show err

processFile :: (String -> String) -> BusR String -> Aff Unit ⑥
processFile convert fileBus = do
  text <- Bus.read fileBus ⑦
  log $ convert text ⑧

test :: Effect Unit
test = launchAff_ do
  fileBus <- Bus.make ⑨
  let Tuple readBus writeBus = Bus.split fileBus ⑩
  void $ forkAff $ processFile toUpper readBus ⑪
  void $ forkAff $ processFile toLower readBus ⑫
  void $ forkAff $ readAFile writeBus ⑬
```

① 导入字符串转换函数供订阅者使用。

② 在这里只导入类型。这是因为下一行我们将以 Bus 名称限定导入所有其他内容。这避免了 Bus.BusR 或 Bus.BusW 这种尴尬的类型名。

③ 以限定方式导入 API。这是为了避免名称冲突和歧义，因为 API 函数具有通用名称，例如 read、write、split 等。相反，我们将使用完全限定名称引用它们，例如 Bus.read。

④ readAFile 接收一个 Bus，它会向其写入文件数据。注意 BusW 类型是一个只写总线，接受一个类型参数。这是你可以写入总线的数据类型。在此例中，它是 String。这与我们的 AVar 版本类似。

⑤ 当文件成功读取时，总线会被写入。

⑥ processFile 接收 2 个参数。第一个是字符串转换函数。第二个是只读总线，即 BusR，它会从中读取文件数据。注意 BusR 类型接受一个类型参数。这是你可以从总线读取的数据类型。在此例中，它是 String。

⑦ 这里是从总线读取数据的位置。如果调用时没有可用数据，这会阻塞订阅者。

⑧ 在记录日志之前，processFile 应用字符串转换函数。

⑨ make 创建一个双向总线，即 BusRW，一个读写总线。

⑩ split 将双向总线拆分为 BusR 和 BusW，即只读和只写总线。

⑪ 第一个 processFile 使用 toUpper 转换文件内容。它还被传入只读总线。

⑫ 第二个 processFile 使用 toLower 转换文件内容。它同样被传入只读总线。

⑬ 只写总线被传入 readFile。

此程序的输出是：

```
THIS IS A TEST.

this is a test.
```

## Chapter 23. Coding With Effects

返回你一直在编码的项目并创建一个名为 Ch23a.purs 的文件并添加以下内容：

```
module Ch23a where

import Prelude ①

import Effect (Effect)
import Effect.Class.Console (log) ②

test :: Effect Unit
test = do
  log "placeholder" ③
```

① 我们再次没有从 Prelude 写入任何内容，所以我们将导入全部。

② 我们现在使用此版本的 log，以便在 Effect 和 Aff 中使用它。

③ 我们很快就会删除它。它只是为了让编译器满意而存在。

接下来，将你的 Main 模块更改为导入 Ch23a 并调用其 test 函数：

```
module Main where

import Prelude
import Effect (Effect)

import Ch23a as Ch23a

main :: Effect Unit
main = Ch23a.test
```

如果运行：

```
npx spago run
```

你应该会看到它构建并打印：

```
[info] Build succeeded.
placeholder
```

## 23.1. Simple AVar Program Specification

首先，我们将编写一个简单的程序来使用 AVar。为了为此准备项目，我们需要在 spago.dhall 文件中添加 2 个包，即 aff 和 avar。

完成后，运行：

```
npx spago build
```

我们将有 3 个 Fiber。一个是半个时钟，即时钟的 Tick 部分。第二个是时钟的后半部分，即 Tock 部分。它们将通过一个 AVar 通信。

第三个是一个炸弹，它会在指定数量的 Tick-Tock 组合后等待然后用 BOOM!! 消息在控制台引爆。

它们都将使用一个名为 ttAVar 的单个 AVar 进行通信，它代表 tick-tock AVar。

Tick Fiber 将每秒查看一次 ttAVar，如果其值是 tock，则将其更改为 tick。Tock Fiber 将执行相反操作。

Bomb Fiber 将每 500 毫秒检查一次 ttAVar，以查看时间是否已从 tick 变为 tock。当它这样做时，它会将其视为倒计时，并在达到指定数量时引爆，我们的程序将退出。

如果这有点令人困惑，不用担心，我们将一步一步构建它。

首先为 ttAVar 建模类型，即 Tick-Tock 值。在继续阅读之前先完成此操作。

以下是类型：

```
data TickTock = Tick | Tock
```

现在，由于没有其他明显需要建模的类型，我们将开始编码我们的 Fiber。我们在需要时沿途建模类型。

首先，只写 Tick Fiber 的类型签名。称它为 tick。重读上述规范，如果在这一步卡住。尝试一下再继续阅读。

Fiber 只需要 ttAVar，并且它不会返回任何内容但仍在 Aff 中运行：

```
import Effect.Aff.AVar (AVar) 1 2

tick :: AVar TickTock -> Aff Unit
```
