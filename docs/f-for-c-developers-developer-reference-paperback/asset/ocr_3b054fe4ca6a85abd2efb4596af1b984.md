# LISTING 2-17 Using a parameterized constructor as the primary constructor

```
// define a Point2D class with a parameterized primary constructor
type Point2D(xValue:double, yValue:double) =
    // define field x
let mutable x = xValue

// define an X property
member this.X with get() = x
and set(v) = x <- v

// define a Y property using an auto-implemented property
val Y = yValue with get, set

// define a function to get the distance from the current point
member this.GetDistance(point:Point2D) =
    let xDif = this.X - point.X
let yDif = this.Y - point.Y
    let distance = sqrt(xDif**2 + yDif**2)
    distance

// define a static method to return a Point2D from (x,y) tuple
static FromXY(x, y) =
    Point2D(x,y)
```

> Note The member function cannot be invoked in the constructor code.

In some cases, you need a different way to initialize an object. C# allows multiple constructors. The sample in Listing 2-18 shows how to define an additional constructor in F#.

# LISTING 2-18 An additional constructor

```
// define a Point2D class with a parameterized primary constructor
type Point2D(xValue:double, yValue:double) =
    // define field x
let mutable x = xValue

    //additional constructor
new() = Point2D(0.,0.)

    // define an X property
member this.X with get() = x
    and set(v) = x <- v

    // define a Y property using an auto-implemented property
val Y = yValue with get, set

    // define a function to get the distance from the current point
member this.GetDistance(point:Point2D) =
```