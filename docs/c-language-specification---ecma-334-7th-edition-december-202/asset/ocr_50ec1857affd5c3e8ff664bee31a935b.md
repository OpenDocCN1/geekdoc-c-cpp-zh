```
```csharp
{
    D[] result = new D[3];
    for (int i = 0; i < 3; i++)
    {
        int x = i * 2 + 1;
        result[i] = () => Console.WriteLine(x);
    }
    return result;
}

static void Main()
{
    foreach (D d in F())
    {
        d();
    }
}
```
```

produces the output:

1  
3  
5

However, when the declaration of x is moved outside the loop:

```
```csharp
delegate void D();

class Test
{
    static D[] F()
    {
        D[] result = new D[3];
        int x;
        for (int i = 0; i < 3; i++)
        {
            x = i * 2 + 1;
            result[i] = () => Console.WriteLine(x);
        }
        return result;
    }

    static void Main()
    {
        foreach (D d in F())
        {
            d();
        }
    }
}
```
```

the output is:

5  
5  
5