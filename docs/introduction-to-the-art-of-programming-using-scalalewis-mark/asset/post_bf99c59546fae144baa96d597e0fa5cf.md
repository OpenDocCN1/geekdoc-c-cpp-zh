
```
scala> val jHat = new Vect3D(0,1,0)
jHat: Vect3D = Vect3D@24753433

scala> jHat.toString
res0: java.lang.String = Vect3D@24753433
```

Here we have a `class` for an immutable 3-D vector type that has no methods, just public members for three components. The second line creates an instance on this class which is followed by a notification that the variable `jHat` is of type `Vect3D` and has a given value. The value is a bit odd, having the name of the class followed by an @ symbol and a number. The third line shows a call to one of the methods inherited from `AnyRef`, the `toString` method. This call makes it clear where the text for the value came from. The `toString` method is actually defined on the type `Any` and, as such, is safe to call on any object in Scala. For that reason, it is used extensively to get a representation of objects. Here we see that it is called by the `REPL`.

Unfortunately, the default implementation of `toString` is not all that informative. For that reason, it is something that you often override. This code listing shows how we can do that.

```
scala> class Vect3D(val x:Double,val y:Double,val z:Double) {
|  override def toString():String = "Vect3D("+x+", "+y+", "+z+")"
|  }
defined class Vect3D

scala> val jHat = new Vect3D(0,1,0)
jHat: Vect3D = Vect3D(0.0, 1.0, 0.0)

scala> jHat.toString
res1: String = Vect3D(0.0, 1.0, 0.0)
```

The inclusion of `override` with a `def` that has the same signature as the inherited `toString` gives us a different implementation. You can see that this is now used in the `REPL` when the value of the object is printed as well as when the method is called directly.

This example shows an inherited method and how we can override it, but it does not actually demonstrate how to get inheritance in our code. It uses the inheritance that we get by default. If we want to inherit from something other than `AnyRef`, we use the `extends` keyword. This keyword is placed after the arguments to the class and before the open curly brace that starts the body of the class.

```
class Name(args) extends Supertype { body }
```

If you do not put in the `extends` keyword you get `extends AnyRef` by default.

To illustrate this, let us look at a different example that is a classic case of inheritance. We define a supertype called `Shape` that has some methods for things that we expect all shapes to be able to do.

```
class Shape {
    def area: Double = 0.0
    def circumference: Double = 0.0
    def draw(g: Graphics2D) {}
}
```

There are many different types of shape that we might want to have as subtypes of this class. Here are two possible examples.

```
class Rectangle(val width:Double, val height:Double) extends Shape {
	override def area:Double = width*height
	override def circumference:Double = 2.0*(width+height)
	override def draw(g:Graphics2D) {
		g.fill(new Rectangle2D.Double(0.0,0.0,width,height))
	}
}
```

```
class Circle(val radius:Double) extends Shape {
	override def area:Double = math.Pi*radius*radius
	override def circumference:Double = 2.0*math.Pi*radius
	override def draw(g:Graphics2D) {
		g.fill(new Ellipse2D.Double(0.0,0.0,2.0*radius,2.0*radius))
	}
}
```

Each of these classes takes some arguments and extends `Shape`, then overrides all of the methods of `Shape`.

We can now write code that takes an instance of `Shape` and pass it an instance of either `Rectangle` or `Circle` and it will work. The reason it will work is that inheritance guarantees us that any method we could call on an instance of `Shape` will be defined in the subtypes.

Consider the following function and two calls to it.

```
def areaCircumferenceRatio(s:Shape):Double = {
	s.area/s.circumference
}
```

```
val circleACR = areaCircumferenceRatio(new Circle(5))
val rectACR = areaCircumferenceRatio(new Rectangle(4,5))
```

This is the heart of polymorphism, one piece of code that can work on multiple types. This is universal polymorphism because at any point in the future we could create a new subtype of `Shape` and it would work with this code as well.

As a general rule, inheritance should be used to represent an “is-a” relationship. In the examples we have seen so far, it seems quite natural to say that an apple *is-a* fruit or that a rectangle *is-a* shape. If you can not say that, then inheritance probably is not the construct you want to use. Instead, you should use composition. This is where you put an instance of the type as a member of some class instead of inheriting from it. To get the functionality, you make calls on that member. Composition is used to model a “has-a” relationship. We will see many examples of this type of construction later in the book. It should be emphasized that you do not want to abuse inheritance. The code-reuse aspect might seem great, but the subtyping should only be used when it makes sense.

The opposite is also true. There are times when you will have an *is-a* relationship and subtyping makes sense, but not all of the methods you would get through code-reuse fit. In those situations you should also refrain from using inheritance. An example of this is a square. Clearly a square *is-a* shape. In addition, a square *is-a* rectangle. That relationship can be expressed with the following one-line class.

```
class Square(length:Double) extends Rectangle(length,length)
```

Here the class `Square` takes one argument for the `length` of an edge. It extends `Rectangle`, and passes that `length` as both the `height` and the `width` arguments. As this example shows, when the subtype takes arguments, they are passed in an argument list that follows the name of the supertype after extends.

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
