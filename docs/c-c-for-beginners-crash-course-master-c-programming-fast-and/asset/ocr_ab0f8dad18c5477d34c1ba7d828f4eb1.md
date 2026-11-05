```
}
class Program
{
    static void Main(string[] args)
    {
        Program p = new Program();
        Console.WriteLine("Minimum value is:{0}",p.Min(3,4));
        Console.WriteLine("Minimum value is:{0}", p.Min(3.2F,1.2F));
        Console.ReadLine();
    }
}
}
```

When the code is compiled and executed, the output is:

Minimum value is: 3
Minimum value is: 1.2