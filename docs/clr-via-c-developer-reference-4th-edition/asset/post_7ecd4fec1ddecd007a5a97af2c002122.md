
In this example, setting type to null is legal because T is known to be a reference type, and all reference type variables can be null. If T were unconstrained, the preceding code would not compile because T could be a value type, and value type variables cannot be null.

The struct constraint promises that a specified type argument will be a value type. Any value type, including enumerations, satisfies this constraint. However, the compiler and the CLR treat System.Nullable<T> as a value type, and nullable types do not satisfy this constraint. The reason is that Nullable<T> constraints its type parameter to struct, and the CLR wants to prohibit recursive type as Nullable<Nullable<T>>. Nullable types are discussed in Chapter 19, "Nullable Value Types".

Here is an example that constrains its type parameter by the struct constraint.

```
internal sealed class PrimaryConstraintOf<T> where T : struct {
    public static T Factory() {
        // Because all value types implicitly
        // have a public, parameterless constructor
        return new T();
    }
}
```

In this example, new up T is legal because T is known to be a value type, and all value types implicitly have a public, parameterless constructor. If T were unconstrained, a reference type, or constrained to class, the above code would not compile because some reference types do not have public, parameterless constructors.

## Secondary Constraints

A type parameter can specify zero or more secondary constraints where a secondary constraint represents an interface type. When specifying an interface constraint, you are promising the compiler that the specified argument will be a type that implements the interface. Because you can specify multiple interface constraints, the type parameter must specify a type that implements all of the interface constraints (and all of the primary constraints too, if specified). Chapter 13 discusses interface constraints in detail.

Another kind of secondary constraint is called a type parameter constraint (sometimes referred to as a native constraint). This kind of constraint is used much less often than an interface constraint. It allows a generic type to indicate that there must be a relationship between specified types. A type parameter can have zero or more type constraints applied to it. Here is a generic method that demonstrates the use of a type parameter constraint.

```
private static List<TBase> ConvertIList<T, TBase>(IList<T> list)
where T : TBase {
    List<TBase> baseList = new List<TBase>(list.Count);
    for (Int32 index = 0; index < list.Count; index++) {
        baseList.Add(list[index]);
    }
    return baseList;
}
```

The ConvertList method specifies two type parameters in which the T parameter is constrained by the TBase type parameter. This means whatever type argument is specified for T, the type argument must be compatible with whatever type argument is specified for TBase. There is a method showing legal and illegal calls to ConvertList.

```
private static void CallingConvertList() {
// Construct and initialize a List<String> (which implements IList<String>)
List<String> ls = new List<String>();
ls.Add("A String");

// Convert the List<String> to an IList<Object>
IList<Object> lo = ConvertList<String, Object>(ls);

// Convert the List<String> to an IList<IComparable>
IList<IComparable> lc = ConvertList<String, IComparable>(ls);

// Convert the List<String> to an IList<IComparable<String>>
IList<IComparable<String>> lcs = ConvertList<String, IComparable<String>>(ls);

// Convert the List<String> to an IList<String>
IList<String> ls2 = ConvertList<String, String>(ls);

// Convert the List to an IList<Exception>// Error
IList<Exception> le = ConvertList<String, Exception>(ls);
}
```

In the first call to ConvertList, the compiler ensures that String is compatible with Object. Because String is derived from Object, the first call adheres to the type constraint. The second call to ConvertList, the compiler ensures that String is compatible with IComparable. Because String implements the IComparable interface, the second call adheres to the type parameter constraint. In the third call to ConvertList, the compiler ensures that String is compatible with IComparable<String>. Because String implements the IComparable<String> interface, the fourth call adheres to the type parameter constraint. The compiler knows that String is compatible with itself. In the fifth call to ConvertList, the compiler ensures that String is compatible with Exception. Because String is not compatible with Exception, the compiler issues the following message: Error CS0311: The type 'string' cannot be used as type parameter 'T' in the generic type or method Program.ConvertList<T,TBase>(System.Collections.Generic.IList<T>). There is no implicit reference conversion from 'string' to 'System.Exception'.

## Constructor Constraints

A type parameter can specify zero constructor constraints or one constructor constraint. By specifying a constructor constraint, you are promising the compiler that the specified type will be a non-abstract type that implements a public, parameterless constructor. Note that the C# compiler considers it an error to specify a constructor constraint with the struct constraint because it is redundant; all value types implicitly offer a public, parameterless constructor. Here is an example class that constrains its type parameter using the constructor constraint.

```
internal sealed class ConstructorConstraint<T> where T : new() {
    public static T Factory() {
        // Allowed because all value types implicitly
        // a public, parameterless constructor and because
        // the constraint requires that any specified reference
        // type also have a public, parameterless constructor
        return new T();
    }
}
```

In this example, new up T is legal because T is known to be a value type, and all value types implicitly have a public, parameterless constructor. If T were unconstrained, a reference type, or constrained to class, the above code would not compile because some reference types do not have public, parameterless constructors.
