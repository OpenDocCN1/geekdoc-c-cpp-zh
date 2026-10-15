```
```csharp
namespace Polygons.Library
{
    public class ConcreteRegularPolygon
    {
        public int NumberOfSides { get; set; }
        public int SideLength { get; set; }

        public ConcreteRegularPolygon(int sides, int length)
        {
            NumberOfSides = sides;
            SideLength = length;
        }

        public double GetPerimeter()
        {
            return NumberOfSides * SideLength;
        }

        public virtual double GetArea()
        {
            throw new NotImplementedException();
        }
    }
}
```
```

Our ConcreteRegularPolygon will act as a base class so that we can create specific polygons. This class has two properties, an integer to represent the NumberOfSides and an integer to represent the SideLength. These properties are what are known as automatic properties. This is a shortened syntax. To show this, let's create a full property. So we'll comment out the SideLength, and I'll use a code snippet in Visual Studio. So I'll type propfull, which is a code snippet for a property with a backing field, and hit Tab twice, and it will fill in a template for us.