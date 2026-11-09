
Like delegates, an interface with generic type parameters can have its type parameters be contra-variant or covariant. Here is an example of an interface with a covariant generic type parameter.

```csharp
public interface IEnumerable<out T> : IEnumerator {
    Boolean MoveNext();
    T Current { get; }
}
```

Because T is covariant, it is possible to have the following code compile and run successfully.

```csharp
// This method accepts an IEnumerable of any reference type
Int32 Count(IEnumerable<Object> collection) { ... }
```

```csharp
// The call below passes an IEnumerable<String> to Count
Int32 c = Count(new[] { "Grant" });
```

> **Important** Sometimes developers ask why they must explicitly put in or out on generic type parameters. They think the compiler should be able to examine the delegate or interface declaration and automatically detect what generic type parameters can be contra-variant and covariant. Although it is true that the compiler could detect this automatically, the C# team believes that you are declaring a contract and that you should be explicit about what you want to allow. For example, it would be bad if the compiler determined that a generic type parameter could be contra-variant and then, in the future, you added a member to an interface that had the type parameter used in an output position. The next time you compile, the compiler would determine that the type parameter should be invariant, but all code sites that reference the other members might now produce errors if they had used the fact that the type parameter had been contra-variant.
>
> For this reason, the compiler team forces you to be explicit when declaring a generic type parameter. Then, if you attempt to use this type parameter in a context that doesn’t match how you declared it, the compiler issues an error letting you know that you are attempting to break the contract. If you then decide to break the contract by adding in or out on generic type parameters, you should expect to have to modify some of the code sites that were using the old contract.

### Generic Methods

When you define a generic class, struct, or interface, any methods defined in these types can refer to a type parameter specified by the type. A type parameter can be used as a method's parameter, a method's return type, or as a local variable defined inside the method. However, the CLR also supports the ability for a method to specify its very own type parameters. And these type parameters can also be used for parameters, return types, or local variables.

Here is a somewhat contrived example of a type that defines a type parameter and a method that has its very own type parameter.

```csharp
internal sealed class GenericType<T> {
    private T m_value;

    public GenericType(T value) { m_value = value; }

    public TOutput Converter<TOutput>() {
        TOutput result = (TOutput) Convert.ChangeType(m_value, typeof(TOutput));
        return result;
    }
}
```

In this example, you can see that the `GenericType` class defines its own type parameter (T), and the `Converter` method defines its own type parameter (TOutput). This allows a `GenericType` to be constructed to work with any type. The `Converter` method can convert the object referred to by the `m_value` field to various types depending on what type argument is passed to it when called. The ability to have type parameters and method parameters allows for phenomenal flexibility.

A reasonably good example of a generic method is the Swap method.

```csharp
private static void Swap<T>(ref T o1, ref T o2) {
    T temp = o1;
    o1 = o2;
    o2 = temp;
}
```

Code can now call Swap as follows.

```csharp
private static void CallingSwap() {
    Int32 n1 = 1, n2 = 2;
    Console.WriteLine("n1={0}, n2={1}", n1, n2);
    Swap<Int32>(ref n1, ref n2);
    Console.WriteLine("n1={0}, n2={1}", n1, n2);

    String s1 = "Aidan", s2 = "Grant";
    Console.WriteLine("s1={0}, s2={1}", s1, s2);
    Swap<String>(ref s1, ref s2);
    Console.WriteLine("s1={0}, s2={1}", s1, s2);
}
```

Using generic types with methods that take out and ref parameters can be particularly interesting because the variable you pass as an out/ref argument must be the same type as the method’s parameter to avoid a potential type safety exploit. This issue related to out/ref parameters is discussed toward the end of the “Passing Parameters by Reference to a Method” section in Chapter 9, “Parameters.” In fact, the `Interlocked` class’s `Exchange` and `CompareExchange` methods offer generic overloads for precisely this reason.¹

¹ The where clause will be explained in the “Verifiability and Constraints” section later in this chapter.

```csharp
public static class Interlocked {
    public static T Exchange<T>(ref T location1, T value) where T : class;
    public static T CompareExchange<T>(
        ref T location1, T value, T comparand) where T : class;
}
```

### Generic Methods and Type Inference

For many developers, the C# generic syntax can be confusing with all of its less-than and greater-than signs. To help improve code creation, readability, and maintainability, the C# compiler offers type inference when calling a generic method. Type inference means that the compiler attempts to determine (or infer) the type to use automatically when calling a generic method. Here is some code that demonstrates type inference.

```csharp
private static void CallingSwapUsingInference() {
    Int32 n1 = 1, n2 = 2;
    Swap(ref n1, ref n2); // Calls Swap<Int32>

    String s1 = "Aidan";
    Object s2 = "Grant";
    Swap(ref s1, ref s2); // Error, type can't be inferred
}
```

In this code, notice that the calls to Swap do not specify type arguments in less-than/greater-than signs. In the first call to Swap, the C# compiler was able to infer that n1 and n2 are Int32s, and therefore, it should call Swap by using an Int32 type argument.

When performing type inference, C# uses the variable's data type, not the actual type of the object referred to by the variable. So in the second call to Swap, C# sees that s1 is a String and s2 is an Object (even though it happens to refer to a String). Because s1 and s2 are variables of different data types, the compiler can't accurately infer the type to use for Swap's type argument, and it issues the following message: error CS0411: The type arguments for method 'Program.Swap<T>(ref T, ref T)' cannot be inferred from the usage. Try specifying the type arguments explicitly.

A type can define multiple methods with one of its methods taking a specific data type and another taking a generic type parameter, as in the following example.

```csharp
private static void Display(String s) {
    Console.WriteLine(s);
}

private static void Display<T>(T o) {
    Display(o.ToString()); // Calls Display(String)
}
```

Here are some ways to call the Display method.

```csharp
Display("Jeff");           // Calls Display(String)
Display(123);              // Calls Display<T>(T)
Display<String>("Aidan");  // Calls Display<T>(T)
```

Every type supports assignment and calls to methods defined by Object (such as ToString and Equals).

Now look at the following method.

```csharp
private static T Min<T>(T o1, T o2) {
    if (o1.CompareTo(o2) < 0) return o1;
    return o2;
}
```

The Min method attempts to use the o1 variable to call the CompareTo method. But there are lots of types that do not offer a CompareTo method, and therefore, the C# compiler can't compile this code and guarantee that this method would work for all types. If you attempt to compile the above code, the compiler issues the following message: error CS1061: 'T' does not contain a definition for 'CompareTo' and no accessible extension method 'CompareTo' accepting a first argument of type 'T' could be found (are you missing a using directive or an assembly reference?)

So it would seem that when using generics, you can declare variables of a generic type, perform some variable assignments, call methods defined by Object, and that's about it! This makes generics practically useless. Fortunately, compilers and the CLR support a mechanism called constraints that you can take advantage of to make generics useful again.

A constraint is a way to limit the number of types that can be specified for a generic argument. Limiting the number of types allows you to do more with those types. Here is a new version of the Min method that specifies a constraint (in bold).

```csharp
public static T Min<T>(T o1, T o2) where T : IComparable<T> {
    if (o1.CompareTo(o2) < 0) return o1;
    return o2;
}
```

The C# `where` token tells the compiler that any type specified for T must implement the generic IComparable interface of the same type (T). Because of this constraint, the compiler now allows the method to call the CompareTo method because this method is defined by the `IComparable<T>` interface.

Now, when code references a generic type or method, the compiler is responsible for ensuring that a type argument that meets the constraints is specified. For example, the following code causes the compiler to issue the following message: error CS0311: The type 'object' cannot be used as type parameter 'T' in the generic type or method 'SomeType.Min<T>(T, T)'. There is no implicit reference conversion from 'object' to 'System.IComparable<object>'.

```csharp
private static void CallMin() {
    Object o1 = "Jeff", o2 = "Richter";
    Object oMin = Min<Object>(o1, o2);   // Error CS0311
}
```

The compiler issues the error because System.Object doesn't implement the `IComparable<Object>` interface. In fact, System.Object doesn't implement any interfaces at all.
