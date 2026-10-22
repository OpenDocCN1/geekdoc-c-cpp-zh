```
Console.ReadLine();
}
}
}
```

# Generic Class and Methods

C# also have classes and methods not made for a specific type but can be used with any general type.

We normally use <> brackets for this purpose. Suppose we have set a class or method with <T> and run each operation on T inside the method or the class. And we added an integer while calling it—<int>, then the T inside the class or the method will be changed to take int during the time of compilation. Let's look at generic classes here:

```
using System;
class Generic<T>
{
    private T genericVariable;
    public Generic(T genericValue)
    {
        this.genericVariable = genericValue;
    }
    public void Display()
    {
        Console.WriteLine(this.genericVariable);
    }
}
class Test
{
    static void Main(string[] args)
```