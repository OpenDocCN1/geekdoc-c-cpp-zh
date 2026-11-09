```
```csharp
using System;

public static class Program {
    public static void Main() {
        Char  c;
        Int32 n;

        // Convert number <-> character using C# casting
        c = (Char) 65;
        Console.WriteLine(c);                 // Displays "A"

        n = (Int32) c;
        Console.WriteLine(n);                 // Displays "65"

        c = unchecked((Char) (65536 + 65));
        Console.WriteLine(c);                 // Displays "A"


        // Convert number <-> character using Convert
        c = Convert.ToChar(65);
        Console.WriteLine(c);                 // Displays "A"

        n = Convert.ToInt32(c);
        Console.WriteLine(n);                 // Displays "65"

        // This demonstrates Convert's range checking
        try {
            c = Convert.ToChar(70000);        // Too big for 16 bits
            Console.WriteLine(c);             // Doesn't execute
        }
        catch (OverflowException) {
            Console.WriteLine("Can't convert 70000 to a Char.");
        }


        // Convert number <-> character using IConvertible
        c = ((IConvertible) 65).ToChar(null);
        Console.WriteLine(c);                 // Displays "A"

        n = ((IConvertible) c).ToInt32(null);
        Console.WriteLine(n);                 // Displays "65"
    }
}
```
```

# The System.String Type

One of the most used types in any application is System.String. A String represents an immutable sequence of characters. The String type is derived immediately from Object, making it a reference type, and therefore, String objects (its array of characters) always live in the heap, never on a thread’s