# 12.1 Custom-Drawn Panels

To add your own graphics to a GUI, you need to create a Panel that draws what you want when it is displayed on the screen. The method for doing this is to make a new Panel and then change the way it is painted to the screen. The Panel type has a method in it called paint, which is passed a single argument of type java.awt.Graphics2D. We want to replace this method in our Panel. The act of changing what a method does is called overriding and we will do it with the override keyword. The syntax for this looks like the following.

```
val panel=new Panel {
  override def paint(g:Graphics2D) {
    // Draw to g
  }
}
```

If you try this in your code make sure that you import java.awt.Graphics2D so that it will know where to find that type.

This panel can then be added to a GUI in the same way that you would add any other panel to a GUI. For this chapter, we will simply make our custom-drawn Panel the entire contents of our Frame.

# 12.2 `java.awt.Graphics2D`

The main capabilities of the Java2D library are accessed through the Graphics2D class in the java.awt package. This class has a number of different methods that we can break into different groups. We list a few of them here. To see all of them you would need to go to the Java API.

+   - Draw/Fill Methods
+     - `draw(s:Shape)`
+     - `drawLine(x1:Int, y1:Int, x2:Int, y2:Int)`
+     - `drawRect(x:Int, y:Int, width:Int, height:Int)`
+     - `drawImage(img:RenderedImage, x:Int, y:Int, obs:ImageObserver)`
+     - `drawImage(img:RenderedImage, x:Int, y:Int, width:Int, height:Int, obs:ImageObserver)`
+     - `drawRenderedImage(img:RenderedImage, trans:AffineTransform)`
+     - `drawString(str:String, x:Int, y:Int)`
+     - `fill(s:Shape)`
+     - `fillRect(x:Int, y:Int, width:Int, height:Int)`

+   - Set Methods
+     - `setPaint(paint:Paint)`