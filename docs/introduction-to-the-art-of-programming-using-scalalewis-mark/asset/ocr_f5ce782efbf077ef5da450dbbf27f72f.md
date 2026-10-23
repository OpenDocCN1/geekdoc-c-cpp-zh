shows, when the subtype takes arguments, they are passed in an argument list that follows the name of the supertype after extends.

Given what we have written for Rectangle, this implementation of Square is perfectly acceptable and calls to all the methods of an instance of Square will work as desired. That is only because our Rectangle type happens to be immutable. Consider this alternative implementation of Rectangle.

```
class Rectangle(var width:Double,var height:Double) extends Shape {
    override def area:Double = width*height
    override def circumference:Double = 2.0*(width+height)
    override def draw(g:Graphics2D) {
        g.fill(new Rectangle2D.Double(0.0,0.0,width,height))
    }
}
```

If you use this with the above definition of Square everything compiles fine and it might even seem to run fine. However, there is something truly broken with this implementation. To see this, consider the following code.

```
val square = new Square(5)
square.width=20 // WARNING: Works in code, but not what we want.
println(square.area)
```

This does something that should not be possible. It makes a “square” that is 20 by 5. That certainly does not seem to fit the normal definition of a square.

The problem here is that when we make the Rectangle type mutable we effectively introduced two new methods: def width_=(w:Double) and def height_=(h:Double). These methods are not suitable for the Square, but by virtue of inheritance, our Square type gets them.

It is tempting to try to fix this by explicitly overriding the methods that set the width and height fields as is done in this code.

```
class Square(length:Double) extends Rectangle(length,length) {
    override def width_=(w:Double) { // ERROR: Can’t override mutable variables.
        width = w
        height = w
    }
    override def height_=(h:Double) { // ERROR: Can’t override mutable variables.
        height = h
        width = h
    }
}
```

This does not compile because you are not allowed to override methods associated with variables. Even if it were allowed, or if we used different methods to access and set the variables, it would not be a good idea. To understand why, consider what a programmer is expecting to happen when a line like rect.width = 20 is executed. Clearly the programmer who writes this line is expecting it to change the value stored in the width field. If the height field changes as well, that would be unexpected behavior and might well violate assumptions made elsewhere in the function. That could lead to bugs that are remarkably hard to find because the code would work fine when used with an instance of Rectangle, and reasoning about the program will not likely help the programmer find the error.

So be careful with how you use inheritance. It should only be used when you want both the subtyping and the code-reuse.