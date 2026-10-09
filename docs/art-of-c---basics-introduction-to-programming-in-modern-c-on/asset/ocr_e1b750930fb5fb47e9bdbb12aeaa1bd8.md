```
area-calculation/mi2/Perimeter.cs

```
csharp
namespace MI2;

/// <summary>Perimeter interface. Used to demonstrate the inheritance.</summary>
public interface IPerimeter {
    /// <summary>
    /// Returns the perimeter.
    /// Has a default implementation.
    /// </summary>
    float Size() => 1.0f;
}
```
```

```
area-calculation/mi2/Shapes.cs

```
csharp
namespace MI2;

/// <summary>ShapeA illustrates multiple interface inheritance.</summary>
public class ShapeA : IArea, IPerimeter { }

/// <summary>ShapeB illustrates multiple interface inheritance.</summary>
public class ShapeB : IArea, IPerimeter {
    /// <summary>An implicit/normal implementation for IArea.Size() and IPerimeter.Size().</summary>
    public float Size() => 210.0f;
}

/// <summary>
/// ShapeC illustrates multiple interface inheritance.
/// It includes explicit implementations of IArea.Size() and IPerimeter.Size().
/// </summary>
public class ShapeC : IArea, IPerimeter {
    /// <summary>An explicit implementation of IArea.Size().</summary>
    float IArea.Size() => 220.0f;

    /// <summary>An explicit implementation of
```
```