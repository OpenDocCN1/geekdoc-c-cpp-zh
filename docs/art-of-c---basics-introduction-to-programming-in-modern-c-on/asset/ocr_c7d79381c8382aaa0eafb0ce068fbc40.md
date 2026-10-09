```
/// <summary>
/// ShapeD illustrates a single interface inheritance.
/// It includes an explicit implementation of IArea.Size().
///</summary>
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

```