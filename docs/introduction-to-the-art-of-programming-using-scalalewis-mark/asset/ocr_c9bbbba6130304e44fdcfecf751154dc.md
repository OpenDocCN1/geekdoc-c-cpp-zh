```
@throws(classOf[RemoteException]) def publicMessage(client:RMIClient,text:String)
{
  history += client.name+" : "+text
  if(history.length>10) history.remove(0)
}

private def sendUpdate {
  val deadClients = clients.filter(c =>
    try {
      c.name
      false
    } catch {
      case ex:RemoteException => true
    }
  )
  clients --= deadClients
  clients.foreach(_.clientUpdate(clients))
}
}

object RemoteServerImpl {
  def main(args:Array[String]) {
    val server = new RMIServerImpl
    Naming.rebind("ChatServer",server)
  }
}
```

The class defines two fields for storing the clients and history, then implements the four methods from the interface with rather short methods. You can see that the connect method returns the history. Both connect and disconnect make use of the one private method that is also included, sendUpdate. This method sends out a message to all the clients letting them know that the client list has been modified. This method is a bit longer because it first runs through all the clients and calls their name method. That value is not used for anything, but it serves as a check that the client is still there. This is part of a filter operation that is checking for dead clients. The clients that can not be reached are removed from the list before that list is sent out to all the active clients.

The main method for running the server is remarkably simple. It makes an instance of RemoteServerImpl then uses rebind to bind it to the rmiregistry.

This next piece of code shows steps 2 and 4 for the client. This code is a bit longer because it includes support for the GUI. Even that does not make it all that long.

```
package scalabook.chat

import java.rmi._
import java.rmi.server.UnicastRemoteObject
import collection.mutable
import swing._

class RMIClientImpl(myName:String,server:RMIServer) extends UnicastRemoteObject with RMIClient {
private val chatText = new TextArea(server.connect(this))
chatText.editable = false
private var clients = server.getClients
private val userList = new ListView(clients.map(_.name))
```