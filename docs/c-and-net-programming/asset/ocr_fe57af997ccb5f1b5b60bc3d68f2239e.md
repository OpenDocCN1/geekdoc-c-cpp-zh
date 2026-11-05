```
{
static int Main()
{
    First fst = delegate()
    {
        Console.WriteLine("Happy new year 2017");
    }
    msg();
    return 0;
}
}
```

# 10. A delegate can return a value

# Example

```
using System;

delegate double Compute();

public class Demo
{
    public static double Product()
    {
        return 64*2;
    }
}

public class Program
{
    static int Main()
    {
        Compute cm = Demo.Product;

        Console.WriteLine("Number = {0}", cm());

        return 0;
    }
}
```

Input

Nil

# Output

128