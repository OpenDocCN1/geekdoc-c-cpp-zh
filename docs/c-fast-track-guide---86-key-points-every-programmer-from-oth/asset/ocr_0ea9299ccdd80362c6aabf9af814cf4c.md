# # 13. PATTERN MATCHING FOR TYPE-SAFE DATA HANDLING

Pattern matching in C# lets you inspect and extract data from objects based on their type and shape, improving code safety and readability.

Here’s a simple example showing how pattern matching can determine an object’s type and access its properties safely.

[Code Example]

```
```csharp
using System;
class Program
{
static void PrintShapeInfo(object shape)
{
// Use pattern matching to safely check type and extract data
if (shape is Circle c)
{
Console.WriteLine($"This is a circle with radius: {c.Radius}");
}
else if (shape is Rectangle r)
{
Console.WriteLine($"This is a rectangle with width {r.Width} and height {r.Height}");
}
else
{
Console.WriteLine("Unknown shape");
}
}
// Sample shape classes
class Circle { public double Radius { get; set; } }
class Rectangle { public double Width { get; set; } public double Height { get; set; } }
```
```