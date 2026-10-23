As you can see from the error message, this does not work because the map method is expecting an argument that is a function of the form (Int) => ?. That is something that takes an Int as a single argument and outputs anything. We can make a type that fits this, but we need to use inheritance to do so.

```
scala> class F extends ((Int)=>Int) { def apply(i:Int) = 2*i }
defined class F
```

```
scala> val f=new F
f: F = <function1>
```

```
scala> List(1,2,3) map f
res1: List[Int] = List(2, 4, 6)
```

The only difference between type F and type G is that F explicitly extends (Int)=>Int. The first impact of this can be seen in the creation of the object f where we get an different version of the toString method.

# 19.3 Inheritance in the Project

You now know enough about inheritance that we can see how to use it in our project code. The most obvious place inheritance will appear is the different Drawable types that we will want to include.

# 19.3.1 Drawables

Each different type of thing that we might want to draw will be a different subtype of Drawable. At the very least, we can start with some basic shapes like rectangles and ellipses. We will also include another type that will group together multiple elements in the drawing and represent a transformation. Back in chapter 12 we learned about the java.awt.geom.AffineTransform type and used it with our drawings on a Graphics2D object. We want a Drawable element that can include that type of functionality in our drawings.

There is another aspect to the Drawable type that relates to how it is included in the Graphical User Interface (GUI). We want the different things that are being drawn to appear in the JTree element in the GUI. The javax.swing.JTree displays objects that have to be subtypes of the javax.swing.tree.TreeNode type.⁴ To make this happen, we can just have the Drawable type extend TreeNode.

Given the description of Shape earlier in this chapter, you have probably also realized that the draw method in Drawable should be abstract because there really is not a good default implementation of how to draw. We will take the additional step of making Drawable into a trait. The resulting code looks like this.

```
/**
```

⁴The TreeNode type is what is called an interface in Java. This is like a Scala trait where all methods are left abstract and no member data is defined.