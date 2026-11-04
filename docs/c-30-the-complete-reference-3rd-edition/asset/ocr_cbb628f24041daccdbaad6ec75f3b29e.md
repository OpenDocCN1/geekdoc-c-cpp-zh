```
```csharp
class Test {
    static void Main() {
        XY xy = new XY(1, 2);

        Console.WriteLine(xy.X + "," + xy.Y);
    }
}
```
```

To use XY, all files must be included in the compile. For example, assuming the XY files are called xy1.cs, xy2.cs, and xy3.cs, and that the Test class is contained in a file called test.cs, then to compile Test, use the following command line:

```
```bash
csc test.cs xy1.cs xy2.cs xy3.cs
```
```

One last point: It is legal to have partial generic classes. However, the type parameters of each partial declaration must match the other parts.

# Partial Methods

As the preceding section described, you can use partial to create a partial type. Beginning with C# 3.0, there is a second use of partial that lets you create a partial method within a partial type. A partial method has its declaration in one part and its implementation in another part. Thus, in a partial class or structure, partial can be used to allow the declaration of a method to be separate from its implementation.

The key aspect of a partial method is that the implementation is not required! When the partial method is not implemented by another part of the class or structure, then all calls to the partial method are silently ignored. This makes it possible for a class to specify, but not require, optional functionality. If that functionality is not implemented, then it is simply ignored.

Here is an expanded version of the preceding program that creates a partial method called Show(). It is called by another method called ShowXY(). (For convenience, all pieces of the partial class XY are shown in one file, but they could have been organized into separate files, as illustrated in the preceding section.)

```
```csharp
// Demonstrate a partial method.
using System;

partial class XY {
    public XY(int a, int b) {
        X = a;
        Y = b;
    }

    // Declare a partial method.
    partial void Show();
}

partial class XY {
    public int X { get; set; }
```
```