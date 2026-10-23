

if(x==ex && y==ey) 0
else if(x<0 || x>=maze.length || y<0 || y>=maze(x).length || maze(x)(y)<0) {
    1000000000
} else if(maze(x)(y)>0 && maze(x)(y)<=steps) {
    1000000000
} else {
    maze(x)(y) = steps
    drawing.refresh
    Thread.sleep(10)
    val ret = 1+(shortestPathFast(x+1,y,steps+1) min
                shortestPathFast(x-1,y,steps+1) min
                shortestPathFast(x,y+1,steps+1) min
                shortestPathFast(x,y-1,steps+1))
    ret
}
}

object DrawMaze {
    def apply(p:DrawTransform,data:xml.Node) = {
        new DrawMaze(p,
            data.text.trim.split("\n").map(_.split(",").map(_ .toInt).toSeq).toSeq,
            (data"@ex").text.toInt,
            (data"@ey").text.toInt)
    }

    def apply(p:DrawTransform) = {
        new DrawMaze(p,
            Seq(Seq( 0,-1, 0, 0, 0, 0, 0, 0, 0),
                Seq( 0,-1, 0,-1,-1,-1,-1,-1, 0),
                Seq( 0,-1, 0,-1, 0, 0, 0, 0, 0),
                Seq( 0,-1, 0,-1, 0,-1,-1,-1,-1),
                Seq( 0, 0, 0,-1, 0, 0, 0, 0, 0),
                Seq( 0,-1,-1,-1,-1,-1,-1,-1,-1, 0),
                Seq( 0,-1, 0, 0, 0, 0, 0, 0,-1, 0),
                Seq( 0,-1, 0,-1, 0, 0,-1, 0, 0, 0),
                Seq( 0,-1, 0,-1,-1, 0,-1,-1,-1,-1),
                Seq( 0, 0, 0,-1, 0, 0, 0, 0, 0, 0)),
            9,9)
    }
}

点击绘图中的迷宫会根据用户选择的选项激活不同的功能，其中包括寻找迷宫的最短路径。

## 28.2.1 重新审视基本方法

shortestPath 方法使用的是我们之前介绍过的方法。它会测试迷宫中的所有路径并返回最短路径的长度。该方法的代码如下所示。

```
private def shortestPath(x:Int,y:Int):Int = {
    if(x==ex && y==ey) 0
    else if(x<0 || x>=maze.length || y<0 || y>=maze(x).length || maze(x)(y)<0) {
        1000000000
} else {
  maze(x)(y) = -2
  drawing.refresh
  Thread.sleep(10)
  val ret = 1+(shortestPath(x+1,y) min
                shortestPath(x-1,y) min
                shortestPath(x,y+1) min
                shortestPath(x,y-1))
  maze(x)(y) = 0
  ret
}
}
```

基本情况是到达出口，返回 0 表示到达出口所需的步数，以及超出边界，返回 1000000000 作为不可能成为解且永远不会成为最小值的数字。这很重要，因为递归情况会在四个不同方向上进行递归调用并取其最小值。

行 maze(x)(y) = -2 是在迷宫上留下“面包屑”，以便计算机不会在循环中运行。你可以将其视为将递归推向基本情况。方格中的负值是基本情况，而该行在调用递归之前使另一个方格变为负值。这只能发生有限次数，然后递归就会用完空方格。完成四次递归调用后，该操作会被撤销，以便在未来以不同方式到达该方格的路径可以重新访问该方格。刷新绘图和休眠线程的代码只是为了动画化搜索过程。你可以减少休眠时间或完全删除该行，以加快解决耗时过长的迷宫的速度。

## 28.2.2 图形编辑

这是第一个真正需要用户使用鼠标与之交互的可绘制对象。解决迷宫需要一个起始位置，很希望能够调整它。合适的迷宫也应该是可编辑的，允许我们更改墙壁的位置以及出口的位置。将这种类型的编辑放入属性面板是可行的，但考虑到迷宫已经在绘图中绘制，这有点愚蠢。我们完全有理由让用户能够通过在绘图中的迷宫上的鼠标活动与迷宫进行交互。

当然，存在一些挑战。这些挑战来自三个不同的来源。最明显的挑战是用户将点击的面板位于 Drawing 类中，而不是 DrawMaze 或我们可能希望执行反应的其他 Drawable 类型中。另一个挑战是绘图中的元素可以被转换，因此面板上的点击位置与相对于绘制对象的点击位置之间存在非常间接的联系。最晦涩的挑战，也许是解决起来最困难的挑战是，我们不希望实现破坏序列化的更改。可以通过添加以下 trait 并对 Drawing 类进行一些更改来部分解决这三个问题。

```
package scalabook.drawing
```

```
import scala.swing._
import scala.swing.event._
import java.awt.geom._
```

```
trait Clickable {
    @transient private var lReactor:Reactor = null
    @transient protected var lastTransform:AffineTransform = null

    def reactor = {
        if(lReactor==null) {
            lReactor = new Reactor {}
            lReactor.reactions += {
                case me:MouseEvent =>
                    val dest = new Point2D.Double
                    lastTransform.inverseTransform(me.point,dest)
                    react(me,dest.x,dest.y)
            }
            lastTransform = new AffineTransform
        }
        lReactor
    }

    def react(evt:Event,cx:Double,cy:Double)
}
```

这个想法是，任何我们希望用户能够使用鼠标与之交互的可绘制对象都应继承此 trait。inverseTransform 的调用将点击位置从屏幕坐标转换为该可绘制对象的坐标。为了使这项工作正常进行，行 lastTransform = g.getTransform() 必须包含在该可绘制对象的 draw 方法中。

该 trait 本身包含用于创建能够很好地处理序列化的 Reactor 的代码，并跟踪可绘制对象最后一次绘制时使用的变换。它还提供了一种特殊类型，我们可以在 Drawing 中查找它以确定是否应将鼠标信息发送到某处。为了使这项工作正常进行，必须将以下代码添加到 Drawing 中。

```
// This was added in the declarations at the top.
@transient private var currentReactor:Reactor = null

// It is used in this code that was added at the end of the executeUnSelection
// code in the TreeSelectionListener.
    if(currentReactor!=null) {
        currentReactor.deafTo(drawPanel.mouse.moves,
            drawPanel.mouse.clicks,
            drawPanel.mouse.wheel)
    }
    d match {
        case r:Clickable =>
            currentReactor = r.reactor
            currentReactor.listenTo(drawPanel.mouse.moves,
                drawPanel.mouse.clicks,
                drawPanel.mouse.wheel)
        case _ =>
    }
```

类型信息对于检查所选 Drawable 是否是 Clickable 的子类型的 match 表达式很重要。如果是，它会记住 reactor 并使其监听面板上的鼠标事件。当选择其他内容时，该 reactor 将对这些事件变得聋。

与其创建 Clickable 类型，不如直接让可绘制对象继承自 Reactor，这很诱人。事实上，作者最初就是这样做的。然而，这会破坏序列化，因为 Reactor 类型包含指向不可序列化数据的链接。代码使用新创建的 Clickable trait 进行了重写，以修复序列化问题，并且还带来了将转换代码合并的好处。完整的 Event 会传递给 react 方法以允许匹配，并提供屏幕坐标以防需要。

在 DrawMaze 类内部，react 方法使用整数除法找到被点击的块，然后使用名为 clickAction 的函数变量来确定点击时发生的情况。clickAction 的值在用户从属性面板中选择单选按钮时设置。这种方法将行为从 react 方法抽象出来，并直接放入单选按钮代码中，以便向用户显示的名称和行为的代码相邻。请注意，路径查找调用使用 Actor.actor 在单独的线程中运行，因为这些操作可能需要相当长的时间，我们希望事件处理线程可以自由地为动画重绘。

## 28.2.3 优化迷宫

如果你在第 15 章或在此代码中玩过迷宫，你可能会注意到一些事情。如果你不断拆除墙壁并运行最短路径函数，随着墙壁的移除，函数会变得越来越慢。某一时刻，你会使迷宫空到足以让函数运行的时间超过你有耐心让它运行的时间。这是因为基本算法会测试所有可能的路径以找到最短路径。空迷宫中可能存在的路径数量极其庞大。DrawMaze 允许你更改大小。10x10 的迷宫如果空置，足以花费比人类寿命长数倍的时间，20x20 或更大的迷宫会使情况变得更糟。

有办法解决这个问题。我们在这里讨论的方法使面包屑变得更智能，以便它们可以提供额外信息，从而在完全探索之前就消除没有机会成为理想的路径。执行此操作的代码如下所示。

```
private def shortestPathFast(x:Int,y:Int,steps:Int):Int = {
  if(x==ex && y==ey) 0
  else if(x<0 || x>=maze.length || y<0 || y>=maze(x).length || maze(x)(y)<0) {
    1000000000
  } else if(maze(x)(y)>0 && maze(x)(y)<=steps) {
    1000000000
  } else {
    maze(x)(y) = steps
    drawing.refresh
    Thread.sleep(10)
    val ret = 1+(shortestPathFast(x+1,y,steps+1) min
                  shortestPathFast(x-1,y,steps+1) min
                  shortestPathFast(x,y+1,steps+1) min
                  shortestPathFast(x,y-1,steps+1))
    ret
  }
}
```

这看起来与早期版本非常相似，但函数多了一个参数，多了一个基本情况，并且面包屑不会被拾取。额外的参数跟踪当前路径中已采取的步数。面包屑除了标记你是否到过某个方格外，还会跟踪到达该方格所需的步数

