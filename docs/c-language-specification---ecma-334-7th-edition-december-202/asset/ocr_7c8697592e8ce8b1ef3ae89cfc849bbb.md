```
```csharp
        Console.Write($"Array contains {args.Length} elements:");
        foreach (int i in args)
        {
            Console.Write($" {i}");
        }
        Console.WriteLine();
    }

    static void Main()
    {
        int[] arr = {1, 2, 3};
        F(arr);
        F(10, 20, 30, 40);
        F();
    }
}
```
```

produces the output

```
```
Array contains 3 elements: 1 2 3
Array contains 4 elements: 10 20 30 40
Array contains 0 elements:
```
```

The first invocation of F simply passes the array arr as a value parameter. The second invocation of F automatically creates a four-element int[] with the given element values and passes that array instance as a value parameter. Likewise, the third invocation of F creates a zero-element int[] and passes that instance as a value parameter. The second and third invocations are precisely equivalent to writing:

```
```csharp
F(new int[] {10, 20, 30, 40});
F(new int[] {});
```
```

*end example*

When performing overload resolution, a method with a parameter array might be applicable, either in its normal form or in its expanded form (§12.6.4.2). The expanded form of a method is available only if the normal form of the method is not applicable and only if an applicable method with the same signature as the expanded form is not already declared in the same type.

*Example: The example*

```
```csharp
class Test
{
    static void F(params object[] a) =>
        Console.WriteLine("F(object[])");

    static void F() =>
        Console.WriteLine("F()");

    static void F(object a0, object a1) =>
        Console.WriteLine("F(object,object)");

    static void Main()
    {
        F();
        F(1);
        F(1, 2);
        F(1, 2, 3);
    }
}
```
```