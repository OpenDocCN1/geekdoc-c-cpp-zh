
# 23.5 协作绘图（项目集成）

现在是时候将各部分整合到绘图程序中了。我们将通过两种方式来实现。为了演示套接字（socket）技术，我们将添加一个简单功能：允许将绘图副本从一个用户发送到另一个用户。实现起来很简单，因为我们已经有了将绘图发送到写入文件的流的代码。我们想要添加的网络另一个方面更为重要，我们将使用 RMI。这将是一个协作面板，多个用户可以在其中发布绘图供他人下载，互相聊天，甚至绘制基本草图。

我们将在 DrawingMain 中框架的菜单栏上添加一个标题为“Collaborate”的第二个菜单。该菜单将有四个选项。前两个用于通过网络基本发送绘图。后两个用于更复杂的基于 RMI 的协作方案。我们先从前两个开始，并在创建“File”菜单之后，将以下代码添加到 DrawingMain 类中。

```
contents += new Menu("Collaborate") {
    contents += new MenuItem("Start Server") {
        action = Action("Start Server"){
            startServer
            enabled = false
        }
    }
    contents += new MenuItem(Action("Send Drawing")(sendDrawing))
}
```

第一个选项用于在当前机器上设置一个 `ServerSocket`，它将一直驻留直到程序停止，并接受来自其他想要共享绘图的机器的连接。第二个选项允许我们将当前所选标签页中的绘图发送到另一台机器。为了让这段代码能够编译，我们需要实现 `startServer` 和 `sendDrawing` 方法。

这两个方法相当简单，可以直接放在 `DrawingMain` 中，因为我们已经使 `Drawing` 类型可以被序列化。如果之前没有为了通过流保存而完成这项工作，我们现在就必须添加该功能。下面是 `startServer` 方法的一种可能实现。

```
private def startServer {
    actors.Actor.actor {
        val ss = new ServerSocket(8080)
        while(true) {
            val sock = ss.accept
            val ois = new ObjectInputStream(new
                BufferedInputStream(sock.getInputStream()))
            val sender = ois.readUTF()
            val title = ois.readUTF()
            ois.readObject() match {
                case drawing:Drawing =>
                    val response = Dialog.showConfirmation(tabbedPane,"Accept "+title+" from "+sender+"?","Accept Drawing?")
                    if(response==Dialog.Result.Yes) {
                        addDrawing(title,drawing)
                    }
                case _ =>
```

这两个方法都没有包含适当的错误检查。这大大减小了代码长度，但生产级网络代码却不能忽视这一点，因为网络任务可能产生多种类型的异常。

这种基本的套接字方法在技术上足以让我们开始绘图，但如果你使用一段时间，就会注意到它实际上并没有太多的协作感。不同用户之间没有任何真正的交互。要实现真正的交互，需要在机器之间发送多种不同类型的消息。这正是 RMI 的优势所在。

理想的特性是真正的绘图协作，即两个或多个用户可以同时查看和编辑同一张绘图。本章曾考虑过这条路，但最终放弃了，因为所需代码过于复杂。由于我们已经使用标准序列化保存绘图，而 RMI 特性与序列化相互作用，这使得实现更加困难。此外，网络连接两侧的用户都需要通过 GUI 与元素交互。GUI 元素恰好是可序列化的，但要正确处理事件处理则更为复杂。最终，我们决定采用这种更简单的协作形式，它展示了实时交互，同时不包含许多会模糊教学目标的细节。

使用 RMI 意味着我们需要遵循 RMI 的基本步骤。首先确定我们希望拥有哪些远程接口，以及这些接口中应该包含哪些方法。我们这里的应用程序仍然足够简单，可以只使用一种服务器类型和一种客户端类型。在这种情况下，服务器类型将相当简单。远程特质（trait）和实现都展示在这里。

```
package scalabook.drawing
import java.rmi._
import server.UnicastRemoteObject
import collection.mutable

trait CollaborationServer extends Remote {
  @throws(classOf[RemoteException]) def joinCollaboration(col:Collaborator) :
    (Array[Collaborator], Array[(String,Drawing)])
  @throws(classOf[RemoteException]) def addDrawing(title:String, drawing:Drawing) :
    Unit
}

class CollaborationServerImpl extends UnicastRemoteObject with CollaborationServer {
  private val collaborators = mutable.Buffer[Collaborator]()
  private val drawings = mutable.Buffer[(String,Drawing)]()

  @throws(classOf[RemoteException]) def joinCollaboration(col:Collaborator) :
    (Array[Collaborator], Array[(String,Drawing)]) = {
    collaborators += col
    (collaborators.toArray,drawings.toArray)
  }

  @throws(classOf[RemoteException]) def addDrawing(title:String, drawing:Drawing) {
    drawings += title -> drawing
    for(c <- collaborators) {
      try {
        c.addDrawing(title, drawing)
```

```
} catch {
    case ex:RemoteException =>
    }
}
}
```

该特质只有两个方法：一个用于加入协作，一个用于共享绘图。实现包含了这两个方法，它们都相当简短，同时还包含两个数据成员，用于存储当前参与协作的人员以及已共享的绘图及其标题。`joinCollaboration` 方法返回所有协作者以及已共享的绘图。有趣的是，这些内容的传递方式不同。绘图和它们的标题都是可序列化的，但不是远程的，因此它们按值传递，新的协作者会得到一份副本。另一方面，协作者是远程的，所以传输过去的数组将充满远程引用，允许新用户与其他人通信。

值得注意的是，我们在为这些类型安排文件时采用了略有不同的方法。文件中并非只包含一个类或特质，而是同时包含了远程特质和实现类。5 这样做是因为两者密切相关，并且可以减少对 `java.rmi` 等内容的额外导入。这样做的缺点是，查找 `CollaborationServerImpl` 的人可能需要很长时间才能找到它，因为没有同名的文件。这很大程度上是一个风格问题，不同的老师和雇主可能会要求不同的规则。

实现协作特性的大部分代码都在客户端代码中。这包括 `Collaborator` 的远程接口及其实现。同样，两者放在一个文件中。这次文件更长，因为实现更长。如果特质和实现都很长，我们一定会把它们拆分成两个文件，以避免文件过长。然而，将特质移出并不能显著减少该文件的长度。这段代码让我们能够生成一个如图 23.3 所示的窗口。

```
package scalabook.drawing
```

```
import java.rmi._
import server.UnicastRemoteObject
import java.awt.image.BufferedImage
import java.awt.{Color,Font}
import java.awt.geom._
import swing._
import event._
import collection.mutable
```

```
trait Collaborator extends Remote {
  @throws(classOf[RemoteException]) def name:String
  @throws(classOf[RemoteException]) def post(text:String):Unit
  @throws(classOf[RemoteException]) def requestSketch:Array[Byte]
  @throws(classOf[RemoteException]) def updateSketch(who:Collaborator,
    img:Array[Byte]):Unit
  @throws(classOf[RemoteException]) def addDrawing(title:String,
    drawing:Drawing):Unit
}
```

> 5 这是你在 Scala 中可以做到的事情，但在其他语言（如 Java）中则不行。在 Java 中，每个文件只能有一个公共类型，并且该类型必须与文件名相同。

