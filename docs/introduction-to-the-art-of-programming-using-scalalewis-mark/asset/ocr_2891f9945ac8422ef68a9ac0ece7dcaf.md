# 28.3 Graph Traversals

A maze is a special case of a very general data structure called a graph. If you draw a bunch of dots and put lines between them, you have made a graph. If you are following the end-of-chapter projects, you might well have a form of a graph in the code that you are writing. For example, the multiuser text game has rooms that are connected by exits. That is an example of a graph. For a graphical game you might have different rooms/levels that have doors or other connections between them. This is also a graph.

Using the foundation of code that we created for the maze, it is not to hard to make a DrawGraph type which the user can interact with by clicking on the drawing. The full code is shown here. It is fairly long in large part because of the ability to interactively edit the graph. There is a text field that can be used to enter an integer weight for edges that are added to the graph.

```
package scalabook.drawing

import java.awt.{Graphics2D,Color}
import java.awt.geom._
import scala.swing._
import scala.swing.event._
import actors.Actor
import collection.mutable

class DrawGraph(p:DrawTransform,nloc:Seq[Point2D],edges:Seq[(Int,Int,Int)],en:Int)
    extends DrawLeaf with Clickable {
  val parent = p
  import DrawGraph.{Node,Edge}
  private val nodes = mutable.Buffer[Node]()
  for(p <- nloc) nodes += new Node(p.getX(),p.getY())
  for((f,t,w) <- edges) nodes(f).edges ::= new Edge(nodes(f),nodes(t),w)
  private var endNode = if(en<0) {
    if(nodes.nonEmpty) nodes(0) else null
  } else nodes(en)
  @transient private var propPanel:Component = null
  @transient private var weight:TextField = null
  @transient private var clickAction:(MouseEvent,Double,Double)=>Unit = null
  @transient private var hoverNode:Node = null
  @transient private var hoverEdge:Edge = null
  @transient private var startNode:Node = null
  @transient private var (dx,dy) = (0.0, 0.0)
  @transient private var pathSet:Set[Node] = null

  def draw(g:Graphics2D) {
    def drawNode(n:Node) {
      g.setColor(if(n == endNode) Color.green else Color.black)
      g.fill(new Ellipse2D.Double(n.x-5,n.y-5,10,10))
      if(n==hoverNode) {
        g.setColor(Color.red)
        g.fill(new Ellipse2D.Double(n.x-4,n.y-4,8,8))
      }
    }
  }
```