
So it would seem that when using generics, you can declare variables of a generic type, perform some variable assignments, call methods defined by **Object**, and that's about it! This makes generics practically useless. Fortunately, compilers and the CLR support a mechanism called *constraints* that you can take advantage of to make generics useful again.

A constraint is a way to limit the number of types that can be specified for a generic argument. Limiting the number of types allows you to do more with those types. Here is a new version of the **Min** method that specifies a constraint (in bold):

```csharp
public static T Min<T>(T o1, T o2) where T : IComparable<T> {
    if (o1.CompareTo(o2) < 0) return o1;
    return o2;
}
```

The C# **where** token tells the compiler that any type specified for T must implement the generic **IComparable** interface of the same type (T). Because of this constraint, the compiler now allows the method to call the **CompareTo** method since this method is defined by the **IComparable<T>** interface.

Now, when code references a generic type or method, the compiler is responsible for ensuring that a type argument that meets the constraints is specified. For example, the following code causes the compiler to issue the following message: 'error CS0311: The type 'object' cannot be used as type parameter 'T' in the generic type or method 'SomeType.Min<T>(T, T)'. There is no implicit reference conversion from 'object' to 'System.IComparable<object>'.'

```csharp
private static void CallMin() {
    Object o1 = "Jeff", o2 = "Richter";
    Object oMin = Min<Object>(o1, o2);   // Error CS0311
}
```

The compiler issues the error because **System.Object** doesn't implement the **IComparable<Object>** interface. In fact, **System.Object** doesn't implement any interfaces at all.

Now that you have a sense of what constraints are and how they work, we'll start to look a little deeper into them. Constraints can be applied to a generic type's type parameters as well as to a generic method's type parameters (as shown in the **Min** method). The CLR doesn't allow overloading based on type parameter names or constraints; you can overload types or methods based only on arity. The following examples show what I mean:

```csharp
// It is OK to define the following types:
internal sealed class AType {}
internal sealed class AType<T> {}
internal sealed class AType<T1, T2> {}

// Error: conflicts with AType<T> that has no constraints
internal sealed class AType<T> where T : IComparable<T> {}
```

## Primary Constraints

A type parameter can specify zero primary constraints or one primary constraint. A primary constraint can be a reference type that identifies a class that is not sealed. You cannot specify one of the following special reference types: **System.Object**, **System.Array**, **System.Delegate**, **System.MulticastDelegate**, **System.ValueType**, **System.Enum**, or **System.Void**.

When specifying a reference type constraint, you are promising the compiler that a specified type argument will either be of the same type or of a type derived from the constraint type. For example, see the following generic class:

```
    internal sealed class PrimaryConstraintOfStream<T> where T : Stream {
        public void M(T stream) {
            stream.Close(); // OK
        }
    }
```

In this class definition, the type parameter T has a primary constraint of **Stream** (defined in the **System.IO** namespace). This tells the compiler that code using **PrimaryConstraintOfStream** must specify a type argument of **Stream** or a type derived from **Stream** (such as **FileStream**). If a type parameter doesn't specify a primary constraint, **System.Object** is assumed. However, the C# compiler issues an error message **"error CS0702: Constraint cannot be special class 'object'"** if you explicitly specify **System.Object** in your source code.

There are two special primary constraints: **class** and **struct**. The **class** constraint promises the compiler that a specified type argument will be a reference type. Any class type, interface type, delegate type, or array type satisfies this constraint. For example, see the following generic class:

```
    internal sealed class PrimaryConstraintOfClass<T> where T : class {
        public void M() {
            T temp = null; // Allowed because T must be a reference type
        }
    }
```

In this example, setting **temp** to **null** is legal because T is known to be a reference type, and all reference type variables can be set to **null**. If T were unconstrained, the code above would not compile because T could be a value type, and value type variables cannot be set to **null**.

The **struct** constraint promises the compiler that a specified type argument will be a value type. Any value type, including enumerations, satisfies this constraint. However, the compiler and the CLR treat any **System.Nullable<T>** value type as a special type, and nullable types do not satisfy this constraint. The reason is because the **Nullable<T>** type constrains its type parameter to **struct**, and the CLR wants to prohibit a recursive type such as Nullable<Nullable<T>>. Nullable types are discussed in Chapter 19, "Nullable Value Types."

Here is an example class that constrains its type parameter by using the **struct** constraint:

```csharp
internal sealed class PrimaryConstraintOfStruct<T> where T : struct {
    public static T Factory() {
        // Allowed because all value types implicitly
        // have a public, parameterless constructor
        return new T();
    }
}
```

In this example, newing up a `T` is legal because `T` is known to be a value type, and all value types implicitly have a public, parameterless constructor. If `T` were unconstrained, constrained to a reference type, or constrained to **class**, the above code would not compile because some reference types do not have public, parameterless constructors.

### Secondary Constraints

A type parameter can specify zero or more secondary constraints where a secondary constraint represents an interface type. When specifying an interface type constraint, you are promising the compiler that a specified type argument will be a type that implements the interface. And since you can specify multiple interface constraints, the type argument must specify a type that implements all of the interface constraints (and all of the primary constraints too, if specified). Chapter 13 discusses interface constraints in detail.

There is another kind of secondary constraint called a *type parameter constraint* (sometimes referred to as a *naked type constraint*). This kind of constraint is used much less often than an interface constraint. It allows a generic type or method to indicate that there must be a relationship between specified type arguments. A type parameter can have zero or more type constraints applied to it. Here is a generic method that demonstrates the use of a type parameter constraint:

```csharp
private static List<TBase> ConvertIList<T, TBase>(IList<T> list)
    where T : TBase {
    List<TBase> baseList = new List<TBase>(list.Count);
    for (Int32 index = 0; index < list.Count; index++) {
        baseList.Add(list[index]);
    }
    return baseList;
}
```

The **ConvertIList** method specifies two type parameters in which the `T` parameter is constrained by the `TBase` type parameter. This means that whatever type argument is specified for `T`, the type argument must be compatible with whatever type argument is specified for `TBase`. Here is a method showing some legal and illegal calls to **ConvertIList**:

```csharp
internal sealed class ConstructorConstraint<T> where T : new() {
    public static T Factory() {
        // Allowed because all value types implicitly
        // have a public, parameterless constructor and because
        // the constraint requires that any specified reference
        // type also have a public, parameterless constructor
        return new T();
    }
}
```

In this example, **newing up a T** is legal because T is known to be a type that has a public, parameterless constructor. This is certainly true of all value types, and the constructor constraint requires that it be true of any reference type specified as a type argument.

Sometimes, developers would like to declare a type parameter by using a constructor constraint whereby the constructor takes various parameters itself. As of now, the CLR (and therefore the C# compiler) supports only parameterless constructors. Microsoft feels that this will be good enough for almost all scenarios, and I agree.

### Other Verifiability Issues

In the remainder of this section, I'd like to point out a few other code constructs that have unexpected behavior when used with generics due to verifiability issues and how constraints can be used to make the code verifiable again.

### Casting a Generic Type Variable

Casting a generic type variable to another type is illegal unless you are casting to a type compatible with a constraint.

```csharp
private static void CastingAGenericTypeVariable1<T>(T obj) {
    Int32 x = (Int32) obj;  // Error
    String s = (String) obj; // Error
}
```

The compiler issues an error on both lines above because T could be any type, and there is no guarantee that the casts will succeed. You can modify this code to get it to compile by casting to **Object** first:

```csharp
private static void CastingAGenericTypeVariable2<T>(T obj) {
    Int32 x = (Int32) (Object) obj;  // No error
    String s = (String) (Object) obj; // No error
}
```

While this code will now compile, it is still possible for the CLR to throw an **InvalidCastException** at runtime.
