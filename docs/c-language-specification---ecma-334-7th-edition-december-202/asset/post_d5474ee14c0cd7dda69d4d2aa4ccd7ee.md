
When a formal parameter is an input parameter, the corresponding argument in a method invocation shall consist of either the keyword in followed by a variable_reference (§9.2.8) of the same type as the formal parameter, or an expression for which an implicit conversion (§10.2) exists from that argument expression to the type of the corresponding parameter. A variable shall be definitely assigned before it can be passed as an input parameter.

It is a compile-time error to modify the value of an input parameter.

Within a method, an input parameter is always considered definitely assigned.

Input parameters are not allowed on functions declared as an iterator (§15.14) or async function (§15.15).

In a method that takes input parameters, it is possible for multiple names to represent the same storage location.

## 15.6.2.4 Reference parameters

A parameter declared with a ref modifier is a reference parameter. A reference parameter is a local reference variable (§9.7) that gets its initial referent from the corresponding argument supplied in the method invocation.

> Note: As with reference variables the referent of a reference parameter can be changed using the ref assignment (= ref) operator. end note

When a formal parameter is a reference parameter, the corresponding argument in a method invocation shall consist of the keyword ref followed by a variable_reference (§9.5) of the same type as the formal parameter. A variable shall be definitely assigned before it can be passed as a reference parameter.

Within a method, a reference parameter is always considered definitely assigned.

A method declared as an iterator (§15.14) may not have reference parameters.

Example: The example

```
class Test
{
    static void Swap(ref int x, ref int y)
    {
        int temp = x;
        x = y;
        y = temp;
    }

    static void Main()
    {
        int i = 1, j = 2;
        Swap(ref i, ref j);
        Console.WriteLine($"i = {i}, j = {j}");
    }
}
```

produces the output

i = 2, j = 1

For the invocation of Swap in Main, x represents i and y represents j. Thus, the invocation has the effect of swapping the values of i and j.

end example

In a method that takes reference parameters, it is possible for multiple names to represent the same storage location.

Example: In the following code

```csharp
class A
{
    string s;
    void F(ref string a, ref string b)
    {
        s = "One";
        a = "Two";
        b = "Three";
    }

    void G()
    {
        F(ref s, ref s);
    }
}
```

the invocation of F in G passes a reference to s for both a and b. Thus, for that invocation, the names s, a, and b all refer to the same storage location, and the three assignments all modify the instance field s.

end example

## 15.6.2.5 Output parameters

A parameter declared with an out modifier is an output parameter. An output parameter is a local reference variable (§9.7) that gets its initial referent from the corresponding argument supplied in the method invocation.

When a formal parameter is an output parameter, the corresponding argument in a method invocation shall consist of the keyword out followed by a variable_reference (§9.5) of the same type as the formal parameter. A variable need not be definitely assigned before it can be passed as an output parameter, but following an invocation where a variable was passed as an output parameter, the variable is considered definitely assigned.

Within a method, just like a local variable, an output parameter is initially considered unassigned and shall be definitely assigned before its value is used.

Every output parameter of a method shall be definitely assigned before the method returns.

A method declared as a partial method (§15.6.9) or an iterator (§15.14) may not have output parameters.

Output parameters are typically used in methods that produce multiple return values.

Example:

```csharp
class Test
{
    static void SplitPath(string path, out string dir, out string name)
    {
        int i = path.Length;
        while (i > 0)
        {
            char ch = path[i - 1];
            if (ch == '\\' || ch == '/' || ch == ':')
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

produces the output

```
Array contains 3 elements: 1 2 3
Array contains 4 elements: 10 20 30 40
Array contains 0 elements:
```

The first invocation of F simply passes the array arr as a value parameter. The second invocation of F automatically creates a four-element int[] with the given element values and passes that array instance as a value parameter. Likewise, the third invocation of F creates a zero-element int[] and passes that instance as a value parameter. The second and third invocations are precisely equivalent to writing:

```csharp
F(new int[] {10, 20, 30, 40});
F(new int[] {});
```

*end example*

When performing overload resolution, a method with a parameter array might be applicable, either in its normal form or in its expanded form (§12.6.4.2). The expanded form of a method is available only if the normal form of the method is not applicable and only if an applicable method with the same signature as the expanded form is not already declared in the same type.

*Example: The example*

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
F(1, 2, 3, 4);
}
```

produces the output

```
F()
F(object[])
F(object,object)
F(object[])
F(object[])
```

In the example, two of the possible expanded forms of the method with a parameter array are already included in the class as regular methods. These expanded forms are therefore not considered when performing overload resolution, and the first and third method invocations thus select the regular methods. When a class declares a method with a parameter array, it is not uncommon to also include some of the expanded forms as regular methods. By doing so, it is possible to avoid the allocation of an array instance that occurs when an expanded form of a method with a parameter array is invoked.

end example

An array is a reference type, so the value passed for a parameter array can be null.

Example: The example:

```
class Test
{
    static void F(params string[] array) =>
        Console.WriteLine(array == null);

    static void Main()
    {
        F(null);
        F((string) null);
    }
}
```

produces the output:

```
True
False
```

The second invocation produces False as it is equivalent to F(new string[] { null }) and passes an array containing a single null reference.

end example

When the type of a parameter array is object[], a potential ambiguity arises between the normal form of the method and the expanded form for a single object parameter. The reason for the ambiguity is that an object[] is itself implicitly convertible to type object. The ambiguity presents no problem, however, since it can be resolved by inserting a cast if needed.

Example: The example

```
class Test
{
    static void F(params object[] args)
    {
        foreach (object o in args)
```

```
{
    Console.Write(o.GetType().FullName);
    Console.Write(" ");
}
Console.WriteLine();
}

static void Main()
{
    object[] a = {1, "Hello", 123.456};
    object o = a;
    F(a);
    F((object)a);
    F(o);
    F((object[])o);
}
```

produces the output

System.Int32 System.String System.Double
System.Object[]
System.Object[]
System.Int32 System.String System.Double

In the first and last invocations of F, the normal form of F is applicable because an implicit conversion exists from the argument type to the parameter type (both are of type object[]). Thus, overload resolution selects the normal form of F, and the argument is passed as a regular value parameter. In the second and third invocations, the normal form of F is not applicable because no implicit conversion exists from the argument type to the parameter type (type object cannot be implicitly converted to type object[]). However, the expanded form of F is applicable, so it is selected by overload resolution. As a result, a one-element object[] is created by the invocation, and the single element of the array is initialized with the given argument value (which itself is a reference to an object[]).

*end example*

## 15.6.3 Static and instance methods

When a method declaration includes a static modifier, that method is said to be a static method. When no static modifier is present, the method is said to be an instance method.

A static method does not operate on a specific instance, and it is a compile-time error to refer to this in a static method.

An instance method operates on a given instance of a class, and that instance can be accessed as this (§12.8.13).

The differences between static and instance members are discussed further in §15.3.8.

## 15.6.4 Virtual methods

When an instance method declaration includes a virtual modifier, that method is said to be a virtual method. When no virtual modifier is present, the method is said to be a non-virtual method.

The implementation of a non-virtual method is invariant: The implementation is the same whether the method is invoked on an instance of the class in which it is declared or an instance of a derived class. In
