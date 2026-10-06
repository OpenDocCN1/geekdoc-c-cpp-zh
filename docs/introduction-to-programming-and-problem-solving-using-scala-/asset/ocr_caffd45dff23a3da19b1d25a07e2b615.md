# Introduction to Programming and Problem-Solving Using Scala

+   - translate(x: Double, y: Double): Unit Applies a translation to the current transform.

With the exception of clip, these methods should be fairly straightforward as they refer to the types of settings that have been covered earlier for non-Canvas based drawing.

There are two other methods to settings on the GraphicsContext that allow you to store and recover settings. The save(): Unit method will call all the current settings and store them in a structure called a stack. You can later call restore(): Unit to bring back earlier settings. If you save() multiple times without calling restore(), they stack up and the last restore will pull off the most recently saved values. Another call will pull the values before and so on.

# 12.6.2 Basic Fills and Strokes

One way of drawing things to a GraphicsContext is to draw shapes directly. This can be done by filling the shape or just by drawing the outline as a stroke. The following methods provide this functionality.

+   - fillArc(x: Double, y: Double, w: Double, h: Double, startAngle: Double, arcExtent: Double, closure: ArcType): Unit
- fillOval(x: Double, y: Double, w: Double, h: Double): Unit
- fillPolygon(points: Seq[[Double,Double])): Unit
- fillPolygon(xPoints: Array[Double], yPoints: Array[Double], nPoints: Int): Unit
- fillRect(x: Double, y: Double, w: Double, h: Double): Unit
- roundRect(x: Double, y: Double, w: Double, h: Double, arcWidth: Double, arcHeight: Double): Unit
- fillText(text: String, x: Double, y: Double, maxWidth: Double): Unit
- fillText(text: String, x: Double, y: Double): Unit
- strokeArc(x: Double, y: Double, w: Double, h: Double, startAngle: Double, arcExtent: Double, closure: ArcType): Unit
- strokeLine(x1: Double, y1: Double, x2: Double, y2: Double): Unit
- strokeOval(x: Double, y: Double, w: Double, h: Double): Unit
- strokePolygon(points: Seq[[Double,Double])): Unit
- strokePolygon(xPoints: Array[Double], yPoints: Array[Double], nPoints: Int): Unit
- strokePolyline(points: Seq[[Double,Double]]): Unit
- strokePolyline(xPoints: Array[Double], yPoints: Array[Double], nPoints: Int): Unit
- stroke(x: Double, y: Double, w: Double, h: Double): Unit
- strokeRoundRect(x: Double, y: Double, w: Double, h: Double, arcWidth: Double, arcHeight: Double): Unit