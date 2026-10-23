
def act {
  loop {
    react {
      case FlipSwitch =>
        state = !state
        out ! SetWire(state)
        drawing.refresh
      case MoveTo(nx,ny) =>
        x = nx
        y = ny
      case GetPos => sender ! (x,y)
      case GetPosAndState => sender ! PositionAndState(x,y,state)
    }
  }
  def toXML:xml.Node = <comp type="switch" x={x.toString} y={y.toString}
    state={state.toString}/>
}

private case class WireChange(value:Boolean,wire:Wire)
private case class SetWire(value:Boolean)
private case class MoveTo(x:Double,y:Double)
private case class ConnectGateInput(y:Double,w:Wire)
private case class ConnectWireOutput(g:Gate)
private case class DisconnectOut(g:Gate)
private case object GetPos
private case object GetPosAndState
private case object GetWires
private case object FlipSwitch
private case class PositionAndState(x:Double,y:Double,state:Boolean)
}

object DrawCircuit {
  def apply(p:DrawTransform) = new DrawCircuit(p,Seq(),Seq(),20)

  def apply(p:DrawTransform,n:xml.Node) = {
    val compData = (n \\ "comp").map(cn => {
      val x = (cn \\ "@x").text.toDouble
      val y = (cn \\ "@y").text.toDouble
      (cn \\ "@type").text match {
        case "switch" => SwitchData(x,y,(cn \\ "@state").text.toBoolean)
        case t => GateData(t, x, y, (cn \\ "in").map(_.text.toInt))
      }
    })
    val wireData = (n \\ "wire").map(wn => {
      val x = (wn \\ "@x").text.toDouble
      val y = (wn \\ "@y").text.toDouble
      val index = (wn \\ "@index").text.toInt
      val state = (wn \\ "@state").text.toBoolean
      WireData(index,x,y,state)
    })
    val speed = (n \\ "@speed").text.toInt
    new DrawCircuit(p,compData,wireData,speed)
  }
}

![](img/157fcf510c119278e4b1267c62717fa8_874_0.png)

## 图34.2：这是添加了DrawCircuit的绘图程序的屏幕截图

其中包含两个不同的电路。每个电路在左侧有两个用方块表示的开关。单击一个方块可以将其打开或关闭。你可以把它们看作输入A和B。底部的电路是“异或”门。它实现了逻辑 A xor B = (A or B) and not (A and B)。顶部电路没有输出。然而，当两个开关都打开时，信号会在环路中传播。

```
case class WireData(index:Int, x:Double, y:Double, state:Boolean)
class CompData
case class GateData(gType:String, x:Double, y:Double, ins:Seq[Int]) extends CompData
case class SwitchData(x:Double, y:Double, state:Boolean) extends CompData
}
```

如果运行这个程序，你可以制作一些简单的电路，如图34.2所示，然后拨动开关，观察信号在电路中传播。

这段代码中新的元素集中在actor的使用上。不是对comps的任何元素调用方法，而是传递消息。当需要立即获取值（例如绘图时）时，消息通过!?发送。²

> ²需要说明的是，在开发这段代码期间，当!?操作符用于一个尚未启动或未响应该消息的actor时，曾多次导致应用程序挂起。

除了Wire类型之外，还有Gate（具有若干子类型）和Switch，它们也是CircuitComponent的子类型。每个Gate子类型都必须定义一个delay值。该值与输入线变化和输出线变化之间所需的时间成正比。请注意，Gate类中对WireChange消息的处理包含对Thread.sleep的调用以实现延迟。由于这种延迟，并且不希望阻塞actor线程，因此将其放入对Actor.actor的调用中，以便在单独的线程中执行，并允许actor在此期间处理其他消息。

这里actor消息处理方式的编写看起来几乎就像

> ²需要说明的是，...

方法一样。case类的名称类似于方法名，模式中绑定的变量非常类似于方法的参数。其后的内容是方法体。消息传递方式比普通方法调用更动态。这有一些好处，但缺点是编译器无法为你发现同样多的错误。向一个不响应某消息类型的actor发送消息并不是错误。如果你使用!或!!发送消息，甚至不会引发运行时错误，因为未被处理的消息只是停留在actor的消息队列中。这也意味着，在原本使用标准方法时会采用包含多态和子类型的地方，代码中会出现多得多的match表达式。

这段代码中还有另一个非常重要的方面需要指出。按照目前的写法，DrawCircuit类型无法序列化。这意味着包含DrawCircuit的绘图无法保存为二进制或zip格式，也无法用于网络协作，因为这些功能依赖于对象流和序列化。原因在于Actor类型不可序列化。更具体地说，actor的消息队列无法序列化。即使我们让CircuitComponent扩展Serializable，序列化尝试仍然会失败。我们可以通过将comps设为transient并覆盖默认序列化来绕过这个问题。考虑到当前代码的长度，为此再添加更多代码并非好主意。由于提供了XML保存和加载支持，因此可以保存带有电路的绘图，而不必每次重新绘制。

## Akka

本章讨论的actor使用Scala标准库中自带的一个库。这个库相当简单易用，能满足大多数需求。还有一个这里没有讨论的scala.actors.remote包，它允许你将actor分布在多台机器上。尽管如此，还有一个为Scala编写的actor库，被推荐用于真正大规模的基于actor的项目或性能至关重要的项目。这就是Akka库，http://akka.io/。Akka被认为是基础Scala安装的主要扩展之一，它被加入Typesafe技术栈（http://typesafe.com/）就证明了这一点。Akka actor比Scala actor的开销更低，因为它们不使用相同类型的消息邮箱结构。它还设计为容错的，这样当出现问题时，程序可以继续运行。Akka同样支持远程actor，适合需要扩展到单台计算机之外的应用。

## 34.4 章末材料

### 34.4.1 概念总结

- • actor模型是编程中一种不同的并发和并行方法。
- – 你可以想象每个actor拥有自己的线程。
- – actor通过发送消息进行通信，而不是调用方法。
- - actor可以拥有可变数据。只要它们不共享可变数据，就不会有竞争条件的风险。
- - Scala在scala.actors包中提供了对actor的支持。
- - 要创建功能完整的actor，需要创建继承Actor特质（trait）的类。
- - 这些类应该实现act方法。这就是actor启动时被调用的方法。
- - 为了处理消息，act方法应包含对receive或react的调用，通常位于循环结构内部。
- * receive和react都接受一个参数，该参数是一个偏函数。它应该针对actor可能被发送的不同消息提供case分支和相应的处理代码。
- * receive方法是一个标准方法，会阻塞直到有合适的消息发送给该actor。它占用actor的线程并返回一个值，因此可以作为一个表达式使用。
- * react方法不返回。它后面的任何代码都不可达。这允许actor之间共享线程。你需要使用loop或loopWhile来使其重复。简单的while循环无法工作。
- - 消息最好是不可变的，并能与模式匹配配合使用。因此，通常使用case类来创建不同类型的消息。
- - 我们已为逻辑门级电路编写了一个基于actor的事件模拟示例。

### 34.4.2 练习

- 1. 编写一个简单的actor，使用不带循环的receive。启动该actor，并验证它只能处理一条消息而无需重启。
- 2. 将上一练习中的actor的receive调用放入while循环中，然后验证它现在可以处理多条消息。
- 3. 编写一个actor，使其能够知道另一个同类型actor，从而协作倒计时。该actor应处理两条消息。一条消息会向它传递一个actor作为其“朋友”。另一条消息处理一个数值，如果该值大于零，则打印该值，然后向朋友发送一个比打印值小1的消息。创建两个这样的actor并让它们倒计时。为了验证两个actor都参与了对话，你可以给它们命名，并在打印数值时同时打印这些名称。
