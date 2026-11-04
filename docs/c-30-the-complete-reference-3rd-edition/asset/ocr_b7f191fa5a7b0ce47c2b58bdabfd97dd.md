```
```csharp
Console.WriteLine(x + ", " + y + ", " + z);
}
class TrueFalseDemo {
    static void Main() {
        ThreeD a = new ThreeD(5, 6, 7);
        ThreeD b = new ThreeD(10, 10, 10);
        ThreeD c = new ThreeD(0, 0, 0);

        Console.Write("Here is a: ");
        a.Show();
        Console.Write("Here is b: ");
        b.Show();
        Console.Write("Here is c: ");
        c.Show();
        Console.WriteLine();

        if(a) Console.WriteLine("a is true.");
        else Console.WriteLine("a is false.");

        if(b) Console.WriteLine("b is true.");
        else Console.WriteLine("b is false.");

        if(c) Console.WriteLine("c is true.");
        else Console.WriteLine("c is false.");

        Console.WriteLine();

        Console.WriteLine("Control a loop using a ThreeD object.");
        do {
            b.Show();
            b--;
        } while(b);
    }
}
```
```

The output is shown here:

Here is a: 5, 6, 7
Here is b: 10, 10, 10
Here is c: 0, 0, 0

a is true.
b is true.
c is false.

Control a loop using a ThreeD object.
10, 10, 10
9, 9, 9
8, 8, 8
7, 7, 7
6, 6, 6
5, 5, 5