```
if(a) Console.WriteLine("a is true.");
if(b) Console.WriteLine("b is true.");
if(c) Console.WriteLine("c is true.");

if(!a) Console.WriteLine("a is false.");
if(!b) Console.WriteLine("b is false.");
if(!c) Console.WriteLine("c is false.");

Console.WriteLine();

Console.WriteLine("Use & and |");
if(a & b) Console.WriteLine("a & b is true.");
else Console.WriteLine("a & b is false.");

if(a & c) Console.WriteLine("a & c is true.");
else Console.WriteLine("a & c is false.");

if(a | b) Console.WriteLine("a | b is true.");
else Console.WriteLine("a | b is false.");

if(a | c) Console.WriteLine("a | c is true.");
else Console.WriteLine("a | c is false.");

Console.WriteLine();

// Now use short-circuit ops.
Console.WriteLine("Use short-circuit && and ||");
if(a && b) Console.WriteLine("a && b is true.");
else Console.WriteLine("a && b is false.");

if(a && c) Console.WriteLine("a && c is true.");
else Console.WriteLine("a && c is false.");

if(a || b) Console.WriteLine("a || b is true.");
else Console.WriteLine("a || b is false.");

if(a || c) Console.WriteLine("a || c is true.");
else Console.WriteLine("a || c is false.");
}
```

The output from the program is shown here:

```
Here is a: 5, 6, 7
Here is b: 10, 10, 10
Here is c: 0, 0, 0

a is true.
b is true.
c is false.

Use & and |
a & b is true.
```