```
def area:Double = 0.0
def circumference:Double = 0.0
def draw(g:Graphics2D) {}
}
```

With color set to be protected, the previous code for Rectangle and Circle will work.

The protected visibility is something that is not used very often. If a value really needs to be hidden it should be private. Making it protected is a signal to programmers that it is needed by subclasses, but that they need to know what they are doing if they are going to use or alter it.

# 19.2.3 Calling Methods on the Supertype

Sometimes when you override a method in a subtype, you still want the code from the supertype to be run. There are actually situations where you are expected to call the method in the supertype before doing additional work. To support this type of behavior, you can use the super keyword like an object that references the part of the current object that is the supertype.

This can be used to solve the coloring problem in a way that keeps the color private. Consider the following implementation of Shape.

```
class Shape(private var color:Color) {
  def area:Double = 0.0
  def circumference:Double = 0.0
  def draw(g:Graphics2D) {
    g.setPaint(color)
  }
}
```

This has a private member color so it is not visible to the subtypes and is well encapsulated so we do not have to worry about other code changing it. Unlike the last version with a private color, this one has some code in the draw method that sets the paint on the Graphics2D object to color. Having this in the code allows us to do the following in Rectangle.

```
class Rectangle(val width:Double,val height:Double,c:Color) extends Shape(c) {
  override def area:Double = width*height
  override def circumference:Double = 2.0*(width+height)
  override def draw(g:Graphics2D) {
    super.draw(g)
    g.fill(new Rectangle2D.Double(0.0,0.0,width,height))
  }
}
```

By making a call to draw on super, this version can set the color when draw is called without actually having access to the value in the supertype. The same type of thing could be done in Circle.

One advantage to this approach is that as long as all the subtypes of Shape follow the pattern of making a call to super.draw before they draw their own geometry, it would be possible to add other settings such as different strokes or transformations to the Shape type without altering the draw methods in the subtypes. In large libraries, this same behavior can be problematic as it forces the supertype to stick with a certain behavior because all the subtypes, including those written by other authors, are expecting it to be maintained.