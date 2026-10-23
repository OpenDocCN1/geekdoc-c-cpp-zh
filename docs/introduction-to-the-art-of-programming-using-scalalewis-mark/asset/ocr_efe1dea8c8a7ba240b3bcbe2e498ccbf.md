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