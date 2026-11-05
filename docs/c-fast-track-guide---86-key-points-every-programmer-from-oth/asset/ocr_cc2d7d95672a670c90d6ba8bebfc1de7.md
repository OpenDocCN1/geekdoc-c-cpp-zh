```
Y = y;
}
public void Print()
{
Console.WriteLine($"Point is at ({X}, {Y})");
}
}
class Program
{
static void Main()
{
Point p = new Point(10, 20);
p.Print();
// The following line would cause a compile error if uncommented:
// p.X = 30;
}
}
```

![](bbox=[0.14, 0.84, 0.22, 0.88])

[Execution Result]