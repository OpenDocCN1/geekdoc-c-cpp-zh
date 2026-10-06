# LISTING 2-61 Extension method for a C# project

```
[<System.Runtime.CompilerServices.Extension>
module MyExtensionMethods =

// extension methods can be invoked from a C# project
[System.Runtime.CompilerServices.Extension]
let ToBinaryString i = sprintf("0%X")

// Way to extend a type
type System.Int32 with
    member this.ToBinaryString() = ToBinaryString this
```

> Note if the code will be invoked by a C# project, always consider putting the code inside a namespace.

# Using Operator Overloading

Operator overloading is used to add new meaning to an operator. The operator that needs to be overloaded in parentheses. If the operator is a unary operator, you have to add a tilde (~) as a prefix. Listing 2-62 shows how to add an operator overload in the Point2D class.

# LISTING 2-62 Operator overloading

```
Defining an operator in a class
// define a 2D location interface
type I2DLocation =
    abstract member X : float with, set
abstract member Y : float with, set

// define a IPoint2D interface
type IPoint2D =
inherit I2DLocation
abstract member GetDistance<'T> when 'T : IPoint2D -> float

// define a Point2D class with a parameterized primary constructor
and Point2D(xValue:double, yValue:double) =
// define field x
let mutable x = xValue

// define a static field named count
static let mutable count = 0

// perform a do binding to increase the count
dn count <- count + 1
```