
If the inherit declaration appears in the primary constructor, it is called implicit class construction. The code in Listing 2-31 is always a good practice to use an implicit constructor and provide an implicit constructor (or overloads). However, the code in Listing 2-30 does not include a primary constructor and instead specifies the desired base class constructor. We refer to this as explicit class construction. It is a recommended way to use implicit constructors.

LISTING 2-31 Example of a keyword base

```
type Particle()
  inherit Point2D()
  member val Mass = 0. with get, set
  override this this.ToString() =
    sprintf("Particle_%s with Mass=%f", (base.ToString()) this.Mass)
```

## Using Abstract and Sealed Classes

The class hierarchies are formed from inheritance a tree structure. Sometimes the root of the tree can be an abstract class. C# uses an abstract keyword to define an abstract class. Unlike C#, F requires the AbstractClass attribute to define an abstract class when no default implementations are provided. See the code in Listing 2-32.

LISTING 2-32 Defining an abstract class

```
[AbstractClass]
type MyAbstractClass()
  member this.F() = 1

  // define an abstract member function
abstract member FunctionNotImplemented : unit -> int
```

> Tip If you cannot remember how to write the function definition for member method, you can also use FSI. For example, if you want to define a function with an int parameter as input and an int as output, you can let f (int) = 1 in FSI and the val : int -> int will display the function definition. In C#, a method can be overridden if it is a virtual method. F does not have a virtual keyword to define a virtual method. Instead, F uses the abstract keyword and the default keyword to define a virtual method. In Listing 2-33, the GetDistance method is defined as a virtual method, and then a default implementation of method is defined.

```
// define a Point2D class with primary constructor
type Point2D(xValue:double, yValue:double) =
  // define field
  let mutable x = xValue

  // define a static field named count
  static let mutable count = 0

  // perform a do binding to increase the count
  do
    count <- count + 1

  // additional constructor
  new() = Point2D(0.,0.)

  // print out message
  member this.Print() = printf "In class Point2D"

  // define an X property
  member this.X with get() = x
    and set(v) = x <- v

  // define a Y property using an auto-implemented property
  member val Y = yValue with get, set

  // define a virtual function to get the distance from the current point
  abstract GetDistance : point:Point2D -> double
  default GetDistance(point) =
    let xDif = point.X
    let yDif = point.Y
    let distance = sqrt (xDif*xDif + yDif)

  // define a static method to return a Point2D from (x,y) tuple
  static member FromXY(x, y) = Point2D(x,y)

  override this.ToString() = sprintf "Point2D(%f, %f)" this.X this.Y
```

nonvirtual method is not a good practice, although it a necessary approach under certain circumstances. F# does not support the new keyword like C# but it still allows users to do it. If you override a nonvirtual method, there will be a warning. Listing 2-34 shows a sample.

LISTING 2-34 Overriding a nonvirtual method

```csharp
// C# code using the new keyword
public class MyClass : List<int>
{
    public new void Add(int n)
    {
        base.Add(n);
        // <additional operations>
    }
}
```

```fsharp
// F# code overriding a nonvirtual method
type MyList() =
    inherit System.Collections.Generic.List<int>()

    // add element
    member this.Add(n) = // yield warning
        base.Add(n)
        // <additional operations>
```

> Note You can use [<#warn>] to disable the warning.

I'm going to change direction slightly and introduce attributes. An attribute in F# is used in a way that is very similar to C#. Listing 2-35 shows how to decorate the Point2D class with DebugDisplayAttribute.

LISTING 2-35 Adding the DebugDisplay attribute to a class

```fsharp
// define a Point2D class with a primary constructor
[System.Diagnostics.DebugDisplay("{X}, {Y}")]
type Point2D(xValue:double, yValue:double) =
  // define field
  let mutable x = xValue

  // define a static field named count
  static let mutable count = 0

  // perform a do binding to increase the count
  do
    count <- count + 1

  // additional constructor
  new() = Point2D(0.,0.)

  // print out message
  member this.Print() = printf "In class Point2D"

  // define an X property
  member this.X with get() = x
    and set(v) = x <- v

  // define a Y property using an auto-implemented property
  member val Y = yValue with get, set
```

The AbstractClass attribute is used to define an abstract class, and the Sealed attribute is for defining a sealed class. See Listing 2-36.

LISTING 2-36 A *Sealed* class definition

```fsharp
[<Sealed>]
type MySealedClass()
    member this.F() = 1
```

## Creating an Instance

F# has the **new** keyword to create an object. The **new** keyword is optional when creating a new object unless the class implements the *IDisposable* interface. If the *new* keyword is not used, there will be a compile-time warning indicating the *new* keyword and the class will implement the *IDisposable* interface. See Listing 2-37.

LISTING 2-37 Using the *new* keyword when creating an object that implements *IDisposable*

```csharp
// create object with the new keyword for a class implementing the IDisposable interface
let myObj = System.Data.SqlClient.SqlConnection()

// Warning: It is recommended that objects that support the
// IDisposable interface are created using 'using()'
// rather than 'new Type()' to indicate that resources may
// be owned by the generated value
let myObj2 = System.Data.SqlClient.SqlConnection()
```

> Note When the class implements the *IDisposable* interface, **use can replace let** in a nonmodule context. Keep in mind that *use* in C# is different from F#.
