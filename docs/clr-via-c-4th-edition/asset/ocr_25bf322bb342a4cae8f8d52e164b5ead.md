```
```csharp
public static class Interlocked {
    public static T Exchange<T>(ref T location1, T value) where T : class;
    public static T CompareExchange<T>(
        ref T location1, T value, T comparand) where T : class;
}
```
```

# ## Generic Methods and Type Inference

For many developers, the C# generic syntax can be confusing with all of its less-than and greater-than signs. To help improve code creation, readability, and maintainability, the C# compiler offers type inference when calling a generic method. Type inference means that the compiler attempts to determine (or infer) the type to use automatically when calling a generic method. Here is some code that demonstrates type inference.

```
```csharp
private static void CallingSwapUsingInference() {
    Int32 n1 = 1, n2 = 2;
    Swap(ref n1, ref n2);// Calls Swap<Int32>

    String s1 = "Aidan";
    Object s2 = "Grant";
    Swap(ref s1, ref s2);// Error, type can't be inferred
}
```
```

In this code, notice that the calls to Swap do not specify type arguments in less-than/greater-than signs. In the first call to Swap, the C# compiler was able to infer that n1 and n2 are Int32s, and therefore, it should call Swap by using an Int32 type argument.

When performing type inference, C# uses the variable's data type, not the actual type of the object referred to by the variable. So in the second call to Swap, C# sees that s1 is a String and s2 is an Object (even though it happens to refer to a String). Because s1 and s2 are variables of different data types, the compiler can't accurately infer the type to use for Swap's type argument, and it issues the following message: error CS0411: The type arguments for method 'Program.Swap<T>(ref T, ref T)' cannot be inferred from the usage. Try specifying the type arguments explicitly.

A type can define multiple methods with one of its methods taking a specific data type and another taking a generic type parameter, as in the following example.

```
```csharp
private static void Display(String s) {
    Console.WriteLine(s);
}

private static void Display<T>(T o) {
    Display(o.ToString()); // Calls Display(String)
}
```
```

Here are some ways to call the Display method.

```
```csharp
Display("Jeff");           // Calls Display(String)
Display(123);              // Calls Display<T>(T)
Display<String>("Aidan");  // Calls Display<T>(T)
```
```