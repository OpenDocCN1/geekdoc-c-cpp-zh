# *23.2. Code Review - Area and Perimeter Calculator for Multiple Shapes*

```
```
size1Ca = 110
size1Cp = 120
```
```

As before, once the methods from both interfaces are explicitly implemented, any method in a concrete type that has the same name and signature provides no polymorphic behavior.

*area-calculation/mi1/ Shapes.cs (lines 26-35)*

```
```
26  public class ShapeD : IArea, IPerimeter {
27      /// <summary>It has nothing to do with IArea.Size() or
28      IPerimeter.Size().</summary>
28      public float Size() => 130.0f;
29
30      /// <summary>An explicit implementation of IArea.Size().</summary>
31      float IArea.Size() => 140.0f;
32
33      /// <summary>An explicit implementation of
34      IPerimeter.Size().</summary>
34      float IPerimeter.Size() => 150.0f;
35  }
```
```

```
```
ShapeD shape1D = new();
var size1D = shape1D.Size();
Console.WriteLine($"size1D = {size1D}");
```
```

The `WriteLine()` method prints out this:

```
```
size1D = 130
```
```

For this type, `Shape6`, only the `IArea.Size()` method is explicitly implemented. The class includes the normal/implicit implementation of `Size()`.