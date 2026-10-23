are instances where those nested types need to be used by outside code, and there are some significant details to it that are worth mentioning.
When you put a **class** or **trait** inside of another class or trait, every instance of that type gets its own version. If you use standard "dot" notation to refer to the type, it needs to be on an object, not the **class**, and the type you get is specific to that object. You can also refer to the general type across all instances with the **class** name followed by a #. The following code demonstrates this.

```
class NestedClasses(x:Double,y:Double) {
  val root = new Plus(new Num(x),new Num(y))
  
  trait Node {
    def eval:Double
  }

  class Plus(left:Node,right:Node) extends Node {
    def eval = left.eval+right.eval
  }

  class Num(n:Double) extends Node {
    def eval = n
  }
}
```

```
object NestedClass {
  def main(args:Array[String]) {
    val a = new NestedClasses(4,5)
    val b = new NestedClasses(8.7,9.3)

    a.root match {
      case n:a.Num => println("A number")
      case n:a.Node => println("Not a number")
    }

    def evalNode(n:NestedClasses#Node) = n.eval
    def evalNodeA(n:a.Node) = n.eval
    def evalNodeB(n:b.Node) = n.eval

    println(evalNode(a.root))
    println(evalNodeA(a.root))
    println(evalNodeB(a.root)) // This is a type mismatch.
    println(evalNode(b.root))
    println(evalNodeA(b.root)) // This is a type mismatch.
    println(evalNodeB(b.root))
  }
}
```

The **class** at the top contains types for a little expression tree. This is greatly simplified for this example. In the companion **object** is a **main** method that makes two instances of the top class called **a** and **b**. A **match** on **a.root** shows how you can refer to types inside of the object **a**. If you try to put something in a case that is not one of the subtypes of **Node** inside of **a**, Scala gives you an error saying it can not be that type.
After the **match** are three **def** declarations of local functions. The first is written to take a general **Node** from inside of any instance of **NestedClasses**. The other two are specific