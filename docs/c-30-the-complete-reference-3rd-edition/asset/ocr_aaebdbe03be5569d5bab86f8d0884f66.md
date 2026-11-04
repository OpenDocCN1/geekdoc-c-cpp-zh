example, if the value 1.23 is assigned to an integer, the resulting value will simply be 1. The 0.23 is lost.

The following program demonstrates some type conversions that require casts. It also shows some situations in which the casts cause data to be lost.

```
// Demonstrate casting.

using System;

class CastDemo {
    static void Main() {
        double x, y;
        byte b;
        int i;
        char ch;
        uint u;
        short s;
        long l;

        x = 10.0;
        y = 3.0;

        // Cast double to int, fractional component lost.
        i = (int) (x / y);
        Console.WriteLine("Integer outcome of x / y: " + i);
        Console.WriteLine();

        // Cast an int into a byte, no data lost.
        i = 255;
        b = (byte) i;
        Console.WriteLine("b after assigning 255: " + b +
            " -- no data lost.");

        // Cast an int into a byte, data lost.
        i = 257;
        b = (byte) i;
        Console.WriteLine("b after assigning 257: " + b +
            " -- data lost.");
        Console.WriteLine();

        // Cast a uint into a short, no data lost.
        u = 32000;
        s = (short) u;
        Console.WriteLine("s after assigning 32000: " + s +
            " -- no data lost.");

        // Cast a uint into a short, data lost.
        u = 64000;
        s = (short) u;
        Console.WriteLine("s after assigning 64000: " + s +
            " -- data lost.");
        Console.WriteLine();
    }
}
```