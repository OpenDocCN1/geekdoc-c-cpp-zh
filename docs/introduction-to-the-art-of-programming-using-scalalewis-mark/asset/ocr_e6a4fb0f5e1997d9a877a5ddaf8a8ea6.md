```
private val chatField = new TextField("") {
  listenTo(this)
  reactions += {
    case e:event.EditDone => if(text.trim.nonEmpty) {
      val recipients = if(userList.selection.items.isEmpty) {
        server.publicMessage(RMIClientImpl.this,text)
        clients
      } else {
        userList.selection.indices.map(clients).toSeq
      }
      recipients.foreach(r => try {
        r.message(RMIClientImpl.this,text)
      } catch {
        case ex:RemoteException => chatText.append("Couldn't send to one recipient.")
      })
      text = ""
    }
  }
}

private val frame = new MainFrame {
  title = "Chat"
  contents = new BorderPanel {
    import BorderPanel.Position._
    val scrollList = new ScrollPane(userList)
    scrollList.preferredSize = new Dimension(200,500)
    layout += scrollList -> West
    layout += new BorderPanel {
      val scrollChat = new ScrollPane(chatText)
      scrollChat.preferredSize = new Dimension(500,200)
      layout += scrollChat -> Center
      layout += chatField -> South
    } -> Center
  }
  listenTo(this)
  reactions += {
    case e:event.WindowClosing => server.disconnect(RMIClientImpl.this)
    case _ =>
  }
}
frame.visible = true

@throws(classOf[RemoteException]) def name:String = myName

@throws(classOf[RemoteException]) def message(sender:RMIClient,text:String) {
  chatText.append(sender.name+" : "+text+"\n")
}

@throws(classOf[RemoteException]) def clientUpdate(cls:Seq[RMIClient]) {
  clients = cls
  if(userList!=null) userList.listData = cls.map(c =>
    try {
      c.name
    } catch {
```