```
delegate bool IsEven(int v);

class SimpleLambdaDemo {
    static void Main() {
        // Create an Incr delegate instance that refers to
        // a lambda expression that increases its parameter by 2.
        Incr incr = count => count + 2;

        // Now, use the incr lambda expression.
        Console.WriteLine("Use incr lambda expression: ");
        int x = -10;
        while(x <= 0) {
            Console.Write(x + " ");
            x = incr(x); // increase x by 2
        }
        Console.WriteLine("\n");

        // Create an IsEven delegate instance that refers to
        // a lambda expression that returns true if its parameter
        // is even and false otherwise.
        IsEven isEven = n => n % 2 == 0;

        // Now, use the isEven lambda expression.
        Console.WriteLine("Use isEven lambda expression: ");
        for(int i=1; i <= 10; i++)
            if(isEven(i)) Console.WriteLine(i + " is even.");
    }
}
```

The output is shown here:

```
Use incr lambda expression:
-10 -8 -6 -4 -2 0

Use isEven lambda expression:
2 is even.
4 is even.
6 is even.
8 is even.
10 is even.
```

In the program, pay special attention to these declarations:

```
Incr incr = count => count + 2;
IsEven isEven = n => n % 2 == 0;
```

The first assigns to incr a lambda expression that returns the result of increasing the value passed to count by 2. This expression can be assigned to an Incr delegate because it is compatible with Incr's declaration. The argument used in the call to incr is passed to count. The result is returned. The second declaration assigns to isEven an expression that returns