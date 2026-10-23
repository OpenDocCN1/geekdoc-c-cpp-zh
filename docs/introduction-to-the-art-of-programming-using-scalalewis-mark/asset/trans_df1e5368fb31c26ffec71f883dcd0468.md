

![](img/157fcf510c119278e4b1267c62717fa8_636_0.png)

图23.1：本图展示了我们想要编写的基于套接字/流的聊天程序的不同使用场景。

`java.io.ObjectInputStream`。如果你使用这种方法，可以通过将`java.io.ByteArrayOutputStream`包装在适当的数据或对象输出流中来取出数据。这种方法并不简单多少。

### 23.2.3 来自套接字的流

对于UDP，我们看到数据必须打包到`DatagramPacket`中才能发送到其他机器，然后在到达时解包。我们没有讨论如何使用普通的`Socket`类通过TCP发送数据。为此，我们使用流。`Socket`类有以下方法。

```
getInputStream() : InputStream
getOutputStream() : OutputStream
```

这些方法的作用与其名称所预期的大致相同。如果你在套接字上调用`getInputStream`，它将返回一个连接到该套接字的`InputStream`实现，这样当从中读取数据时，读取到的将是通过套接字从另一台机器发送过来的数据。你可以像包装连接到文件的流一样包装这些流。这正是流库灵活性的体现。你可以编写使用`InputStream`或`OutputStream`的代码，无论传入的是哪种类型的流，它都能正常工作。因此，同样的代码既可以用于套接字，也可以用于文件。

为了了解这是如何工作的，我们将创建一个简单的聊天室，其中包含一个服务器，并能够容纳多个客户端。为了明确我们真正需要什么，我们应该做一些分析。图23.1展示了我们想要做的用例图。系统有两类用户：一类用户将在某台特定计算机上以服务器身份启动聊天室。其他用户将作为服务器的客户端，连接到聊天室，并可以选择聊天或离开。当一个人连接时，他必须提供一个昵称，以便其他人知道某条消息是谁发的，也便于发送私密消息。为了实现这一点，任何给定时间只能有一个用户使用某个特定的昵称。

我们将从客户端代码开始，因为它更简单。它只需要向服务器创建一个套接字，获取用户的昵称，请求用户输入要发送到服务器的聊天内容，并显示来自服务器的聊天文本。以下代码通过控制台界面实现了这些功能。

```scala
package scalabook.chat

import java.net._
import java.io._
import actors.Actor.actor
import annotation.tailrec

/**
 * 此应用程序运行一个聊天室的服务器，演示基于套接字的网络编程。
 */
object ChatClient {
  def main(args : Array[String]) {
    if(args.isEmpty) {
      println("Usage: scala ChatClient host [port]")
    } else {
      val port = if(args.length>1) args(1).toInt else 8000
      val sock = new Socket(args(0),port)
      val dis = new DataInputStream(new BufferedInputStream(sock.getInputStream()))
      val dos = new DataOutputStream(new
        BufferedOutputStream(sock.getOutputStream()))
      println("What is your handle for the chat room?")
      val name = readLine()
      dos.writeUTF(name)
      dos.flush()
      val response = dis.readUTF()
      if(response!=":quit") {
        actor { incoming(dis) }
        println("Welcome! Begin chatting.")
        outgoing(dos)
      } else {
        println("The server has rejected you.")
      }
      sock.close()
    }
    sys.exit(0)
  }

  @tailrec private def incoming(dis:DataInputStream) {
    val line = dis.readUTF()
    println(line)
    incoming(dis)
  }

  @tailrec private def outgoing(dos:DataOutputStream) {
    print("> ")
    val input = readLine().trim
    dos.writeUTF(input)
    dos.flush()
    if(input!=":quit") outgoing(dos)
  }
}
```

输入“:quit”作为聊天内容将终止聊天。请注意，传入消息是在单独的线程中处理的。该线程是使用`actor`快捷方式生成的。这样做的原因是，传入和传出的消息处理都包含阻塞方法，即**readUTF**和**readLine**。如果要在单个线程中处理这两者，我们就必须编写更复杂的代码，只在有内容可读时才读取，以避免阻塞。

**incoming**和**outgoing**方法中包含了一些我们以前没见过的新内容，一个名为**@tailrec**的注解。这个注解告诉Scala编译器，某个递归方法必须针对尾递归进行优化。如果不能，编译器应该生成错误。这意味着什么？尾递归是一个术语，用来描述只包含一个递归调用，并且在调用返回后不做大量工作的递归函数。这类递归函数通常可以转换为**while**循环。这样，你既能获得**while**循环的效率，又能获得递归的编程便利。如果Scala编译器无法将该函数转换为循环，**@tailrec**注解将强制产生错误。这一点很重要，因为你可能还记得，递归调用会消耗堆栈上的内存，如果递归太深，内存就会耗尽，程序会因堆栈溢出而崩溃。

服务器的代码稍微复杂一些，因为它要做的工作更多。它需要一个接受新连接的**ServerSocket**，每个套接字都需要有接收聊天消息的代码，还需要有让运行服务器的人输入命令来停止它的代码。与客户端一样，其中一些操作涉及阻塞调用，因此多线程会很有帮助。以下是编写该代码的一种方式。

```scala
package scalabook.chat

import java.net._
import java.io._
import actors.Actor._
import annotation.tailrec
import collection.mutable

/**
 * 此应用程序运行一个聊天室的服务器，演示基于套接字的网络编程。
 */
object ChatServer {
  def main(args : Array[String]) {
    val port = if(args.isEmpty) 8000 else args(0).toInt
    actor { startServer(port) }
    checkQuit()
    sys.exit(0)
  }

  private case class User(name:String, sock:Socket, dis:DataInputStream,
        dos:DataOutputStream)
  private val users = new mutable.HashMap[String,User] with
    mutable.SynchronizedMap[String,User] {}

  private def startServer(port:Int) {
    val ss = new ServerSocket(port)
    while(true) {
      val sock = ss.accept()
      actor { addUser(sock) }
    }
  }

  private def addUser(sock:Socket) {
    val dis = new DataInputStream(new BufferedInputStream(sock.getInputStream()))
    val dos = new DataOutputStream(new BufferedOutputStream(sock.getOutputStream()))
    val name = dis.readUTF()
    if(users.contains(name)) {
      dos.writeUTF(":quit")
      dos.flush()
      sock.close()
    } else {
      dos.writeUTF(":accept")
      dos.flush()
      val user = User(name,sock,dis,dos)
      users += name -> user
      doChat(user)
    }
  }

  @tailrec private def doChat(user:User) {
    val input = user.dis.readUTF().trim
    if(input!=":quit") {
      val index = input.indexOf("<-")
      if(index>0) {
        val oname = input.take(index).trim
        if(users.contains(oname)) {
          users(oname).dos.writeUTF(user.name+" -> "+input.drop(index+2).trim)
          users(oname).dos.flush()
        } else {
          user.dos.writeUTF(oname+" is not a valid handle.")
          user.dos.flush()
        }
      } else {
        val output = user.name+" : "+input
        for((name,ouser) <- users; if name!=user.name) {
          ouser.dos.writeUTF(output)
          ouser.dos.flush()
        }
      }
      doChat(user)
    } else {
      users.remove(user.name)
    }
  }

  @tailrec private def checkQuit() {
    if(readLine() != ":quit") checkQuit()
  }
}
```

main方法获取一个端口号，然后在单独的线程中启动服务器。主线程等待用户输入。

创建ServerSocket的函数进入一个无限循环，在其中接受连接，并通过actor创建的新线程调用addUser。这意味着每个客户端都可以在单独的线程中。实际上，actor库会管理线程，我们无法确定它会创建多少个线程来处理这些操作。

addUser方法从套接字获取流，并将它们包装在数据流中。然后读取一个字符串，该字符串应该是该客户端的昵称。请注意，服务器定义了一个名为User的case类，并维护一个将名称与用户关联的可变映射。这个可变映射是同步的，这样就不会因涉及多个线程而出现问题。这个映射使我们很容易确保永远不会有两个用户使用相同的昵称。它也使得发送私密消息更加容易。读取到的名称会与映射进行核对。如果映射中已经有该键，服务器会告诉客户端终止，然后关闭套接字。否则，它会告诉客户端已接受，向映射中添加一个新User，并继续执行doChat方法。

doChat方法是另一个尾递归方法。它从该用户的输入流中读取数据，并检查他们是否已断开连接。如果尚未断开，它要么向正确的用户发送一条私密消息，要么遍历所有用户并向每个人发送消息。如果用户退出，该用户名将从映射中移除，并且不再进行递归调用。你还会看到私密消息在此方法中处理。它会在文本中查找<-，并假定该符号之前的内容是用户昵称，之后的内容是要发送的消息。

在客户端和服务器的代码中，有多个地方可以看到输出流被刷新。实际上，每次写入后都会进行刷新。原因是大多数写入都很小，如果不刷新，整个内容就会滞留在缓冲区中。

输入这些文件并检查它们是否工作。如果你使用“localhost”作为机器名，你可以在单台计算机上与自己进行对话。玩了一段时间后，你可能会注意到一些不足之处。首先，它不太美观。这只是控制台中的纯文本。传入的聊天消息会打印在你正在输入的内容中间，这不仅看起来有点难看，而且可能难以使用，因为你无法跟踪自己正在写什么。

还有一些其他问题不仅仅是外观上的。目前，任何内容都可以作为昵称。只要你的用户不试图破坏系统，这不会造成问题。然而，有些名称可能会导致不太理想的行为。仅包含空白字符或开头或结尾包含空白字符的字符串会阻止私密消息的发送。服务器在接收到名称时应该进行更多的检查，以拒绝任何会导致问题的内容。

你可能注意到的另一个问题是，如果客户端在没有输入“:quit”的情况下断开连接，服务器中会出现异常。网络代码抛出的异常比使用文件的代码还要多。这段代码从不包含try/catch，但在每次调用readUTF或writeUTF时，它们都可能很有用。如果客户端不恰当地断开连接，会导致异常的通常是doChat中的第一行以及用于发送消息的writeUTF调用。解决办法是使用try/catch来检测链接何时失败。此时，它应该停止该用户的doChat，并将其从users映射中移除。这项练习留给读者完成。

## 网络安全

计算中的安全性和信息保障主题范围极其广泛，在我们这个现代、由计算机驱动的世界中至关重要。处理机密信息的程序需要努力保护这些信息。

