```
```csharp
}
```
```

# ## Namespace SI2

*area-calculation/si2/Area.cs*

```
```csharp
namespace SI2;

/// <summary>Area interface. Used to demonstrate an interface inheritance.</summary>
public interface IArea {
    /// <summary>
    /// Returns the area.
    /// Has a default implementation.
    /// </summary>
    float Size() => 30.0f;
}
```
```

*area-calculation/si2/Shapes.cs*

```
```csharp
namespace SI2;

/// <summary>ShapeA illustrates a single interface inheritance.</summary>
public class ShapeA : IArea { }

/// <summary>ShapeB illustrates a single interface inheritance.</summary>
public class ShapeB : IArea {
    /// <summary>An implicit/normal implementation of IArea.Size().</summary>
    public float Size() => 35.0f;
}

/// <summary>ShapeC illustrates a single interface inheritance.</summary>
public class ShapeC : IArea {
    /// <summary>An explicit implementation of IArea.Size().</summary>
    float IArea.Size() => 40.0f;
}
```
```