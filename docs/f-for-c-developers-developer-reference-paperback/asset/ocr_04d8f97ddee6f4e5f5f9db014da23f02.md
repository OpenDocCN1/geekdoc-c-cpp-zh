```
//additional constructor
new() = Point2D(0.,0.)

// define an X property
member this.X with get() = x
and set(v) = x <- v

// define a Y property using an auto-implemented property
member val Y = yValue with get, set

// define a function to get the distance from the current point
abstract GetDistance<'T when : IPoint2D > : point.'T' - double
default this.GetDistance<'T when : IPoint2D>(point:T) =
let xDif = this.X - point.X
let yDif = this.Y - point.Y
let distance = sqrt(xDif*xDif + yDif*yDif)

// define a static method to return a Point2D from (x,y)
static member FromXY(x, y) =
    Point2D(x,y)

// overload + operator
static member (+)(point: Point2D, offset:double) =
    Point2D(point.X + offset, point.Y + offset)

// unary operator
static member (--)(point: Point2D) =
    Point2D(-point.X, -point.Y)

interface I2DLocation
    member this.X with get() = this.X and set(v) = this.X <- v
    member this.Y with get() = this.Y and set(v) = this.Y <- v
interface IPoint2D
    member this.GetDistance<'T when 'T : IPoint2D > (p) = this.GetDistance(p)'
```

Using the operators
let c =Point2D(2., 2.)
let d = -c
let originalPoint = d + 2. // the result is original point (0,0)

The F# compiler compiles an operator, it generates a method that has a compiler-generated name. If you use reflection, or Microsoft IntelliSense, the generated method name is what you will see. Table 2-3 shows the standard operators and corresponding names.