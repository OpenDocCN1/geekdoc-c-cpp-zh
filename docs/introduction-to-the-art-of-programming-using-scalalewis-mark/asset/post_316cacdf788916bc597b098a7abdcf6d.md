
there on the shortest path so far. The extra base case is for a room that is reached taking more steps than the current step count. In that situation, the path can not possibly be the shortest and the recursion is terminated.

If you make the maze big enough, even this approach will be insufficient. If you test an empty 30 by 30 maze you will discover this for yourself. An alternate approach is to abandon recursion completely and do a *breadth-first* search of the maze. By its nature, recursion is *depth-first*. This means that it goes as far down one path as possible before trying another path. For a shortest-path algorithm, the first solution reached is the winner. For that reason, it is more efficient to try all paths at the same time, taking one step forward on each. That approach works very well of a maze, but there are some problems for which the number of independent paths is so large that you can not keep track of all the different paths without running out of memory. The breadth-first approach also does not help with problems such as finding the longest path or counting the number of paths.

## How Many Paths Are There?

You can empirically check to see that an empty maze takes a long time to solve. With a little work we can estimate more accurately how long it would take. Imagine a 10 by 10 empty maze. In the recursive case, the function calls itself four times. Some of those will lead to base cases and immediately return. For our estimate we will say that two of the calls are not base cases. So the initial call splits to two, which split to four, and so on. After n steps in the recursion, there are roughly 2^n paths being worked on. The longest path in a 10 by 10 maze is 100 steps. To keep things simple we will stick with that number for how deep the recursion goes. It is an overestimate, but it is somewhat offset by assuming only two branches. This implies on the order of 2^100 paths.

Hopefully, it is clear that 2^100 is a very big number. Such big numbers can be hard for people to really comprehend. After all, computers are really fast. Modern computers run at clock frequencies of several gigahertz. To help us put this number into perspective, assume that your computer can do 10^9 recursive calls each second. We then use two other rough estimates: 2^10 ~ 10^3 and 1yr ~ 3 × 10^7 sec. This gives us the following:

2^100 ops ~ 10^30 ops ~ 10^21 sec ~ 3 × 10^13 yr.

That is a few times longer than the best estimates for the current age of the Universe.

This type of exponential growth is common for recursive algorithms. If each non-base case calls the function m times and this goes n calls deep, then there will be m^n total calls. For some problems, this seems to be unavoidable. A lot of effort goes into trying to find ways of getting around this. You should learn about approaches to dealing with this later in your studies.

## 28.3 Graph Traversals

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

```
def drawEdge(e:Edge) {
    g.setColor(if(e==hoverEdge) Color.red else Color.black)
    g.draw(new Line2D.Double(e.from.x,e.from.y,e.to.x,e.to.y))
    g.drawString(e.weight.toString,0.5f*(e.from.x+e.to.x).toFloat,
        0.5f*(e.from.y+e.to.y).toFloat)
}

for(n <- nodes) {
    drawNode(n)
    for(e <- n.edges; if(nodes.indexOf(e.from)<nodes.indexOf(e.to))) {
        drawEdge(e)
    }
    g.setPaint(Color.black)
    if(startNode!=null) g.draw(new Line2D.Double(startNode.x,startNode.y,dx,dy))
}
if(pathSet!=null) {
    g.setPaint(Color.blue)
    for(n <- pathSet) {
        g.fill(new Ellipse2D.Double(n.x-2,n.y-2,4,4))
    }
}

def propertiesPanel() : Component = {
    if(propPanel == null) {
        import BorderPanel.Position._
        propPanel = new BorderPanel {
            val radioButtons = Seq(
                new RadioButton { action = Action("Add Node") {
                    clickAction = (e,x,y) => e match {
                        case mc:MouseClicked =>
                            nodes += new Node(x,y)
                            if(nodes.length==1) endNode = nodes(0)
                        case _ =>
                    }
                }},
                new RadioButton { action = Action("Add Edge") {
                    clickAction = (e,x,y) => e match {
                        case mp:MousePressed =>
                            if(hoverNode!=null) {
                                startNode = hoverNode
                                dx = startNode.x
                                dy = startNode.y
                            }
                        case mp:MouseDragged =>
                            if(startNode!=null) {
                                dx = x
                                dy = y
                            }
                        case mp:MouseReleased =>
                            if(startNode!=null && hoverNode!=null) {
                                startNode.edges ::= new
                                    Edge(startNode,hoverNode,weight.text.toInt)
```

```
hoverNode.edges ::= new
    Edge(hoverNode,startNode,weight.text.toInt)
}
    startNode = null
    case _ =>
}
} },
new RadioButton { action = Action("Move Node") {
    clickAction = (e,x,y) => e match {
        case mp:MousePressed =>
            if(hoverNode!=null) {
                startNode = hoverNode
                dx = startNode.x
                dy = startNode.y
            }
        case mp:MouseDragged =>
            if(startNode!=null) {
                startNode.x = x
                startNode.y = y
                dx = x
                dy = y
            }
        case mp:MouseReleased =>
            if(startNode!=null && hoverNode!=null) {
                startNode.x = x
                startNode.y = y
            }
            startNode = null
        case _ =>
    }
} },
new RadioButton { action = Action("Remove") {
    clickAction = (e,x,y) => e match {
        case mc:MouseClicked =>
            if(hoverNode!=null) {
                nodes -= hoverNode
                for(n <- nodes) n.edges = n.edges.filter(_.to != hoverNode)
                if(hoverNode==endNode && nodes.nonEmpty) endNode = nodes(0)
                pathSet = null
            } else if(hoverEdge!=null) {
                hoverEdge.from.edges = hoverEdge.from.edges.filterNot(_ sameAs hoverEdge)
                hoverEdge.to.edges = hoverEdge.to.edges.filterNot(_ sameAs hoverEdge)
            }
        case _ =>
    }
} },
new RadioButton { action = Action("Set End") {
    clickAction = (e,x,y) => e match {
        case mc:MouseClicked =>
            if(hoverNode!=null) {
                endNode = hoverNode
            }
        case _ =>
```
