The CLR allows you to pass parameters by reference instead of by value. In C#, you do this by using the out and ref keywords. Both keywords tell the C# compiler to emit metadata indicating that this designated parameter is passed by reference, and the compiler uses this to generate code to pass the address of the parameter rather than the parameter itself.

From the CLR's perspective, out and ref are identical—that is, the same IL is produced regardless of which keyword you use, and the metadata is also identical except for 1 bit, which is used to record whether you specified out or ref when declaring the method. However, the C# compiler treats the two keywords differently, and the difference has to do with which method is responsible for initializing the object being referred to. If a method's parameter is marked with out, the caller isn't expected to have initialized the object prior to calling the method. The called method can't read from the value, and the called method must write to the value before returning. If a method's parameter is marked with ref, the caller must initialize the parameter's value prior to calling the method. The called method can read from the value and/or write to the value.

Reference and value types behave very differently with out and ref. Let's look at using out and ref with value types first.

```
```csharp
public sealed class Program {
    public static void Main() {
        Int32 x;                // x is uninitialized.
        GetVal(out x);          // x doesn't have to be initialized.
        Console.WriteLine(x);   // Displays "10"
    }

    private static void GetVal(out Int32 v) {
        v = 10;  // This method must initialize v.
    }
}
```
```

In this code, x is declared in Main's stack frame. The address of x is then passed to GetVal. GetVal's v is a pointer to the Int32 value in Main's stack frame. Inside GetVal, the Int32 that v points to is changed to 10. When GetVal returns, Main's x has a value of 10, and 10 is displayed on the console. Using out with large value types is efficient because it prevents instances of the value type's fields from being copied when making method calls.

Now let's look at an example that uses ref instead of out.

```
```csharp
public sealed class Program {
    public static void Main() {
        Int32 x = 5;            // x is initialized.
        AddVal(ref x);          // x must be initialized.
        Console.WriteLine(x);   // Displays "15"
    }

    private static void AddVal(ref Int32 v) {
        v += 10; // This method can use the initialized value in v.
    }
}
```
```