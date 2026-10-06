# LISTING 2-45 Defining an interface with properties

```
Interface definition with interface...end
type I2DLocation = interface
abstract member X : float with get, set
abstract member Y : float with get, set

Lightweight interface definition
type I2DLocation =
abstract member X : float with get, set
abstract member Y : float with get, set
```

> Note Unlike C#, an F# interface does not support a partial keyword. Therefore, an interface has to be in one file.

F# requires interfaces to be explicitly implemented; as a result, the code needs some extra work. See Listing 2-46. Adding an interface seems to add much value to this code; however, the interface can make code easy to expand and testing frameworks such as Fakes in Visual Studio requires an interface.

# LISTING 2-46 Implementing an interface

```
// 2D location interface
type I2DLocation =
abstract member X : float with get, set
abstract member Y : float with get, set

// define a Point2D class with a parameterized primary constructor
type Point2D(XValue:double, yValue:double) as =
// -other Point2D members as property X and Y
  // define field x
let mutable x = xValue

// define an X property
member this.X with get() = x
  and set(v) = x <- v

// define a Y property using an auto-implemented property
member val Y = yValue with get, set
```