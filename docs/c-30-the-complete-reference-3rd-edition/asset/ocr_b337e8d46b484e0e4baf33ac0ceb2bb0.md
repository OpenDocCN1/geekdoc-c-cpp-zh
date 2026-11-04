# ### Using Explicit Type Arguments to Call a Generic Method

Although implicit type inference is adequate for most invocations of a generic method, it is possible to explicitly specify the type argument. To do so, specify the type argument after the method name when calling the method. For example, here `CopyInsert()` is explicitly passed type `string`:

```
```csharp
ArrayUtils.CopyInsert<string>("in C#", 1, strs, strs2);
```
```

You will need to explicitly specify the type when the compiler cannot infer the type for the `T` parameter or if you want to override the type inference.

# ### Using a Constraint with a Generic Method

You can add constraints to the type arguments of a generic method by specifying them after the parameter list. For example, the following version of `CopyInsert()` will work only with reference types:

```
```csharp
public static bool CopyInsert<T>(T e, uint idx,
                      T[] src, T[] target) where T : class {
```
```

If you were to try this version in the program shown earlier, then the following call to `CopyInsert()` would not compile because `int` is a value type, not a reference type:

```
```csharp
// Now wrong because T must be reference type!
ArrayUtils.CopyInsert(99, 2, nums, nums2); // Now illegal!
```
```

# ## Generic Delegates

Like methods, delegates can also be generic. To declare a generic delegate, use this general form:

```
```csharp
delegate ret-type delegate-name<type-parameter-list>(arg-list);
```
```

Notice the placement of the type parameter list. It immediately follows the delegate's name. The advantage of generic delegates is that they let you define, in a type-safe manner, a generalized form that can then be matched to any compatible method.

The following program demonstrates a generic delegate called `SomeOp` that has one type parameter called `T`. It returns type `T` and takes an argument of type `T`.

```
```csharp
// A simple generic delegate.

using System;

// Declare a generic delegate.
delegate T SomeOp<T>(T v);

class GenDelegateDemo {
    // Return the summation of the argument.
    static int Sum(int v) {
        int result = 0;
        for(int i=v; i>0; i--)
```
```