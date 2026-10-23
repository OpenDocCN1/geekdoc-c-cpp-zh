
running on the Java Virtual Machine (JVM), and it runs slower than well-done specialized code for the same task. The rest of this section will talk about the setup and help you climb the learning curve. Our application is running on the JVM so that is not a problem for us. Our application is not highly dependent on performance either so the costs involved will not be significant and will be more than made up for by the convenience that RMI provides.

There are a number of steps that are required to get an application to use RMI. Here they are listed out.

- 1. Set up abstract types that specify the methods that can be called remotely. This is done by making traits for any types that you want to have remote access to. These traits need to inherit from java.rmi.Remote and they should only include methods that are abstract. So the only things in the trait should be declarations using def that do not specify any code to run.[^2] Each method needs to say it can throw a java.rmi.RemoteException. More on that below.
- 2. Write a class that extends java.rmi.server.UnicastRemoteObject with the trait you just created. You have to implement all the methods from the trait. Provide others as needed to make a complete implementation for your program.[^3]
- 3. Create a server application that binds the server object to an RMI registry. You do this by calling bind or rebind on java.rmi.Naming. Those methods take two arguments. The first is the name the registry will know the object by and the second is the object to bind. The bind method will throw an exception if that name is already in use. The rebind method will unbind the old object and bind this new one in its place.
- 4. Create a client application that uses the lookup method of java.rmi.Naming to get hold of the server object. The lookup method takes a single argument that is a URL for the server and object to look up. The protocol for the URL should be “rmi” and the name should be separated from the server by a slash. An example would be “rmi://computer.college.edu/ServerObjectName”. The name used here must match what the server used when it was bound to the registry.
- 5. Lastly you need to run rmiregistry then start up the server and clients. The rmiregistry program is part of the Java Development Kit (JDK) installation. For a Java program, the registry needs to have access to the compiled “.class” files for the application. This can be accomplished either by setting a CLASSPATH environment variable or by running rmiregistry in the base directory that the program compiles to.[^4] For a Scala program, odds are good that it will also need to be able to find certain Scala jar files. These are in the lib file of the Scala install directory. More details on this below in the example.

This might seem like a daunting list, but it really is only five steps and once you have done that it becomes much easier to extend your networked application. We will go back through the steps shortly as part of an example.

Before the example, there is one other detail of RMI that needs to be covered, the passing of arguments. Back in sections 7.8-7.9 we talked about how arguments are passed in Scala. The normal style is to pass a reference to the object with support for pass-by-name semantics as well. With RMI there are two different ways to pass things: pass-by-value and pass-by-reference. Which happens depends on the type of the object being passed. Pass-by-value implies that the object is copied and the other machine gets its own copy that is independent of the first one. This happens for Serializable data and includes the standard types you are used to working with in Scala. Objects with a type that implements Remote are passed as a remote reference. Instead of getting a copy of the object, the remote machine gets an object that implements the remote interface and which has the ability to communicate calls across the network. Methods called on these objects go back to the original value. The fact that there is network communication involved means that they are much slower than calls on local objects.

If you try to pass a value that is not serializable or remote, you will get an exception. The reason for this should be fairly clear to you, RMI is utilizing object streams to perform communication. Only objects that can be serialized will go through those. So the discussion of how to make objects serializable in 22.4.3 is relevant when using RMI as well.

To help you see how this all goes together, we will write another chat application that uses RMI instead of making direct use of sockets. We will run through the steps from above and point out what code is written for each one. Before we can write it though, we need to figure out what we are writing. This chat application is going to be a bit different from the last one. In particular, it will have a GUI for the client. The GUI will include not only standard chat elements, but a list of everyone logged onto the server. The idea is that users can send private messages by selecting one or more users from the list when they do their chats. Only the selected users will get their messages.

Starting with step 1 from the RMI steps, we lay out the types we want to have remote access to and put in the methods that we need to be able to call remotely. We start with the server.

```scala
package scalabook.chat

import java.rmi._

trait RMIServer extends Remote {
    @throws(classOf[RemoteException]) def connect(client:RMIClient):String
    @throws(classOf[RemoteException]) def disconnect(client:RMIClient):Unit
    @throws(classOf[RemoteException]) def getClients:Seq[RMIClient]
    @throws(classOf[RemoteException]) def publicMessage(client:RMIClient,
        text:String):Unit
}
```

The fundamental structure is that we have a trait that extends java.rmi.Remote. Inside of that trait there are four methods that we want to be able to call on a server remotely. These allow the client to connect, disconnect, and get a list of the current clients. There is also a method called publicMessage that should be called whenever a client sends out a message publicly. This allows the server to keep a brief history so that someone new logging in can see what has been discussed recently.

This code uses a new annotation that we have not seen before, @throws. This annotation allows us to specifically state exceptions that can be thrown by methods. It takes a single argument for the class of exception that might be thrown. This is not something that we have to do very often in Scala. The equivalent code is much more common in Java and in this case it is required for Scala because we need our code to work smoothly with the Java RMI libraries.

A second trait is set up for the methods that we want to be able to call remotely on the client. It looks like the following.

```scala
package scalabook.chat

import java.rmi._

trait RMIClient extends Remote {
    @throws(classOf[RemoteException]) def name:String
    @throws(classOf[RemoteException]) def message(sender:RMIClient, text:String):Unit
    @throws(classOf[RemoteException]) def clientUpdate(clients:Seq[RMIClient]):Unit
}
```

There are only three methods on the client. These get the name of the client, deliver a message to this client, and tell the client to update its list of clients logged into the server.

Looking at these two interfaces you might feel like there is something missing, methods on the server for sending out public or private chats. In the last chat, when one person wrote a chat message, that was sent to the server as just a String, and the server figured out what to do with it then sent it to the various chat participants. This uses the standard client-server network application structure where all communication goes through the server. This worked well for sockets and made our life easier. However, it is not very efficient as the server becomes a significant bottleneck. What is more, if you really wanted your messages to be private, you lack some security because they all have to go through the server for processing. Basically, the server sees everything and does a lot of work sending out all the messages.

RMI makes it easy for us to deviate from the client-server structure and use more of a peer-to-peer approach. The clients won’t just have a remote reference to the server, they will have remote references to all the other clients. This means that each client can call the message method on the other clients it wants messages to go to. This reduces pressure on the server and makes it less of a bottleneck. If we did not want to keep a history of what was being said on the server, chat traffic would not be sent to the server at all.

This next piece of code includes steps 2 and 3 for the server. Step 2 is in the class RMIServerImpl while step 3 is in the companion object.

```scala
package scalabook.chat

import java.rmi._
import java.rmi.server.UnicastRemoteObject
import collection.mutable

class RMIServerImpl extends UnicastRemoteObject with RMIServer {
    private val clients = mutable.Buffer[RMIClient]()
    private var history = mutable.ListBuffer("Server Started\n")

    @throws(classOf[RemoteException]) def connect(client:RMIClient):String = {
        clients += client
        sendUpdate
        history.mkString("\n")+"\n"
    }

    @throws(classOf[RemoteException]) def disconnect(client:RMIClient) {
        clients -= client
        sendUpdate
    }

    @throws(classOf[RemoteException]) def getClients:Seq[RMIClient] = clients
```

[^2]: Java has a construct called an interface that is purely abstract. That is what RMI actually requires. Scala traits with no data that have only abstract methods get compiled to Java interfaces.

[^3]: There are other servers you can use instead of UnicastRemoteObject. That one is specified because it is the most straightforward.

[^4]: If you are using Eclipse, there is a bin directory in the project that is the base directory for the compiled files.
