existing Shape. You can add to the path with methods like moveTo, lineTo, quadTo, or curveTo.

+   - Point2D – A point in 2-D space you make with new Point2D.Double(x:Double, y:Double).

+   - QuadCurve2D – Makes a curve described by quadratic polynomials in x, y, and z. You can create this by calling new QuadCurve2D.Double(x1:Double, y1:Double, ctrlx1:Double, ctrly1:Double, x2:Double, y2:Double).

+   - Rectangle2D – Represents a rectangle. You make one with new Rectangle2D.Double (x:Double, y:Double, w:Double, h:Double) where (x, y) specifies the top-left corner.

+   - RoundRectangle2D – This is a rectangle with rounded corners. You make one with new RoundRectangle2D.Double(x:Double, y:Double, w:Double, h:Double, arcw:Double, arch:Double).

Most of these are fairly straightforward. The exceptions are the Area and Path2D types. Interested readers are directed to the Java API for more details on these and how to use them. For the types that end with 2D, they can be created with either .Float or .Double. We have used .Double in the list above because it makes things simpler.

We can demonstrate quite a few of these in just a few lines of code. In the body of the paint method put the following lines instead of the call to g.fillRect.

```
g.fill(new Rectangle2D.Double(20,20,50,80))
g.draw(new Ellipse2D.Double(0,200,500,300))
g.fill(new Arc2D.Double(250,0,250,250,45,270,Arc2D.PIE))
g.draw(new QuadCurve2D.Double(0,500,250,0,500,500))
```

When you run this code you will get a window like that shown in figure 12.2.

# 12.2.2 Settings

Drawing shapes provides a significant amount of power and flexibility. However, there are some clear limitations that are visible in figure 12.2. The most significant of these is the fact that everything is appearing in the same color on the default light gray background. Another limitation is that the shapes are being drawn with thin, single pixels lines. In order to get around these limitations, we need to be able to tell the Graphics2D object to draw things in different ways. This is done by changing various settings.

# 12.2.2.1 Paint

The most significant setting in most application is the Paint setting. Prior to Java2D, this was a simple color setting. However, when you draw something there are a lot more options than just having a single, solid color. The Paint type is a way of representing these different options, just like the Shape type is a way of generally representing the different types of things that you might want to draw. The main options you can use for a Paint are listed here.

+   - Color – Solid colors are still helpful and the Color type represents these. A lot of standard colors are predefined for you. So you can use Color.white, Color.black, Color.red, Color.green, Color.blue, etc. You can also “mix” your own colors by combining different amounts of red, green, and blue with either