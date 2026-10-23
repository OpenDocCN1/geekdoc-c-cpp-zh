

这个 RPNCalc 对象也可以作为命令集成到绘图程序中。为了使用变量，我们在 Drawing 类中增加了一个额外的 val，名为 vars，它是一个 mutable.Map[String,Double]。然后我们添加了两个名为 “rpn” 和 “set” 的命令。第一个使用指定的参数调用该 RPNCalc 对象。第二个允许你在该绘图的 Map 中设置变量。下面是 Commands 的修改版本代码

```
package scalabook.drawing

/**
 * This object defines the command processing features for the drawing.
 * Use apply to invoke a command.
 */
object Commands {
  private val commands = Map[String,(String,Drawing)=>Any](
    "add" -> ((rest,d) => rest.trim.split(" +").map(_.toInt).sum),
    "echo" -> ((rest,d) => rest.trim),
    "refresh" -> ((rest,d) => d.refresh),
    "freeze" -> ((rest,d) => Thread.sleep(rest.trim.toInt*1000)),
    "rpn" -> ((rest,d) => scalabook.util.RPNCalc(rest.trim.split(" +") ,d.vars)),
    "set" -> ((rest,d) => {
      val parts = rest.trim.split(" +")
      d.vars(parts(0)) = parts(1).toDouble
      parts(0)+" = "+parts(1)
    })
  )

  def apply(input:String,drawing:Drawing):Any = {
    val spaceIndex = input.indexOf(' ')
    val (command,rest) = if(spaceIndex < 0) (input.toLowerCase(),"")
    else (input.take(spaceIndex).toLowerCase(),input.drop(spaceIndex))
    if(commands.contains(command)) commands(command)(rest,drawing)
    else "Not a valid command."
  }
}
```

得益于原始设计的灵活性，添加两个额外命令几乎不需要任何工作。添加 vars 到 Drawing 则需要更多的工作。最明显的地方是在顶行传递参数。

```
class Drawing(private val root:DrawTransform,private[drawing] val vars:mutable.Map[String,Double]) extends Serializable {
```

更大的挑战来自于伴生对象中反序列化 XML 的 apply 方法需要一个合适的 map。下面是两个版本的 apply 代码以及从 XML 构建 map 的一个方法。

```
def apply(data:xml.Node):Drawing = {
  new Drawing(DrawTransform(null,(data \ "drawTransform") (0)),buildVars(data \
    "variable"))
}

def apply():Drawing = {
  new Drawing(new DrawTransform(null),mutable.Map[String,Double]())
}
```

```
def buildVars(nodes:NodeSeq):mutable.Map[String,Double] = {
	mutable.Map((for(n <- nodes) yield (n \ "@name").text -> (n \ "@value").text.toDouble): _ *)
}
```

要从 XML 中提取数据，就意味着数据必须先进入 XML。为此，我们还必须修改 Drawing 中的 toXML 方法，以包含变量的额外元素。这可以用以下代码完成。

```
def toXML : xml.Node =
<drawing>
  {root.toXML}
  { for(n,v) <- vars) yield (<variable name={n} value={v.toString}/>) }
</drawing>
```

这里使用了一个 for 循环来简化处理从 map 中出来的元组时的语法。

## 24.9 本章末尾材料

### 24.9.1 概念总结

- • 术语抽象数据类型，ADT，用于描述具有良好定义的操作的程序结构，但不指定这些操作是如何实现的。这个概念与接口与实现分离的思想相联系。

- • 栈是一种简单的 ADT，具有两个基本操作，push 和 pop。push 操作将元素添加到栈顶。pop 操作移除最近添加的元素。这种内容移除的顺序称为后进先出，LIFO。

- • 队列是另一种简单的 ADT，具有 enqueue 和 dequeue 操作。enqueue 将元素添加到队列，而 dequeue 取出在队列中停留最久的元素。这种元素移除的排序方案称为先进先出，FIFO。

- • 阶数分析帮助我们理解算法随着输入规模增大时的行为。O 记号忽略常数倍数和低阶项。它只有在输入规模变得很大时才真正相关。

- • 由于其简单性，栈或队列的任何合理实现都应具有 O(1) 的摊还成本操作。

- • 实现该栈 ADT 的一种方法是使用 Array 来存储数据。只需在 Array 中维护指向栈顶的索引并从 0 开始构建。当 Array 已满时，应通过乘性因子增长，以在复制操作上保持 O(1) 的摊还成本。

- • 也可以用 Array 实现队列。实现稍微复杂一些，因为数据在一端添加，在另一端移除。当它们到达末端时，前端和后端会绕回，以便 Array 保持小巧且大多数操作不需要复制。与栈一样，当 Array 确实需要增长时，应通过乘性因子增长。

- 测试是软件开发中非常重要的一部分。单元测试是对代码小单元的功能测试，例如单个类。JUnit 框架提供了一种简单的方法来构建可在软件开发期间定期运行的单元测试。

### 24.9.2 练习

- 1. 为 RPN 计算器添加额外的函数。
- 2. 为书中所示的 JUnit 测试编写更多测试。
- 3. 编写一些代码，以便通过网络发送的请求被排队并按到达顺序处理。你可以用 Thread.sleep 模拟长时间运行的计算。
- 4. 对于此练习，你应该实现队列和栈的几种可能版本，然后对它们进行计时测试，以查看它们的扩展效果。你将包含本章中开发的实现以及一些略有修改的实现，以查看细微选择如何影响最终实现的速度。
- 5. 使用 synchronized.wait 和 notifyAll 构建你自己的 BlockingQueue 版本，以重现 java.util.concurrent 中的版本行为。

### 24.9.3 项目

正如你可能猜到的，本章的项目要求你在代码中添加栈和/或队列。其中许多要求你制作线程安全的队列，以便在代码中放置在你可能使用过 java.util.concurrent.BlockingQueue 的地方。

- 1. 如果你一直在做 MUD 项目，对于本次迭代，你应该制作自己的线程安全队列，专门用于将从服务器套接字线程登录的玩家传递给主游戏线程。你可以决定包含的确切功能，但两个关键方面是它需要是 FIFO 并且线程安全。
- 2. 如果你一直在做网页爬虫项目，请制作并使用自己的线程安全队列，用于在套接字读取线程和解析线程之间传递信息以及返回。至少会有两个队列实例用于这些功能，每个数据流方向至少有一个。
- 3. 如果你正在做网络图形游戏，你需要为与 MUD 相同的目的编写一个线程安全队列。
- 4. 回到项目 4（p.494）关于数学练习表，建议你可以通过使用命令模式将多态性集成到你的项目中。命令模式的主要用途之一是实现撤销和重做功能。栈是执行此操作的理想数据结构。你让主应用程序跟踪两个栈。一个是撤销栈，你在命令执行时将其推入。当用户选择撤销时，你弹出撤销栈上的最后一个命令，调用其 undo 方法，然后将其推到第二个栈，即重做栈。当用户选择重做时，事情向相反方向移动。注意，任何正常活动可能都应清除重做栈。

你在此使用的栈可能与默认实现略有不同。首先，你需要重做栈具有 clear 方法。此外，你可能不想要无限撤销，因此你可能希望栈在推送一定数量的元素后“丢失”元素。如何以保持 $O(1)$ 行为的方式实现这一点留给学生作为练习。

- 项目 5（p.494）建议你在 Photoshop® 项目中添加命令模式以实现撤销和重做功能。正如上面对数学练习表所描述的那样，这最好用两个栈完成。对于本次迭代，你应该为 Photoshop 做上面为数学练习表描述的内容。

- 到目前为止，仿真工作台的项目让你使用像重力或布粒子网格这样的 N 体仿真。现在我们要加入一种根本不同类型的仿真，离散事件仿真。这些在第 26 章中讨论得更深入，但你可以在这里创建第一个简单的仿真，单服务器队列。

单服务器队列的想法是你有人们到达并排队以从单个服务器接收服务。人们以随机间隔到达，服务器花费随机时间处理请求。当人们到达而服务器忙时，他们进入队列。仿真可以跟踪人们等待多长时间以及队列的平均长度等信息。

离散事件仿真的关键是你只关心事件，而不是事件之间的时间。在此系统中，只有两种类型的事件，客户到达和服务完成。每次只能安排其中一种。要模拟到达，你将使用指数分布，要模拟服务时间，你将使用 Weibull 分布。以下公式可用于从这些分布生成数字，其中 $r$ 是对 `math.random` 的调用结果。

- $a(\lambda)_{exponential} = -\frac{-\ln(1-r)}{\lambda}$
- $a(k, \lambda)_{Weibull} = \lambda(-\ln(1-r))^{\frac{1}{k}}$

对于 Weibull，使用 $k = 2$。$\lambda$ 值决定到达或服务之间的平均时间。你应该让用户更改这些值。

仿真应从 $t = 0$ 开始，队列中没有人。你从指数分布生成一个值，$a_{exponential,1}$ 并立即推进到那个时间，此时第一个人进入。由于此时没有人被服务，他们直接进入服务器。你还从指数分布生成另一个数字，$a_{exponential,2}$ 并将其保留为下一个人进入的时间。第一个人进入服务器导致你生成一个服务时间，$a_{Weibull,1}$ 表示那个人何时完成服务，你将其存储。

然后你立即推进到两个事件时间中较小的那个。因此，要么第二个人到达并进入队列，要么第一个人被服务且服务器空闲且无人。每次有人到达时，你都会安排下一次到达。每次有人进入服务器时，你都会安排他们何时

