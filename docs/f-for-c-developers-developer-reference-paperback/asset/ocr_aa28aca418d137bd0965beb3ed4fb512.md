The C# class has its ToString method overridden. To do this in F#, you can use the override keyword. Listing 2-27 shows how to override the ToString function in F#. Inside the ToString implementation, you use sprintf as an alternative to String.Format. The sprintf function can be viewed as a strongly typed version of String.Format. You pretty have the conversion work done, but let's continue using Point2D as a sample to explore OOP concepts in F.

# **Listing 2-27** Function override

```
// define a Point2D class with a parameterized primary constructor
type Point2D(xValue:double, yValue:double) as this=
    // define field x
    let mutable x = xValue

    // define a static field named count
    static let count = 0

    // perform a do binding to increase the count
    do
        count <- count + 1
        this.Y <- .

    //additional constructor
    new() = Point2D(0.,0.)

    // define an X property
    member this.X with get() = x
        and set(v) = x <- v

    // define a Y property using an auto-implemented property
    member val Y = yValue with get, set

    // define a function to get the distance from the current point
    member this.GetDistance(point:Point2D) =
        let xDif = this.X - point.X
        let yDif = this.Y - point.Y
        let distance = sqrt (xDif**2 + yDif**2)
        distance

    // define a static method to return a Point2D from (x,y) tuple
    static member FromXY(x,y) =
        Point2D(x,y)

    // override the ToString function
    override this.ToString() =
        String.Format("Point2D({0}, {1})", this.X, this.Y)
        sprintf "Point2D(%f, %f)" this.X this.Y
```