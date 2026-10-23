```
}
pq.dequeue()
}
```

This code will run the simulation, but it does not really do anything useful for us because it does not do much for us. It returns the amount of time it took to reach the stop population. We can produce something that is a bit more functional by putting this inside of a class that is Drawable and having it plot the population as a function of time. Code that does that is shown here.

```
package scalabook.drawing

import swing._
import event._
import java.awt.{Color}
import java.awt.geom._
import java.awt.image.BufferedImage
import collection.mutable
import scalabook.ad t._

class DrawCellSim(p:DrawTransform,
    private var width:Int,
    private var height:Int,
    private var maximumPopulation:Int,
    private var minSplitTime:Double,
    private var maxSplitTime:Double,
    private var numSims:Int) extends DrawLeaf {
val parent = p
@transient private var propPanel:Component = null
@transient private var img:BufferedImage = null

private def runSimulation(splits:mutable.Buffer[Double]) {
val pq = new SortedListPriorityQueue[Double]((a,b) => b.compareTo(a))
pq.enqueue(minSplitTime+math.random*(maxSplitTime-minSplitTime))
while(splits.length+1<maximumPopulation) {
val time = pq.dequeue()
splits += time
pq.enqueue(time+minSplitTime+math.random*(maxSplitTime-minSplitTime))
pq.enqueue(time+minSplitTime+math.random*(maxSplitTime-minSplitTime))
}
}

private def redoImage {
if(img==null || width!=img.getWidth || height!=img.getHeight) {
img = new BufferedImage(width,height,BufferedImage.TYPE_INT_ARGB)
}
for(i <- 0 until width; j <- 0 until height) img.setRGB(i,j,0) // transparent
val data = mutable.Buffer[Double]()
var maxTime = -1.0
val g = img.createGraphics()
g.setPaint(Color.black)
for(i <- 0 until numSims) {
runSimulation(data)
if(maxTime < 0) {
maxTime = data.last*1.2
```