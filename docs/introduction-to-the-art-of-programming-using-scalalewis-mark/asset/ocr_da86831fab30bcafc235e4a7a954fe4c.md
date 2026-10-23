Typing in “quit” as a chat line will terminate the chat. Note that the incoming messages are handled in a separate thread. This thread is spawned using the actor shortcut. The reason for doing this is that both incoming and outgoing message handling contain blocking methods in the form of **readUTF** and **readline**. To handle both in a single thread we would have to write more elaborate code that only reads when there are things to read to prevent blocking.

The **incoming** and **outgoing** methods include something new that we have not seen before, an annotation called **@tailrec**. This annotation tells the Scala compiler that a particular recursive method must be optimized for tail recursion. If it can not, the compiler should generate an error. What does this mean? Tail recursion is a term used to describe a recursive function that contains only one recursive call and does not do significant work after the call returns. These types of recursive functions can often be transformed into **while** loops. In this way you can get the efficiency of a **while** loop while getting the programming benefits of recursion. The **@tailrec** annotation will force an error if the Scala compiler can not convert the function to a loop. This is important, because you might recall that recursive calls consume memory on the stack, and if you recurse too deeply, you run out of memory and the program crashes from a stack overflow.

The code for the server is a bit more complex because it has more work to do. It needs to have a **ServerSocket** that is accepting new connections, code for each socket that takes in chat messages, and code that lets the person who runs the server enter a command to stop it. Like the client, some of these things involve blocking calls so multithreading can be helpful. Here is one way of writing the code.

```
```scala
package scalabook.chat

import java.net._
import java.io._
import actors.Actor._
import annotation.tailrec
import collection.mutable

/**
 * This application runs a server for a chat room that demonstrates the use of
 * socket based networking.
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
}
```
```