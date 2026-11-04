```
Console.Write("Here is b: ");
b.Show();
Console.WriteLine();

c = a + b; // add a and b together
Console.Write("Result of a + b: ");
c.Show();
Console.WriteLine();

c = a + b + c; // add a, b, and c together
Console.Write("Result of a + b + c: ");
c.Show();
Console.WriteLine();

c = c - a; // subtract a
Console.Write("Result of c - a: ");
c.Show();
Console.WriteLine();

c = c - b; // subtract b
Console.Write("Result of c - b: ");
c.Show();
Console.WriteLine();

c = -a; // assign -a to c
Console.Write("Result of -a: ");
c.Show();
Console.WriteLine();

c = a++; // post-increment a
Console.WriteLine("Given c = a++");
Console.Write("c is ");
c.Show();
Console.WriteLine("a is ");
a.Show();

// Reset a to 1, 2, 3
a = new ThreeD(1, 2, 3);
Console.Write("\nResetting a to ");
a.Show();

c = ++a; // pre-increment a
Console.WriteLine("\nGiven c = ++a");
Console.Write("c is ");
c.Show();
Console.WriteLine("a is ");
a.Show();
}
}
```

The output from the program is shown here:

```
Here is a: 1, 2, 3
```