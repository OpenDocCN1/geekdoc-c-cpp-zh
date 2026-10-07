
## LISTING 10.4: Overloading the – and + Unary Operators

```cs
// ...
    public static Latitude operator -(Latitude latitude)
{
        return new Latitude(-latitude.Degrees);
    }

    public static Latitude operator +(Latitude latitude)
{
        return latitude;
    }

    // ...
```

public struct Longitude
{

```cs
// ...
    public static Longitude operator -(Longitude longitude)
{
        return new Longitude(-longitude.Degrees);
    }

    public static Longitude operator +(Longitude longitude)
{
        return longitude;
    }

    // ...
```

public readonly struct Arc
{

```cs
// ...
    public static Arc operator -(Arc arc)
{
        // Uses unary – operator defined on
        // Longitude and Latitude
        return new Arc(-arc.LongitudeDifference, -arc.LatitudeDifference);
    }
```

```cs
public static Arc operator +(Arc arc)
{
    return arc;
```

## # Chapter 10: Well-Formed Types

Overloading the true and false operators is subject to the additional requirement that both must be overloaded—not just one of the two. The signatures are the same as with other operator overloads; however, the return must be a bool, as demonstrated in Listing 10.5.

## Listing 10.5: Overloading the true and false Operators

```cs
public static bool operator false(object item)
{
    // ...
}
public static bool operator true(object item)
{
    // ...
}
```

You can use types with overloaded true and false operators in if, do, while, and for controlling expressions.

## Conversion Operators

Currently, there is no support in Longitude, Latitude, and Coordinate for casting to an alternative type. For example, there is no way to cast a double into a Longitude or Latitude instance. Similarly, there is no support for assigning a Coordinate using a string. Fortunately, C# provides for the definition of methods specifically intended to handle the converting of one type to another. Furthermore, the method declaration allows for specifying whether the conversion is implicit or explicit.

## ADVANCED TOPIC

### Cast Operator (())

Implementing the explicit and implicit conversion operators is not technically overloading the cast operator (()). However, this action is effectively what takes place, so defining a cast operator is common terminology for implementing explicit or implicit conversion.

Defining a conversion operator is similar in style to defining any other operator, except that the “operator” is the result type of the conversion. Additionally, the operator keyword follows a keyword that indicates whether the conversion is implicit or explicit (see Listing 10.6).

### Listing 10.6: Providing an Implicit Conversion between Latitude and double

```cs
public readonly struct Latitude
{
    // ...
    public double DecimalDegrees(double decimalDegrees)
    {
        DecimalDegrees = Normalize(decimalDegrees);
    }
    public double DecimalDegrees { get; }

    // ...
    public static implicit operator double(Latitude latitude)
    {
        return latitude.DecimalDegrees;
    }
    public static implicit operator Latitude(double degrees)
    {
        return new Latitude(degrees);
    }

    // ...
}
```

With these conversion operators, you now can convert doubles implicitly to and from Latitude objects. Assuming similar conversions exist for Longitude, you can simplify the creation of a Coordinate object by specifying the decimal degrees portion of each coordinate portion (e.g., coordinate = new Coordinate(43, 172));

> NOTE
> When implementing a conversion operator, either the return or the parameter must be of the enclosing type—in support of encapsulation. C# does not allow you to specify conversions outside the scope of the converted type.

## Guidelines for Conversion Operators

The difference between defining an implicit and an explicit conversion operator centers on preventing an unintentional implicit conversion that results in undesirable behavior. You should be aware of two possible consequences of using the explicit conversion operator. First, conversion operators that throw exceptions should always be explicit, thereby requiring the user. For example, it is highly likely that a string will not conform to the format that a conversion from string to Coordinate requires. Given the chance of a failed conversion, you should define the particular conversion operator as explicit, thereby requiring that you be intentional about the conversion and ensure that the format is correct or, alternatively, that you provide code to handle the possible exception. Frequently, the pattern for conversion is that one direction (string to Coordinate) is explicit and the reverse (Coordinate to string) is implicit.

A second consideration is that some will be lossy. Converting from a float (4.2) to an int is entirely valid, assuming an awareness of the fact that the decimal portion of the float will be lost. Any conversions that will lose data and will not successfully convert back to the original type should be defined as explicit. If an explicit cast is unexpectedly lossy or invalid, consider throwing a System.InvalidCastException.

## Referencing Other Assemblies

### Guidelines

- DO NOT provide an implicit conversion operator if the conversion is lossy.
- DO NOT throw exceptions from implicit conversions.

## Referencing Other Assemblies

Instead of placing all code into one monolithic binary file, C# and the underlying CLI framework allow you to spread code across multiple assemblies. This approach enables you to reuse assemblies across multiple executables.

## BEGINNER TOPIC

### Class Libraries
The HelloWorld program is one of the most trivial programs you can write. Real-world programs are more complex, and as complexity increases, it helps to organize the complexity by breaking programs into multiple parts. To do this, developers move portions of a program into separate compiled units called class libraries or, simply, libraries. Programs then reference and rely on class libraries.

Frequently, the code we write could be useful to more than one program. Imagine, for example, using the Longitude, Latitude, and Coordinate classes from a mapping program and a digital photo geocoding program or writing command-line parser class. Classes and sets of classes like these can be written once and reused from many different programs. As such, they need to be grouped together into an assembly a library or class library and written for the purposes of reuse rather than only within a single program.

To create a library rather than a console project, follow the same directions provided in Chapter 1, with one exception: For .NET CLI, use Class Library or classlib for the project. Similarly, with Visual Studio 2022, from the File->New Project... menu item (Ctrl+Shift+N), use the Search box to find All Class Library templates, and then select Class Library—the Visual C# version, or use GeoCoordinates for the project name.

Next, place the source code from Listing 10.4 into separate files for each struct and name the file after the struct and build the project. Building the project will compile the C# code into an assembly—a GeoCoordinates.dll file—and place it into a subdirectory of .\bin\.

## Chapter 10: Well-Formed Types

### Referencing a Library

Given the library, we need to reference it from a program. For example, for a new console program using the Program class from Listing 10.3, we need to add a reference to the GeoCoordinates.dll assembly, identifying where the library is located and embedding metadata that uniquely identifies the library into the program. There are several ways to do this. First, you can reference the library project file (*.csproj), identifying which project contains library source code and forming a dependency between the two projects. You can't compile the program referencing the library until the library is compiled. This dependency causes the library to compile (if it isn't compiled already) when the program compiles. In other words, reference the compiled library (*.dll) rather than the project. This makes sense when the library is compiled separately from the program, as by by team within your organization.

Third, you can reference a NuGet package, as described in the next section.
