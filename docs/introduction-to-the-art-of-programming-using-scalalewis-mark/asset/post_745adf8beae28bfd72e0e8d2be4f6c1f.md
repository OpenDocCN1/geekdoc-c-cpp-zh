
/**
 * This implementation will run on the clients and bring up a window that will show
 * thumb nails of the shared drawings, a simple sketch pad, and chat window.
 */
class CollaboratorImpl(server:CollaborationServer) extends UnicastRemoteObject
        with Collaborator {
  private[drawing] val sketch = {
    val img = new BufferedImage(CollaboratorImpl.sketchSize,
        CollaboratorImpl.sketchSize, BufferedImage.TYPE_INT_ARGB)
    for(i <- 0 until img.getWidth; j <- 0 until img.getHeight)
      img.setRGB(i,j,0)
    img
  }

  private[drawing] val (sketches,drawings) = {
    val (cols,draws) = server.joinCollaboration(this)
    mutable.Map(cols.map(c => {
      try {
        Some(c -> ImageHandling.imageFromBytes(c.requestSketch()))
      } catch {
        case ex:RemoteException => None
      }
    }).filter(!_.isEmpty).map(_get:_*) -> mutable.Buffer(draws:_*)
  }

  private val nameField = new TextField("Name")
  private val chatField = new TextField
  private val chatArea = new TextArea
  chatArea.editable = false

  object SharedPanel extends Panel {
    preferredSize = new Dimension(150,200)
    val bigFont = new Font(Font.SERIF,Font.PLAIN,75)

    override def paint(g:Graphics2D) {
      g.setPaint(Color.white)
      g.fillRect(0,0,size.width,size.height)
      g.scale(0.15,0.15)
      g.setPaint(Color.black)
      for(i <- drawings.indices) {
        drawings(i)._2.renderTo(g)
        g.setPaint(Color.black)
        g.setFont(bigFont)
        g.drawString(drawings(i)._1,0,100/0.15f)
        g.translate(0,200/0.15)
      }
    }
  }

  def setSize() {
    preferredSize = new Dimension(150,200*drawings.size)
  }

  listenTo(mouse.clicks)
  reactions += {
case mc:MouseClicked =>
if(mc.clicks==2 && mc.point.y<drawings.size*200) {
val index = mc.point.y/200
DrawingMain.addDrawing(drawings(index)._1,drawings(index)._2)
}
}

val sketchPanel = new SketchPanel(this)

sketchUpdated()

import BorderPanel.Position._

val collabSplit = new SplitPane(Orientation.Horizontal,sketchPanel,
new BorderPanel {
layout += chatField -> North
layout += chatArea -> Center
})

private val frame = new Frame {
contents = new BorderPanel {
layout += new BorderPanel {
layout += new Label("Name") -> West
layout += nameField -> Center
} -> North
layout += new ScrollPane(SharedPanel) -> West
layout += collabSplit -> Center
}
listenTo(chatField)
reactions += {
case ed:EditDone =>
if(chatField.text.trim.nonEmpty) {
foreachCollaborator(_.post(name+" : "+chatField.text))
chatField.text = ""
}}
size = new Dimension(800,600)
}

def showFrame {
frame.visible = true
collabSplit.dividerLocation = 0.7
}

private def forCollaborators[A](f:Collaborator=>A):Seq[A] = {
(for(c <- sketches.keys) yield try {
Some(f(c))
} catch {
case ex:RemoteException => None
}).toSeq.filter(!_.isEmpty).map(_.get)
}

private def foreachCollaborator(f:Collaborator=>Unit) {
  for(c <- sketches.keys) try {
    f(c)
  } catch {
    case ex:RemoteException =>
  }
}

@throws(classOf[RemoteException]) def name:String = nameField.text

@throws(classOf[RemoteException]) def post(text:String) {
  chatArea.append(text+"\n")
}

@throws(classOf[RemoteException]) def requestSketch:Array[Byte] = {
  ImageHandling.imageAsBytes(sketch)
}

@throws(classOf[RemoteException]) def
  updateSketch(who:Collaborator,img:Array[Byte]) {
    sketches(who)=ImageHandling.imageFromBytes(img)
    sketchPanel.sketchSlider.max = sketches.size-1
    sketchPanel.repaint()
}

private[drawing] def sketchUpdated() {
  val bytes = ImageHandling.imageAsBytes(sketch)
  foreachCollaborator(c => {
    c.updateSketch(this,bytes)
  })
}

@throws(classOf[RemoteException]) def addDrawing(title:String,drawing:Drawing) {
  drawings += title->drawing
  SharedPanel.setSize()
  SharedPanel.repaint()
}

object CollaboratorImpl {
  val sketchSize = 1000
}

The class starts with the creation of a sketch image that is filled in with transparent color. After that, is code that joins the collaboration, then uses the return from that to get the sketches of all the other collaborators as well as all shared drawings. This is followed by code to set up the GUI in a frame and two helper methods that make it easier to perform actions on the collaborators without worrying about exceptions. The implementation class ends with definitions of the five remote methods that were put into the trait. A companion object includes a constant that can be used to size the images used in the sketches.

The CollaboratorImpl depends on code in two other files. The fact that BufferedImage is not serializable presents a problem for sending sketches between the collaborators. If you look in the remote interface, sketches are passed around using the type Array[Byte].

mouseDown=true
sx=x
sy=y
ex=x
ey=y
}
def released(x:Int,y:Int) {
    ex=x
    ey=y
    drawCurrent
    mouseDown=false
}
def dragged(x:Int,y:Int) {
    ex=x
    ey=y
}
}
object LineDrawer extends PositionDrawer {
    def draw(g:Graphics2D) { if(mouseDown) g.draw(new Line2D.Double(sx,sy,ex,ey)) }
}
object RectangleDrawer extends PositionDrawer {
    def draw(g:Graphics2D) { if(mouseDown) g.fill(new Rectangle2D.Double(sx min ex, sy min ey, (ex-sx).abs, (ey-sy).abs)) }
}
object EllipseDrawer extends PositionDrawer {
    def draw(g:Graphics2D) { if(mouseDown) g.fill(new Ellipse2D.Double(sx min ex, sy min ey, (ex-sx).abs, (ey-sy).abs)) }
}
var curDrawer:Drawer = FreeDrawer
val buttons = new GridPanel(6,1) {
    val b = Array(
        new ToggleButton {
            selected = true
            action = Action("Free")(curDrawer = FreeDrawer)
        },
        new ToggleButton { action = Action("Line")(curDrawer = LineDrawer) },
        new ToggleButton { action = Action("Rectangle")(curDrawer = RectangleDrawer) },
        new ToggleButton { action = Action("Ellipse")(curDrawer = EllipseDrawer) }
    )
    val group = new ButtonGroup(b:_*)
    b.foreach(contents += _)
    contents += Button("Clear") {
        for(i <- 0 until collab.sketch.getWidth; j <- 0 until collab.sketch.getHeight)
            collab.sketch.setRGB(i,j,0)
        collab.sketchUpdated()
    }
    contents += Button("Color") {
        val c = javax.swing.JColorChooser.showDialog(peer,"Select Color",curColor)
        if(c!=null) curColor = c
    }
}
val sketchDraw = new Panel {

override def paint(g:Graphics2D) {
    g.setPaint(Color.white)
    g.fillRect(0,0,size.width,size.height)
    val sketchSeq = collab.sketches.toSeq
    for(index <- 0 until collab.sketches.size) {
        val (c,i) = sketchSeq((index+sketchSlider.value)%sketchSeq.size)
        g.drawImage(i,0,0,null)
    }
    g.setPaint(curColor)
    curDrawer.draw(g)
}
import BorderPanel.Position._
layout += sketchDraw -> Center
layout += buttons -> East
layout += sketchSlider -> North
listenTo(sketchDraw.mouse.clicks,sketchDraw.mouse.moves,sketchSlider)
reactions += {
    case mp:MousePressed =>
        curDrawer.pressed(mp.point.x,mp.point.y)
        sketchDraw.repaint()
    case mp:MouseDragged =>
        curDrawer.dragged(mp.point.x,mp.point.y)
        sketchDraw.repaint()
    case mp:MouseReleased =>
        curDrawer.released(mp.point.x,mp.point.y)
        sketchDraw.repaint()
    case vc:ValueChanged =>
        sketchDraw.repaint()
}
The class gets passed the CollaboratorImpl because it needs to have access to the sketch and some other parts of that object. Much of this class is focused on dealing with the user drawing to his/her sketch. There is a group of ToggleButtons that allow the user to select how they are drawing as well as other buttons to clear the sketch and select a color. The ToggleButtons are added to a ButtonGroup so that only one can be selected at a time.

The State Pattern is used to make it so that mouse input is interpreted properly for each different type of thing that the user can draw [6]. The way this works is that we have a trait called Drawer that has four abstract methods in it. These methods deal with the mouse being pressed, released, and dragged as well as how to draw what would be drawn if the mouse were released. Each style of drawing is represented by an object that extends this interface. A mutable variable named curDrawer stores a reference to one of these objects, the one associated with the currently selected drawing mode. Events are passed through to that object, and are placed where the proper shape needs to be drawn to screen of an image.

You might be tempted to write code like this by keeping an integer value telling you what style you are drawing in and then having multiple if/else conditions to take the right action in different situations. While that approach can work, it is less flexible and more bug prone. The real advantage of the abstraction shown here is how easy it is to add new drawing modes. You simply add a new button to the GUI and a new Drawer object for handling that style and it works. This is an example of using abstraction to make code more flexible.
