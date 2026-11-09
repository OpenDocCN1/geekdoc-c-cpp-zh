
- The System.TypeInfo type offers the following instance members: DeclaredNestedTypes and GetDeclaredNestedType.
- The System.Reflection.Assembly type offers the following instance members: GetType, DefinedTypes, and ExportedTypes.

> **Note** Microsoft has defined a Backus-Naur Form grammar for type names and assembly-qualified type names that is used for constructing strings that will be passed to reflection methods. Knowledge of the grammar can come in quite handy when you are using reflection, specifically if you are working with nested types, generic types, generic methods, reference parameters, or arrays. For the complete grammar, see the FCL documentation or do a web search for "Backus-Naur Form Grammar for Type Names." You can also look at Type's and TypeInfo's MakeArrayType, MakeByRefType, MakeGenericType, and MakePointerType methods.

Many programming languages also offer an operator that allows you to obtain a Type object from a type name that is known at compile time. When possible, you should use this operator to obtain a reference to a Type instead of using any of the methods in the preceding list, because the operator generally produces faster code. In C#, the operator is called typeof, and you use this operator typically to compare late-bound type information with early-bound (known at compile time) type information. The following code demonstrates an example of its use.

```
    private static void SomeMethod(Object o) {
        // GetType returns the type of the object at runtime (late-bound)
        // typeof returns the type of the specified class (early-bound)
        if (o.GetType() == typeof(FileInfo)) { ... }
        if (o.GetType() == typeof(DirectoryInfo)) { ... }
    }
```

> **Note** The first if statement in the code checks whether the variable o refers to an object of the FileInfo type; it does not check whether o refers to an object that is derived from the FileInfo type. In other words, the preceding code tests for an exact match, not a compatible match, which is what you would get if you use a cast or C#'s is or as operators.

As mentioned earlier, a Type object represents a type reference that is a lightweight object. If you want to learn more about the type itself, then you must acquire a TypeInfo object, which represents a type definition. You can convert a Type object to a TypeInfo object by calling System.Reflection.IntrospectionExtensions' GetTypeInfo extension method.

```
    Type typeReference = ...;  // For example: o.GetType() or typeof(Object)
    TypeInfo typeDefinition = typeReference.GetTypeInfo();
```

type. Second, these methods allow you to construct a remote object if you have remoting options configured properly. Third, these versions don't return a reference to the new object. Instead, they return a `System.Runtime.Remoting.ObjectHandle` (which is derived from `System.MarshalByRefObject`).

An `ObjectHandle` is a type that allows an object created in one AppDomain to be passed around to other AppDomains without forcing the object to materialize. When you're ready to materialize the object, you call `ObjectHandle`'s `Unwrap` method. This method loads the assembly that defines the type being materialized in the AppDomain where `Unwrap` is called. If the object is being marshaled by reference, the proxy type and object are created. If the object is being marshaled by value, the copy is deserialized.

- **`System.Activator`'s `CreateInstanceFrom` methods** The `Activator` class also offers a set of static `CreateInstanceFrom` methods. These methods behave just as the `CreateInstance` method, except that you must always specify the type and its assembly via string parameters. The assembly is loaded into the calling AppDomain by using `Assembly`'s `LoadFrom` method (instead of `Load`). Because none of these methods takes a `Type` parameter, all of the `CreateInstanceFrom` methods return a reference to an `ObjectHandle`, which must be unwrapped.

- **`System.AppDomain`'s methods** The `AppDomain` type offers four instance methods (each with several overloads) that construct an instance of a type: `CreateInstance`, `CreateInstanceAndUnwrap`, `CreateInstanceFrom`, and `CreateInstanceFromAndUnwrap`. These methods work just as `Activator`'s methods except that these methods are instance methods, allowing you to specify which `AppDomain` the object should be constructed in. The methods that end with `Unwrap` exist for convenience so that you don't have to make an additional method call.

- **`System.Reflection.ConstructorInfo`'s `Invoke` instance method** Using a reference to a `TypeInfo` object, you can bind to a particular constructor and obtain a reference to the constructor's `ConstructorInfo` object. Then you can use the reference to the `ConstructorInfo` object to call its `Invoke` method. The type is always created in the calling AppDomain, and a reference to the new object is returned. I'll also discuss this method in more detail later in this chapter.

> **Note** The CLR doesn't require that value types define any constructors. However, this is a problem because all of the mechanisms in the preceding list construct an object by calling its constructor. However, `Activator`'s `CreateInstance` methods will allow you to create an instance of a value type without calling a constructor. If you want to create an instance of a value type without calling a constructor, you must call the version of the `CreateInstance` method that takes a single `Type` parameter or the version that takes `Type` and `Boolean` parameters.

The mechanisms just listed allow you to create an object for all types except for arrays (System.Array-derived types) and delegates (System.MulticastDelegate-derived types). To create an array, you should call Array's static CreateInstance method (several overloaded versions exist). The first parameter to all versions of CreateInstance is a reference to the Type of elements you want in the array. CreateInstance's other parameters allow you to specify various combinations of dimensions and bounds. To create a delegate, you should call MethodInfo's CreateDelegate method. The first parameter to all versions of CreateDelegate is a reference to the Type of delegate you want to create. CreateDelegate's other parameter allows you to specify which object should be passed as the this parameter when calling an instance method.

To construct an instance of a generic type, first get a reference to the open type, and then call Type's MakeGenericType method, passing in an array of types that you want to use as the type arguments. Then, take the returned Type object and pass it into one of the various methods previously listed. Here is an example.

```csharp
using System;
using System.Reflection;

internal sealed class Dictionary<TKey, TValue> { }

public static class Program {
    public static void Main() {
        // Get a reference to the generic type's type object
        Type openType = typeof(Dictionary<,>);

        // Close the generic type by using TKey=String, TValue=Int32
        Type closedType = openType.MakeGenericType(typeof(String), typeof(Int32));

        // Construct an instance of the closed type
        Object o = Activator.CreateInstance(closedType);

        // Prove it worked
        Console.WriteLine(o.GetType());
    }
}
```

If you compile the preceding code and run it, you get the following output.

```
Dictionary`2[System.String,System.Int32]
```

## Designing an Application That Supports Add-Ins

When you're building extensible applications, interfaces should be the centerpiece. You could use a base class instead of an interface, but in general, an interface is preferred because it allows add-in developers to choose their own base class. Suppose, for example, that you're writing an application and you want others to be able to create types that your application can load and use seamlessly.
