```
private def foreachCollaborator(f:Collaborator=>Unit) {
  for(c <- sketches.keys) try {
    f(c)
  } catch {
    case ex:RemoteException =>
  }
}
```

```
@throws(classOf[RemoteException]) def name:String = nameField.text
```

```
@throws(classOf[RemoteException]) def post(text:String) {
  chatArea.append(text+"\n")
}
```

```
@throws(classOf[RemoteException]) def requestSketch:Array[Byte] = {
  ImageHandling.imageAsBytes(sketch)
}
```

```
@throws(classOf[RemoteException]) def
  updateSketch(who:Collaborator,img:Array[Byte]) {
    sketches(who)=ImageHandling.imageFromBytes(img)
    sketchPanel.sketchSlider.max = sketches.size-1
    sketchPanel.repaint()
}
```

```
private[drawing] def sketchUpdated() {
  val bytes = ImageHandling.imageAsBytes(sketch)
  foreachCollaborator(c => {
    c.updateSketch(this,bytes)
  })
}
```

```
@throws(classOf[RemoteException]) def addDrawing(title:String,drawing:Drawing) {
  drawings += title->drawing
  SharedPanel.setSize()
  SharedPanel.repaint()
}
```

```
object CollabororImpl {
  val sketchSize = 1000
}
```

The class starts with the creation of a sketch image that is filled in with transparent color. After that, is code that joins the collaboration, then uses the return from that to get the sketches of all the other collaborators as well as all shared drawings. This is followed by code to set up the GUI in a frame and two helper methods that make it easier to perform actions on the collaborators without worrying about exceptions. The implementation class ends with definitions of the five remote methods that were put into the trait. A companion object includes a constant that can be used to size the images used in the sketches.

The CollabororImpl depends on code in two other files. The fact that BufferedImage is not serializable presents a problem for sending sketches between the collaborators. If you look in the remote interface, sketches are passed around using the type Array[Byte].