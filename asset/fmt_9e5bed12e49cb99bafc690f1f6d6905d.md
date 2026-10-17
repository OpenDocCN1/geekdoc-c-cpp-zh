
## `salary-calculation/Organizations.cs`

```csharp
namespace Corporation;

public abstract class Organization : List<Employee> {

    public string Name { get; }

    protected Organization(string name) => Name = name;

    public decimal TotalExpense {

        get {

            var sum = 0m;

            ForEach(s => sum += s.Salary);

            return sum;

        }

    }

}
```

### 面积与周长

### `area-calculation/area-calculation.csproj`

```xml
<Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>net6.0</TargetFramework>
        <ImplicitUsings>enable</ImplicitUsings>
        <Nullable>enable</Nullable>
        <GenerateDocumentationFile>true</GenerateDocumentationFile>
    </PropertyGroup>
</Project>
```

### `area-calculation/Program.cs`

```csharp
// Test drivers
SI1.Driver.M();
SI2.Driver.M();
MI1.Driver.M();
MI2.Driver.M();
```

### 命名空间 SI1

`*area-calculation/si1/Area.cs*`

```csharp
namespace SI1;

/// <summary>Area interface. Used to demonstrate an interface
/// inheritance.</summary>
public interface IArea {
    /// <summary>
    /// Returns the area.
    /// This method needs to be implemented in the concrete types.
    /// </summary>
    float Size();
}
```

`*area-calculation/si1/Shapes.cs*`

```csharp
namespace SI1;

/// <summary>ShapeB illustrates a single interface inheritance.</summary>
public class ShapeB : IArea {
    /// <summary>Implicit/normal implementation of
    /// IArea.Size().</summary>
    public float Size() {
        return 5.0f;
    }
}

/// <summary>ShapeC illustrates a single interface inheritance.</summary>
public class ShapeC : IArea {
    /// <summary>Explicit implementation of IArea.Size().</summary>
    float IArea.Size() {
        return 10.0f;
    }
}

/// <summary>
/// ShapeD illustrates a single interface inheritance.
/// It includes an explicit implementation of IArea.Size().
/// </summary>
public class ShapeD : IArea {
    /// <summary>It has nothing to do with IArea.Size().</summary>
    public float Size() {
        return 15.0f;
    }
    /// <summary>Explicit implementation of IArea.Size().</summary>
    float IArea.Size() {
        return 20.0f;
    }
}

/// <summary>Test driver</summary>
public static class Driver {
    /// <summary>Test Program</summary>
    public static void M() {
        Console.WriteLine(">> SI1");
        ShapeB shape1B = new();
        var size1B = shape1B.Size();
        Console.WriteLine($"size1B = {size1B}");
        ShapeC shape1C = new();
        var size1C = (shape1C as IArea).Size();
        Console.WriteLine($"size1C = {size1C}");
        IArea shape1Ca = new ShapeC();
        var size1Ca = shape1Ca.Size();
        Console.WriteLine($"size1Ca = {size1Ca}");
        ShapeD shape1D = new();
        var size1D = shape1D.Size();
        Console.WriteLine($"size1D = {size1D}");
        IArea shape1Da = new ShapeD();
        var size1Da = shape1Da.Size();
        Console.WriteLine($"size1Da = {size1Da}");
    }
}
```

### 命名空间 SI2

`*area-calculation/si2/Area.cs*`

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

`*area-calculation/si2/Shapes.cs*`

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

/// <summary>
/// ShapeD illustrates a single interface inheritance.
/// It includes an explicit implementation of IArea.Size().
/// </summary>
public class ShapeD : IArea {
    /// <summary>It has nothing to do with IArea.Size().</summary>
    public float Size() => 45.0f;
    /// <summary>An explicit implementation of IArea.Size().</summary>
    float IArea.Size() => 50.0f;
}

/// <summary>Test driver</summary>
public static class Driver {
    /// <summary>Test Program</summary>
    public static void M() {
        Console.WriteLine(">> SI2");
        IArea shape2Aa = new ShapeA();
        var size2Aa = shape2Aa.Size();
        Console.WriteLine($"size2Aa = {size2Aa}");
        var shape2B = new ShapeB();
        var size2B = shape2B.Size();
        Console.WriteLine($"size2B = {size2B}");
        IArea shape2Ba = new ShapeB();
        var size2Ba = shape2Ba.Size();
        Console.WriteLine($"size2Ba = {size2Ba}");
        IArea shape2Ca = new ShapeC();
        var size2Ca = shape2Ca.Size();
        Console.WriteLine($"size2Ca = {size2Ca}");
        var shape2D = new ShapeD();
        var size2D = shape2D.Size();
        Console.WriteLine($"size2D = {size2D}");
        IArea shape2Da = new ShapeD();
        var size2Da = shape2Da.Size();
        Console.WriteLine($"size2Da = {size2Da}");
    }
}
```

### 命名空间 MI1

`*area-calculation/mi1/Area.cs*`

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

`*area-calculation/mi1/Perimeter.cs*`

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

`*area-calculation/mi1/Shapes.cs*`

```csharp
namespace MI1;

/// <summary>ShapeB illustrates multiple interface inheritance.</summary>
public class ShapeB : IArea, IPerimeter {
    /// <summary>An implicit/normal implementation for IArea.Size() and IPerimeter.Size().</summary>
    public float Size() => 100.0f;
}

/// <summary>
/// ShapeC illustrates multiple interface inheritance.
/// It includes explicit implementations of IArea.Size() and IPerimeter.Size().
/// </summary>
public class ShapeC : IArea, IPerimeter {
    /// <summary>An explicit implementation of IArea.Size().</summary>
    float IArea.Size() => 110.0f;
    /// <summary>An explicit implementation of IPerimeter.Size().</summary>
    float IPerimeter.Size() => 120.0f;
}

/// <summary>
/// ShapeD illustrates multiple interface inheritance.
/// It includes explicit implementations of IArea.Size() and IPerimeter.Size().
/// It also includes a method Size() with the same name and signature.
/// </summary>
public class ShapeD : IArea, IPerimeter {
    /// <summary>It has nothing to do with IArea.Size() or IPerimeter.Size().</summary>
    public float Size() => 130.0f;
    /// <summary>An explicit implementation of IArea.Size().</summary>
    float IArea.Size() => 140.0f;
    /// <summary>An explicit implementation of
    /// IPerimeter.Size().</summary>
    float IPerimeter.Size() => 150.0f;
}

/// <summary>
/// ShapeG illustrates multiple interface inheritance.
/// It includes an explicit implementation for IArea.Size().
/// The IPerimeter.Size() method is implemented in the "normal" way.
/// </summary>
public class ShapeG : IArea, IPerimeter {
    /// <summary>An implicit/normal implementation of
    /// IPerimeter.Size().</summary>
    public float Size() => 160.0f;
    /// <summary>An explicit implementation of IArea.Size().</summary>
    float IArea.Size() => 170.0f;
}

/// <summary>
```
