

subtypes，act():Unit。正如名称所示，此方法定义了 actor 在开始运行时将执行的操作。以下 REPL 序列演示了这一点。

```
scala> import actors._
import actors._

scala> val actor = new Actor {
|   def act {
|       println("Hello world!")
|   }
| }
actor: java.lang.Object with scala.actors.Actor = $anon$1@368e091

scala> actor.start
res0: scala.actors.Actor = $anon$1@368e091

scala> Hello world!
```

请注意，打印语句在 actor 被告知启动之前实际上并未执行。当它被告知启动时，该行会使用与 REPL 不同的线程打印出来。在这种情况下，这导致它在提示符之后打印。这里所做的基本上是这个的更长版本。

```
scala> Actor.actor{ println("Hello world!") }
Hello world!
res1: scala.actors.Actor = scala.actors.Actor$$anon$1@7c7bd649
```

当你调用 Actor.actor 时，参数会成为 Actor 的一个新子类型的体，并且会在该类型的实例上调用 start 方法。

你只能调用一次 start 方法。对该方法的进一步调用不会导致任何事情发生。要使 act 方法再次发生，可以调用 restart 方法。

## 34.2.1 receive 方法和消息

以上面所示的方式使用，actor 不过是某个操作发生的单独线程。要更好地利用 actor 模型，我们需要在 actor 之间传递消息并让 actor 对这些消息做出反应。消息的发送使用感叹号，使用形式 actor ! message。消息的类型为 Any，因此你可以发送任何你想要的消息作为消息。有些东西，比如 case class，因我们将在此处讨论的原因而更适合使用。

让 actor 获取消息的一种方式是让它调用 receive。receive 方法接受一个部分函数的单个参数。该部分函数应针对 actor 应使用该 receive 处理的消息提供 case。receive 接受具有 case 的部分函数这一事实是 case class 作为消息有意义的第一个原因之一。你可以在编写部分函数时对任何可以进行模式匹配的东西进行操作。这包括数字、字符串和元组的字面量。使用此类内置类型的问题在于类型本身不携带含义，并且随着应用程序的增长，这可能导致问题。使用有意义的类型与为变量、方法或类型本身使用有意义的名称一样重要。

简单的 actor 示例在说明力方面有点不足。它们有点像面向对象的小例子。它们不足以激发该主题。为此，我们将改为查看与

![](img/157fcf510c119278e4b1267c62717fa8_861_0.png)

### 图 34.1：这些是“与”、“或”和“非”门的标准图形表示。

将在第 34.3 节中完全展开的更大示例相关的代码片段相关代码。我们将在该部分开发的示例代码使用 actor 来模拟电路中逻辑门级别的元素。这将被放入绘图程序中并使用 Clickable trait，如 DrawGraph 所做的那样，以便用户可以图形化地构建电路。

计算机电路使用晶体管这一基本组件构建。晶体管可以以产生我们自第 4 章以来一直在逻辑运算中使用的逻辑运算行为的方式连接：与，或，非。这些通常在图形图中用图 34.1 所示的形状表示。从门进出门的实线代表可以处于表示 0 或 1 的电压的导线。

模拟将使用 actor 表示门和导线。Wire 类的基本实现以及将发送到导线的消息类型的 case class 如下所示。导线具有其上电压的布尔状态、应绘制的笛卡尔位置的值，以及连接到的门的 Buffer。

```
private class Wire(private[this] var state:Boolean,
    private[this] var x:Double,
    private[this] var y:Double) extends Actor{
private[this] val outs = mutable.Buffer[Gate]()
def act {
    while(true) {
    receive {
    case SetWire(v) =>
        if(v!=state) {
        state = v
        outs foreach (_ ! WireChange(state,this))
        drawing.refresh
        }
    }
    case MoveTo(nx,ny) =>
        x = nx
        y = ny
    case GetPos => sender ! (x,y)
    case GetPosAndState => sender ! PositionAndState(x,y,state)
    case ConnectWireOutput(g) =>
        outs += g
        g ! WireChange(state,this)
    case DisconnectOut(g) => outs -= g
    }
    }
}
```

```
private case class SetWire(value:Boolean)
private case class MoveTo(x:Double,y:Double)
```

```
private case class ConnectWireOutput(g:Gate)
private case class DisconnectOut(g:Gate)
private case object GetPos
private case object GetPosAndState
private case class PositionAndState(x:Double,y:Double,state:Boolean)
```

`Wire` actor 中唯一的 method 是 `act`。此方法在使用 `receive` 时遵循许多 actor 的某种标准形式。有一个 `while` 循环，直到 actor 不再需要时才结束，调用 `receive` 在该循环内部。在这种情况下，循环无限期进行，因为电路仅在整个应用程序停止时才应停止运行。需要这样的循环，因为每次对 `receive` 的调用只处理一条消息。

在这种情况下，有六种不同的 case 对应于可以传递给导线的六种不同类型的消息。第一个设置状态。如果有变化，此变化会传递给所有连接的门。请注意使用 `!` 向每个门发送 `WireChange` 消息。这很重要。actor 应该只通过消息进行通信，而不是直接方法调用。直接方法调用可能导致 actor 方法的安全性崩溃，并出现随之而来的竞争条件。为了明确表示除了当前 actor 之外没有任何东西可以更改 `x, y, state` 或存储在 `outs` 中的值的值，所有四个成员值都被声明为 `private[this]`。这种表示法在第 399 页的一个旁注中简要描述过。它意味着这些成员只能由它们存在的对象访问。甚至同一类型的其他对象也无法查看或更改这些值。所有四个值都是可变的，这使它们成为竞争条件的潜在原因。在正确完成的情况下，actor 模型将限制此类可变值的修改为单个线程。声明它们为 `private[this]` 有助于强制执行我们想要维护的访问要求。

将访问限制为单个线程的目标是使用 case class 作为消息的另一个原因。通过消息发送的数据隐式地为两个不同的 actor 所知。如果该数据是可变的，那么两个 actor 就有可能对数据进行更改并导致竞争条件。防止这种情况的最简单方法是使用不可变数据作为消息。case class 的一个特性是它们是不可变的。因此，如果你的所有消息都是 case class 且内容不可变或基本不可变类型如 `Int, Double, String`，或元组，你就不必担心两个 actor 通过消息修改相同的数据。

虽然不可变消息是首选，因为它们使生活更简单，但使用可变消息也是可能的。装配线示例，如果按字面理解，就是可变消息的示例。从一个工位传递到另一个工位的物品就是消息。如果工人们在改变这些物品，那么它们就是可变的。这种情况可以在代码中复制，但你必须确保当可变对象被传递出去时，发送消息的 actor 停止修改它。理想情况下，它会删除对其的所有引用以确保安全。

处理的两个消息都有代码向 `sender` 发送消息返回。在这种上下文中使用时，名称 `sender` 完全按你期望的方式工作。这就是我们如何从消息处理程序返回一个值。`!` 不设置任何处理响应的东西。它返回类型为 `Unit` 的值。对于需要响应的消息，我们可以使用另外两个发送运算符。`!!` 运算符返回一个 `scala.actors.Future[Any]`。这与我们在第 21.5 节中看到的对 `Futures.future` 的调用中看到的相同的 `Future` 类型。有一个 `apply` 方法返回响应，如果没有可用则阻塞。如果不想冒阻塞的风险，`isSet:Boolean` 方法会告诉你值是否已准备好。我们可以用 `GetPos` 消息使用如下代码。

```
val fut = comp !! GetPos
val (ccx:Double,ccy:Double) = fut()
```

