```
using System;

namespace Polygons.Library
{
    public class Octagon : Object, IRegularPolygon
    {
        public int NumberOfSides { get; set; }
        public int SideLength { get; set; }

        public Octagon(int length)
        {
            NumberOfSides = 8;
            SideLength = length;
        }

        public double GetPerimeter()
        {
            return NumberOfSides * SideLength;
        }

        public double GetArea()
        {
            return SideLength * SideLength * (2 + 2 * Math.Sqrt(2));
        }
    }
```

That means, in our Octagon class, we must provide all of these implementations. If I comment out to GetPerimeter method and try to build the application, we will get a build error. And if we look at the error, it says, 'Octagon' does not implement interface member GetPerimeter(). So just like with abstract members in an abstract class, we get a compiler error if we do not provide the implementations that are needed by the interface.

![](bbox=[0.12, 0.67, 0.91, 0.79])

This is just a quick overview so that we can see how concrete classes, abstract classes, and interfaces work. There are several