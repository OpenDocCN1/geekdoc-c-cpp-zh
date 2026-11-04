```
```csharp
// Cast a long into a uint, no data lost.
l = 64000;
u = (uint) l;
Console.WriteLine("u after assigning 64000: " + u +
                  " -- no data lost.");

// Cast a long into a uint, data lost.
l = -12;
u = (uint) l;
Console.WriteLine("u after assigning -12: " + u +
                  " -- data lost.");

Console.WriteLine();

// Cast an int into a char.
b = 88; // ASCII code for X
ch = (char) b;
Console.WriteLine("ch after assigning 88: " + ch);
}
```
```

The output from the program is shown here:

```
```
Integer outcome of x / y: 3

b after assigning 255: 255 -- no data lost.
b after assigning 257: 1 -- data lost.

s after assigning 32000: 32000 -- no data lost.
s after assigning 64000: -1536 -- data lost.

u after assigning 64000: 64000 -- no data lost.
u after assigning -12: 4294967284 -- data lost.

ch after assigning 88: X
```
```

Let’s look at each assignment. The cast of (x / y) to int results in the truncation of the fractional component, and information is lost.

No loss of information occurs when b is assigned the value 255 because a `byte` can hold the value 255. However, when the attempt is made to assign b the value 257, information loss occurs because 257 exceeds a `byte`’s range. In both cases the casts are needed because there is no implicit conversion from `int` to `byte`.

When the `short` variable s is assigned the value 32,000 through the `uint` variable u, no data is lost because a `short` can hold the value 32,000. However, in the next assignment, u has the value 64,000, which is outside the range of a `short`, and data is lost. In both cases the casts are needed because there is no implicit conversion from `uint` to `short`.

Next, u is assigned the value 64,000 through the `long` variable l. In this case, no data is lost because 64,000 is within the range of a `uint`. However, when the value -12 is assigned to u, data is lost because a `uint` cannot hold negative numbers. In both cases the casts are needed because there is no implicit conversion from `long` to `uint`.

Finally, no information is lost, but a cast is needed when assigning a `byte` value to a `char`.