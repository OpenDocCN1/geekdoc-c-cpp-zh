```
```csharp
IArea shape2Da = new ShapeD();
var size2Da = shape2Da.Size();
Console.WriteLine($"size2Da = {size2Da}");
```

```
```
```

# ## Namespace MI1

*area-calculation/mi1/Area.cs*

```
```csharp
namespace MI1;

/// <summary>Area interface. Used to demonstrate the inheritance.</summary>
public interface IArea {
    /// <summary>
    /// Returns the area.
    /// This method needs to be implemented in the concrete types.
    /// </summary>
    float Size();
}
```
```

*area-calculation/mi1/Perimeter.cs*

```
```csharp
namespace MI1;

/// <summary>Perimeter interface. Used to demonstrate the inheritance.</summary>
public interface IPerimeter {
    /// <summary>
    /// Returns the perimeter.
    /// This method needs to be implemented in the concrete types.
    /// </summary>
    float Size();
}
```
```