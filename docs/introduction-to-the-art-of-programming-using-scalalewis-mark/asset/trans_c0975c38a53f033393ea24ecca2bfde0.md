

# 27.3.2 练习

+   1. 在 Eclipse 中测试每一种内置的重构选项。
+   
+   2. 该书的网站上有一些有异味代码的示例。逐一查看它们，弄清楚为什么它有异味，并对其进行重构。

# 27.3.3 项目

与其为每个项目提供单独的描述，本章更侧重于一般性描述。浏览你所编写的代码并找出其中的异味。当你找到它们时，对其进行重构，使其不再有异味。

今后，很可能会出现需要你更改项目某些设计方面的项目。当这些情况出现时，请确保先重构代码，然后再添加新功能。力求不要混合步骤。先进行重构并验证代码的工作方式与之前相同，然后再对其进行添加。

# 第 28 章

# 递归

+   28.1 复习 ......................................................................................... 709
+   28.2 项目集成：迷宫 ........................................................................... 710
+   28.2.1 重新审视基本方法 ................................................................... 713
+   28.2.2 图形编辑 ............................................................................... 714
+   28.2.3 优化迷宫 ............................................................................ 716
+   28.3 图遍历 .................................................................................... 718
+   28.4 分而治之 ................................................................................. 725
+   28.4.1 归并排序 ................................................................................ 725
+   28.4.2 快速排序 ................................................................................ 727
+   28.4.3 公式解析 ................................................................................. 730
+   28.5 章节结束材料 ............................................................................. 731
+   28.5.1 概念总结 ........................................................................... 731
+   28.5.2 练习 ........................................................................................ 732
+   28.5.3 项目 ......................................................................................... 732

递归首次出现在本书第 6 章中，当时它被用来提供基本的迭代。这在第 15 章中得到了扩展，其中利用了栈的内存，使用递归函数，这些函数会调用自身不止一次。本章将重新审视递归的概念，以帮助你在脑海中巩固它。¹ 接下来的三章将利用递归，这使得现在提供复习并将其整合到我们的项目中成为理想时机。

# 28.1 复习

递归函数只不过是一个调用自身的函数。这意味着它是用自身来定义的。这种看似循环的定义方式之所以可行，是因为所有递归函数都需要某种形式的基线情况，在该情况下它们不会调用自身。其他情况应朝着基线情况进展。仅调用自身一次的递归函数提供迭代，并且在大多数编程语言中通常会被循环所取代。²

递归的真正威力在于函数调用自身不止一次。这使得递归函数能够测试多种替代方案。栈的内存对于此至关重要，因为真正发生的是一个调用被执行，并且在它完成后，栈会跟踪代码所在的位置，然后再次执行。像这样的函数可以转换为循环，但通常需要付出显著更大的努力。我们在第

> ¹递归是许多学生难以掌握的主题，但它非常强大，因此多次返回它是有价值的。
> ²值得注意的是，即使函数只调用自身一次，如果它在从栈中弹出时做一些工作，仍然可以从递归中受益。我们将在第 29 章中看到此类的示例。

15 章中看到，某些使用普通循环解决起来相当具有挑战性的问题，可以通过递归代码非常轻松地处理。

## 28.2 项目集成：迷宫

我们在第 15 章中考虑过的一个问题是完成迷宫。特别是，我们想要找到穿过迷宫的最短路径长度。所采用的递归方法也很好地适用于类似的问题，例如找到迷宫中最长路径或找到迷宫中路径的数量。迷宫是人类喜欢以图形方式表示的东西。因此，它们很适合放入我们的绘图程序中。

为此，我们将为迷宫创建一个可绘制对象。最终组合起来的代码如下所示。我们将在接下来的小节中逐步介绍它。

```
package scalabook.drawing

import java.awt.{Graphics2D,Color}
import java.awt.geom._
import scala.swing._
import scala.swing.event._
import actors.Actor

class DrawMaze(p:DrawTransform,m:Seq[Seq[Int]],
	private var ex:Int,
	private var ey:Int) extends DrawLeaf with Clickable {
val parent = p
private var maze = m.map(_.toArray).toArray
@transient private var propPanel:Component = null
@transient private var clickAction: (Int,Int)=>Unit = null

def draw(g:Graphics2D) {
	lastTransform = g.getTransform()

g.setPaint(Color.black)

g.drawRect(-1,-1,20*maze.length+1,20*maze(0).length+1)
	for(i <- 0 until maze.length; j <- 0 until maze(i).length) {
		g.setPaint(maze(i)(j) match {
			case -1 => Color.black
			case -2 => Color.yellow
			case 0 => Color.white
			case s => new Color(0, (255-s) max 0,0)
		})
		g.fillRect(i*20,j*20,20,20)
	}

g.setPaint(Color.green)

g.fillOval(ex*20,ey*20,20,20)
}

def propertiesPanel() : Component = {
if(propPanel == null) {
	import BorderPanel.Position._
	propPanel = new BorderPanel {
```

```
layout += new BorderPanel {
  layout += new GridPanel(2,1) {
    contents += new Label("Width")
    contents += new Label("Height")
  } -> West
  layout += new GridPanel(2,1) {
    contents += new TextField(maze.length.toString) {
      listenTo(this)
      reactions += { case e:EditDone =>
        val size = text.toInt
        if(size>5) resize(size,maze(0).length)
      }
    }
    contents += new TextField(maze(0).length.toString) {
      listenTo(this)
      reactions += { case e:EditDone =>
        val size = text.toInt
        if(size>5) resize(maze.length,size)
      }
    }
  } -> Center
val radioButtons = Seq(
  new RadioButton { action = Action("Draw Walls") {
    clickAction = (x,y) => {
      maze(x)(y) = if(maze(x)(y) == -1) 0 else -1
      drawing.refresh
    }
  } },
  new RadioButton { action = Action("Place Exit") {
    clickAction = (x,y) => {
      ex = x
      ey = y
      drawing.refresh
    }
  } },
  new RadioButton { action = Action("Shortest Path") {
    clickAction = (x,y) => Actor.actor {
      Dialog.showMessage(propPanel,"The shortest path has length " +
        shortestPath(x,y) + ".")
      drawing.refresh
    }
  } },
  new RadioButton { action = Action("Shortest Path Fast") {
    clickAction = (x,y) => Actor.actor {
      Dialog.showMessage(propPanel,"The shortest path has length " +
        shortestPathFast(x,y,0) + ".")
      drawing.refresh
    }
  } }
)
val group = new ButtonGroup(radioButtons:_*)
layout += new GridPanel(radioButtons.length+1,1) {
  radioButtons.foreach(rb => contents += rb)
  contents += Button("Clear Breadcrumbs") {
    for(i <- maze.indices; j <- maze(i).indices)
```

```
if(maze(i)(j)>0) maze(i)(j) = 0
    drawing.refresh
}
} -> South
} -> North
}
}
propPanel
}

override def toString() = "Maze"

def toXML : xml.Node = {
<drawMaze ex={ex.toString} ey={ey.toString}>
{maze.map(_.mkString(",")).mkString("\n")}
</drawMaze>
}

def react(evt:Event,cx:Double,cy:Double) {
    evt match {
        case mc:MouseClicked =>
            val x = cx.toInt/20
            val y = cy.toInt/20
            if(x>=0 && x<maze.length && y>=0 && y<maze(x).length && clickAction!=null) {
                clickAction(x,y)
            }
        case _ =>
    }
}

private def resize(w:Int,h:Int) {
    maze = Array.tabulate(w,h)((i,j) => {
        if(i<maze.length && j<maze(i).length) maze(i)(j) else 0
    })
    drawing.refresh
}

private def shortestPath(x:Int,y:Int):Int = {
    if(x==ex && y==ey) 0
    else if(x<0 || x>=maze.length || y<0 || y>=maze(x).length || maze(x)(y)<0) {
        100000000
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

private def shortestPathFast(x:Int,y:Int,steps:Int):Int = {
```

