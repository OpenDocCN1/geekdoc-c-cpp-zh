
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

The **class** at the top contains types for a little expression tree. This is greatly simplified for this example. In the companion **object** is a **main** method that makes two instances of the top class called **a** and **b**. A **match** on **a.root** shows how you can refer to types inside of the object **a**. If you try to put something in a case that is not one of the subtypes of **Node** inside of **a**, Scala gives you an error saying it can not be that type. After the **match** are three **def** declarations of local functions. The first is written to take a general **Node** from inside of any instance of **NestedClasses**. The other two are specific to a and b. There are six calls where these three methods are invoked on the root objects of both a and b. Two of these result in errors as a.root is a mismatch with b.Node and b.root is a mismatch with a.Node.

### B.10 Self Types

There are times when you will create a trait which is intended to be mixed in with some other trait or class. Occasionally, inside of the mix-in trait, you will need to make reference to members of the type it is being mixed in to. Conceptually this makes sense as you know that this will always be safe. However, the compiler does not know that this will be safe. To get around this, you have to have a way to tell the compiler that the particular trait will only be used in situations where it is part of some other type. This can be done using a self type.

The syntax of a self type is as follows.

```
trait A {
  this: B =>
  ...
}
```

This tells Scala that any object that includes the trait A must include the type B above it in the resolution linearization. With this in place, the body of A can include references to members of B.

One common place that this is used in Scala is in something called the Cake pattern. Interested readers can use that term as a jumping-off point for searching for more information.

### B.11 Making Executable JAR Files

Scala programs compile to bytecode, not an actual executable. If you want to be able to give your program to someone else for them to run, you need to package it in a proper form. For code compiled to Java bytecode, that format is an executable JAR file. You can make these using the jar command from the Java Development Kit (JDK). Complete instructions can be found on the book’s website as the ideal set of steps is likely to change over time.

## Appendix C

### Glossary

- **Abstract** Lacking a definition. A val, var, def, or type declaration in a class or trait can be left without a definition, making it abstract. If a class contains any members that are abstract, then it must be declared to be abstract. Abstract types, whether class or trait, can not be instantiated. Only subtypes that have defined all the abstract members can be instantiated.

- **Abstraction** The concept of writing code so that certain parts of what happens are not concrete until the usage point. Functionality can be abstracted by passing in functions. Types can be abstracted through subtyping or type parameters.

- **Actor** An actor is an object that receives messages and acts on them. It should be able to process those messages in a manner that is independent of what thread is doing the work.

- **Affine Transform** This is a term from graphics that is defined as any transformation of the space where parallel lines are preserved. The basic affine transforms are translation, rotation, scale, and shear. Any combination of these is also an affine transform.

- **Argument** A value that is passed into a function or method.

- **Array** A basic collection of values that is a sequence represented by a single block of memory. Arrays have efficient direct access, but do not easily grow / shrink.

- **Class** A construct that works as the blueprint for objects.

- **CPU** The term Central Processing Unit is used to describe the primary computing element in a computer. This is where most of the work for the programs you are writing takes place.

- **Concrete** This is a term used to describe a type in which all members are defined and that can be instantiated. Non-abstract classes are concrete.

- **Concurrent** Concurrent execution is when two parts of a program are executing in a manner that appears to be simultaneous to the user and where the programmer has limited control over what is happening at any given time. A concurrent program does not have to be parallel. Concurrent programs include those where two threads of control swap between one another, but are never active at the same time.

- **Conditional** An expression of the Boolean type that is used to determine if code is executed.

- **Embarrassingly Parallel** This is a term used to describe a problem that breaks into problems that are completely independent. Such problems can be easily parallelized because the different pieces don't really have to communicate with one another.

## Bibliography

- [1] Gene M. Amdahl. Validity of the single processor approach to achieving large scale computing capabilities. In *Proceedings of the April 18-20, 1967, spring joint computer conference*, AFIPS ’67 (Spring), pages 483–485, New York, NY, USA, 1967. ACM.

- [2] Josh Barnes and Piet Hut. A hierarchical O(N log N) force-calculation algorithm. *Nature*, 324:446–449, December 1986.

- [3] Rudolf Bayer and Edward M. McCreight. Organization and maintenance of large ordered indices. *Acta Inf.*, 1:173–189, 1972.

- [4] Noam Chomsky. Three models for the description of language. *IRE Transactions on Information Theory*, 2:113–124, 1956. http://www.chomsky.info/articles/195609--.pdf – last visited 14th January 2009.

- [5] Martin Fowler. *Refactoring: Improving the Design of Existing Code*. Addison-Wesley, Boston, MA, USA, 1999.

- [6] Erich Gamma, Richard Helm, Ralph E. Johnson, and John Vlissides. *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley, Reading, MA, 1995.

- [7] Donald Knuth. *Structured Programming with Go To Statements*, pages 257–321. Yourdon Press, Upper Saddle River, NJ, USA, 1979.

- [8] Michael P. Marder. *Research Methods for Science*. Cambridge University Press, New York, NY, USA, 1st edition, 2011.

- [9] Martin Odersky, Lex Spoon, and Bill Venners. *Programming in Scala: A Comprehensive Step-by-Step Guide, 2nd Edition*. Artima Incorporation, USA, 2nd edition, 2011.

- [10] Robert Sedgewick. *Algorithms*. Addison-Wesley, Reading, Mass., 1983.

- [11] Herb Sutter. The free lunch is over: A fundamental turn toward concurrency in software. *Dr. Dobb's Journal*, 30(3):202–210, 2005.
