target method can assign the caller's original variable a new value. Since a copy is made, the caller's copy cannot be reassigned.

In more detail, a reference type variable contains an address of the memory location where the data is stored. If a reference type variable is passed by value, the address is copied from the caller to the method parameter. As a result, the target method cannot update the caller variable's address value but it may update the data within the reference type. Alternatively, if the method parameter is a value type, the value itself is copied into the parameter, and changing the parameter will not affect the original caller's variable.

# Reference Parameters (ref)

Consider Listing 4.12, which calls a function to swap two values, and Output 4.6, which shows the results.

```
LISTING 4.12: Passing Variables by Reference

class Program
{
    static void Main()
    {
        // ...
        string first = "first";
        string second = "second";
        Swap(ref first, ref second);

        System.Console.WriteLine(
            @"first = "{0}", second = "{1}"",
            first, second);
        // ...
    }

    static void Swap(ref string first, ref string second)
    {
        string temp = first;
        first = second;
        second = temp;
    }
}
```

```
OUTPUT 4.6:

first = "second", second = "first"
```