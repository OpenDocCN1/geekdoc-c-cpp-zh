
## Why You Should Use Generics

In Hour 9, you saw how to create an array of integer values. Because you explicitly stated the data type for each element in the array was `int`, the compiler verified that you were assigning only integer values to each element. You also operated on each element using methods and operators defined for integer values. Imagine the code required to find the minimum value of an arbitrary array of integers (see Listing 11.1).

### LISTING 11.1 Finding the Minimum Value

```csharp
public int Min(int[] values)
{
    int min = values[0];
    foreach (int value in values)
    {
        if (value.CompareTo(min) < 0)
        {
            min = value;
        }
    }
    return min;
}
```

What would happen if you wanted this to work with any numeric type? Without generics, you would need to write a different version of Min for each numeric type with the only difference being the data type. Although that is certainly possible, it introduces a lot of complexity and redundancy in your code.

Knowing that the `IComparable` interface defines a `CompareTo` method, you could write this in a more generic way using objects. This would allow you to write the code once yet still use it for an array of any numeric type, as shown in Listing 11.2.

### LISTING 11.2 Finding the Minimum Value Using Objects

```csharp
public object Min(object[] values)
{
    IComparable min = (IComparable)values[0];
    foreach (object value in values)
    {
        if (((IComparable)value).CompareTo(min) < 0)
        {
            min = (IComparable)value;
        }
    }
    return min;
}
```

Unfortunately, although you gained by needing to write the code only once, you also lost any type safety. In addition, an array of integers is not convertible to an array of objects. Because this method works with objects, what happens when it is passed an array that was defined like:

`object[] array = { 5, 3, "a", "hello" };`

This is legal because the array holds elements of type object and any value is implicitly convertible to object.

### Try It Yourself

#### Finding the Minimum Without Generics

By following these steps, you see how creating a generalized method without the use of generics prevents type safety yet still compiles correctly. Keep Visual Studio open at the end of this exercise because you will use this application later.

- 1. Create a new Console application.
- 2. In the Program.cs file, implement the two functions shown in Listings 11.1 and 11.2. Make sure you declare these methods as static.
- 3. Change both versions of Min so that the first line of each has a Console.WriteLine to print out which method is executed.
- 4. In the Main method of the Program.cs file, declare and initialize an integer array named array of five elements followed by a Console.WriteLine statement to print the minimum value.
- 5. Run the application using Ctrl+F5, and make sure the output displays the correct minimum value for your array.
- 6. Change the declaration of array from int to long.
- 7. You should notice the call to Min has a red squiggly line, and two errors are reported in the error window. This happens because there is no implementation of Min that takes a long[] as a parameter.
- 8. Change the declaration of array from long to object to remove the compiler errors.
- 9. Run the application again using Ctrl+F5, and make sure the output displays the correct minimum value for your array. (This should be the same value as shown from step 4.)
- 10. Change the elements of array to the following:

`{ 5, 3, "a", "hello", 1 };`

- 11. Run the application using Ctrl+F5, and observe that the output matches what is shown in Figure 11.1.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_268_0.png)

**FIGURE 11.1**
Runtime exception generated from the lack of type-safety

Not only have you lost type safety, you are also performing *n*+1 conversion operations, where *n* is the number of elements in the array. As you might guess, the larger the array, the more expensive this method becomes.

Using generics, this problem becomes simple. You gain the ability to write the code only once without losing type safety or incurring multiple conversion operations. Listing 11.3 shows the same **Min** method defined using generics. If you compare this to the method defined in Listing 11.1, you can see that they are almost identical.

### LISTING 11.3 Finding the Minimum Value Using Generics

```csharp
public T Min<T>(T[] values) where T: IComparable<T>
{
    T min = values[0];
    foreach (T value in values)
    {
        if (value.CompareTo(min) < 0)
        {
            min = value;
        }
    }
    return min;
}
```

> **By the Way**
> `where T : IComparable<T>`
> This constraint might be a bit confusing because it looks like there is a circular dependency here. In fact, it's actually straightforward and means that T must be a type that can be compared to other T's.

The biggest difference is that the generic version uses a generic type parameter *T*, specified by the **<T>** syntax, after the method name. The type parameter acts as a placeholder for a real type supplied at compile time. In this example, we know that any real type used in place of T must implement the IComparable<T> interface, where the T of the interface is the type parameter of the generic method. This constrains, or limits, the type parameter to be any type that implements the interface.

### Watch Out!

#### C# Generics, C++ Templates, and Java Generics

Although C# generics, Java generics, and C++ templates all provide support for parameterized types, several significant differences exist among them. The syntax for C# generics is similar to that of Java and simpler than C++ templates.

All the type substitutions for C# generics occur at runtime, thereby preserving the generic type information for instantiated objects. In Java, generics are a language-only construction implemented only in the compiler in a technique known as type erasure. As a result, the generic type information for instantiated objects is not available at runtime. This is different from C++ templates that are expanded at compile-time, generating additional code for each template type.

C# generics do not provide the same amount of flexibility as C++ templates and Java generics in some cases. For example, C# generics do not support the idea of a wildcard for the type parameter like Java generics. It is also not possible to call arithmetic operators on a type parameter, as you can in C++ templates.

### Try It Yourself

#### Finding the Minimum with Generics

To modify the code written in the previous exercise to use a generic version of the Min function, follow these steps. If you closed Visual Studio, repeat the previous exercise first.

- 1. In the Program.cs file, implement the generic function shown in Listing 11.3. Make sure you declare this method as static and make the same change to add as the first line a call to Console.Write to print out the method name.
- 2. Change the declaration of array so that it is `int[]` and change the elements to be all numeric values again so that your program compiles and executes correctly.
- 3. Run the application using Ctrl+F5. Notice that you are still using the non-generic strongly typed version of Min.
- 4. Change only the type of array so that it is `long[]`.
- 5. Run the application again using Ctrl+F5. Notice that you are now using the generic version of Min.
- 6. Change only the elements of array to the following:

`{ 5, 3, "a", "hello", 1 };`

- 7. Run the application again. This time, instead of running and generating a runtime exception, you receive two compiler errors saying that you cannot implicitly convert type ‘string’ to ‘long’, as shown in Figure 11.2.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_270_0.png)
![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_270_1.png)

## Understanding Generic Type Parameters

Just as methods have parameters and the values of those parameters at runtime are arguments, generic types and methods also type parameters and type arguments. Type parameters act as placeholders for a type argument supplied at compile time.

This is more than simple text replacement of the type parameter with the supplied type. When a generic type or method is compiled, the CIL contains metadata identifying it as having type parameters. At runtime, the JIT creates a constructed type with the supplied type parameter substituted in the appropriate locations.

A generic type or method can have multiple type parameters separated by a comma (,) in the type parameter specification. Several of the generic collection classes, such as `Dictionary<TKey, TValue>`, and `KeyValuePair<TKey, TValue>`, use more than one type parameter. The `Tuple` class, which we discuss a bit later, is also generic and has up to eight type parameters.

### Constraints

Constraints enable you to apply restrictions on the types used for the type arguments at compile-time. These restrictions are specified using the where keyword, as you saw in Listing 11.3. When you constrain a type parameter, the number of allowable operations and methods increase to those supported by the constrained type and all types in its inheritance chain.

There are six possible constraints, as shown in Table 11.1.

**TABLE 11.1 Generic Type Parameter Constraints**

| Constraint | Description |
| :--- | :--- |
| where T : struct | The type argument must be a value type, except a Nullable value type. |
| where T : class | The type argument must be a reference type. This applies to any class, interface, delegate, or array type. |
