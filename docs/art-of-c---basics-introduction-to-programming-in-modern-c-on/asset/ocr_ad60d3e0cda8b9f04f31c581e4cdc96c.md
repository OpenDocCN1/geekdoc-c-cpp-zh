```
Console.WriteLine($"c =\n{c}");
c.RotateWhite(false);
Console.WriteLine($"c =\n{c}");

c.RotateBlue();
Console.WriteLine($"c =\n{c}");
c.RotateBlue(false);
Console.WriteLine($"c =\n{c}");

c.RotateRed();
Console.WriteLine($"c =\n{c}");
c.RotateRed(false);
Console.WriteLine($"c =\n{c}");

c.RotateGreen();
Console.WriteLine($"c =\n{c}");
c.RotateGreen(false);
Console.WriteLine($"c =\n{c}");

c.RotateOrange();
Console.WriteLine($"c =\n{c}");
c.RotateOrange(false);
Console.WriteLine($"c =\n{c}");

c.RotateYellow();
Console.WriteLine($"c =\n{c}");
c.RotateYellow(false);
Console.WriteLine($"c =\n{c}");

// Shuffle the cube.

c.Randomize();
Console.WriteLine($"c =\n{c}");
```

rubiks-cube/Cube.cs

```
namespace Rubiks;
```