```
Console.WriteLine($"size1Ga = {size1Ga}");

IPerimeter shape1Gp = new ShapeG();
var size1Gp = shape1Gp.Size();
Console.WriteLine($"size1Gp = {size1Gp}");

ShapeH shape1H = new();
var size1H = shape1H.Size();
Console.WriteLine($"size1H = {size1H}");

IArea shape1Ha = new ShapeH();
var size1Ha = shape1Ha.Size();
Console.WriteLine($"size1Ha = {size1Ha}");

IPerimeter shape1Hp = new ShapeH();
var size1Hp = shape1Hp.Size();
Console.WriteLine($"size1Hp = {size1Hp}");
    }
}
```

# # Namespace MI2

*area-calculation/mi2/Area.cs*

```
namespace MI2;

/// <summary>Area interface. Used to demonstrate the
/// inheritance.</summary>
public interface IArea {
    /// <summary>
    /// Returns the area.
    /// Has a default implementation.
    /// </summary>
    float Size() => 20.0f;
}
```