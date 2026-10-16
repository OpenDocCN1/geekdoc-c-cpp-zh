```
{
    // members
}
```

If a class (or a struct) also derives from interfaces, the list of base class and interfaces is separated by commas:

```
public class MyDerivedClass: MyBaseClass, IInterface1,
IInterface2
{
    // members
}
```

> NOTE In case a class and interfaces are used to derive from, the class always must come first—before interfaces.

For a struct, the syntax is as follows (it can only use interface inheritance):

```
public struct MyDerivedStruct: IInterface1, IInterface2
{
    // members
}
```

If you do not specify a base class in a class definition, the C# compiler assumes that System.Object is the base class. Hence, deriving from the Object class (or using the object keyword) is the same as not defining a base class.

```
class MyClass // implicitly derives from System.Object
{
    // members
}
```

Let’s get into an example to define a base class Shape. Something that’s common with shapes—no matter whether they are rectangles or ellipses—is that they have position and size. For position and size, corresponding classes are defined that are contained within the Shape class. The Shape class defines read-only properties Position and Shape that are initialized using auto property initializers (code file VirtualMethods/Shape.cs):

```
public class Position
{
    public int X { get; set; }
    public int Y { get; set; }
}
```

```
public class Size
{
    public int Width { get; set; }
    public int Height { get; set; }
}
```

```
public class Shape
{
    public Position Position { get; } = new Position();
    public Size Size { get; } = new Size();
```