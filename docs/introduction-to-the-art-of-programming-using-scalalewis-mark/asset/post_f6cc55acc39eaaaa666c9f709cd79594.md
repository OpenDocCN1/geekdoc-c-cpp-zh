
![](img/157fcf510c119278e4b1267c62717fa8_636_0.png)

FIGURE 23.1: This figure shows the different use-cases for the socket/stream-based chat program that we want to write.

java.io.ObjectInputStream. If you use this approach, you can get the data out with a java.io.ByteArrayOutputStream wrapped in the appropriate data or object output stream. This approach is not all that much simpler.

### 23.2.3 Streams from Sockets

For UDP we saw that data has to be packed into the DatagramPackets to be sent to other machines and then unpacked when they arrive. We did not discuss how data is sent using the plain Socket class for TCP. To do this, we use streams. The Socket class has the following methods.

```
getInputStream() : InputStream
getOutputStream() : OutputStream
```

These methods do pretty much exactly what you would expect them to given their names. If you call getInputStream on a socket, it will return an implementation of InputStream that connects to the socket so that when data is read from it, data sent through the socket from the other machine will be read. You can wrap these streams in the same manner you would have wrapped streams attached to files. This is part of the flexibility of the stream library. You can write code that uses an InputStream or an OutputStream and it can work regardless of the type of stream that is passed to it. So the same code can be used to work with sockets or files.

To see how this works, we will create a simple chat room with a server and the ability to include multiple clients. To see what we really want, we should do some analysis. Figure 23.1 shows a use-case diagram for what we want to do. There are two types of users of the system, one will start the chat room as a server on a particular computer. Other users will be clients of the server and will connect into the room and have options for chatting and leaving. When a person connects they have to give a handle they will go by so that others will know who has chatted certain messages and so that private messages can be sent. For this to work, only a single user at any given time can have a particular handle.

We will start with the client code because it is simpler. It only needs to make a socket to the server, get the user's handle, ask the user for chat lines that are sent to the server, and display chat text coming from the server. Here is code that does that with a console interface.

```scala
package scalabook.chat

import java.net._
import java.io._
import actors.Actor.actor
import annotation.tailrec

/**
 * This application runs a server for a chat room that demonstrates the use of
 * socket based networking.
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

Typing in “:quit” as a chat line will terminate the chat. Note that the incoming messages are handled in a separate thread. This thread is spawned using the actor shortcut. The reason for doing this is that both incoming and outgoing message handling contain blocking methods in the form of **readUTF** and **readLine**. To handle both in a single thread we would have to write more elaborate code that only reads when there are things to read to prevent blocking.

The **incoming** and **outgoing** methods include something new that we have not seen before, an annotation called **@tailrec**. This annotation tells the Scala compiler that a particular recursive method must be optimized for tail recursion. If it can not, the compiler should generate an error. What does this mean? Tail recursion is a term used to describe a recursive function that contains only one recursive call and does not do significant work after the call returns. These types of recursive functions can often be transformed into **while** loops. In this way you can get the efficiency of a **while** loop while getting the programming benefits of recursion. The **@tailrec** annotation will force an error if the Scala compiler can not convert the function to a loop. This is important, because you might recall that recursive calls consume memory on the stack, and if you recurse too deeply, you run out of memory and the program crashes from a stack overflow.

The code for the server is a bit more complex because it has more work to do. It needs to have a **ServerSocket** that is accepting new connections, code for each socket that takes in chat messages, and code that lets the person who runs the server enter a command to stop it. Like the client, some of these things involve blocking calls so multithreading can be helpful. Here is one way of writing the code.

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

The main method gets a port number, then starts the server in a separate thread. The main thread waits for input from the user.

The function that creates the ServerSocket goes into an infinite loop where it accepts connections and calls addUser in new threads created with actor. This means that each client could be in a separate thread. In reality, the actor library handles threads and we can not be certain of how many threads it will create to do the processing.

The addUser method gets streams from the socket and wraps them in data streams. It then reads a string which should be the name/handle of that client. Note that the server defined a case class called User and keeps a mutable map associating names with users. This mutable map is synchronized so that it does not run into problems with the multiple threads involved. This map allows us to easily ensure that there are never two users with the same handle. It also makes it easier to do private messages. The name that is read in is checked against the map. If the map already has that as a key, it tells the client to terminate before closing the socket. Otherwise, it tells the client that it was accepted, adds a new User to the map, and moves on to the doChat method.

The doChat method is another tail recursive method. It reads from the input stream of that user and checks to see if they have disconnected. If they have not, it either sends out a private message to the correct user or runs through all users sending everyone a message. If they quit, that user name is removed from the map and there is no recursive call. You will also see that private messages are handled in this method. It looks for <- in the text and assumes that what is before that is a user handle and what is after it is the message to send.

There are several places in both the client and the server where you see output streams getting flushed. In fact, there is a flush after every write. The reason is that most of the writes will be small and the whole thing will sit in the buffer if we do not flush it.

Enter these files and check that they work. If you use “localhost” as the machine name you can have conversations with yourself on a single computer. After playing with this for a while you might notice some areas in which it is lacking. First, it is not very pretty. It is plain text in the console. Chat messages that come in will print in the middle of what you are typing in a way that can make it not only a bit ugly, but can also make it hard to use as you can not keep track of what you are writing.

There are some other problems that are more than cosmetic. Currently anything is allowed for a handle. That will not cause a problem as long as your users are not trying to break the system. However, there are names that could lead to less than ideal behavior. Strings that are only whitespace or that include whitespace at the beginning or end will prevent private messages from being sent. More checking should be put into the server when it receives a name to reject anything that would cause a problem.

The other problem you might have noticed is that if a client disconnects without entering “:quit” there is an exception in the server. Networking code throws even more exceptions than code using files. This code never includes a try/catch, but they could be useful around every call to readUTF or writeUTF. The ones that will cause exceptions if a client disconnects improperly are the first line in doChat and the writeUTF calls for sending messages. The cure for this is having a try/catch that will detect when a link fails. At that point it should stop the doChat for that user and remove it from the users map. Doing this is left as an exercise.

## Network Security

The topics of security and information assurance in computing are extremely broad in scope and of critical importance in our modern, computer-driven world. Programs that deal with confidential information need to take efforts to protect that information
