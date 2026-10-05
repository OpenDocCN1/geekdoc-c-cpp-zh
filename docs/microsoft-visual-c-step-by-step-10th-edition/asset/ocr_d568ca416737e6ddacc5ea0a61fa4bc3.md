```
var c = new Circle(42);               // Circle of radius 42
var s = new Square(55);                          // Square of side 55
var t = new Triangle(33);                        // Equilateral triangle of side 33

object o = s;
...
if (o is Circle myCircle)
{
    ... // o is a Circle, a reference is available in myCircle
}\else if (o is Square mySquare)
{
    ... // o is a Square, a reference is available in mySquare
}\else if (o is Triangle myTriangle)
{
    ... // o is a Triangle, a reference is available in myTriangle
}
```