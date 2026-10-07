```
// ...
public static implicit operator Nullable<T>(T value) => new(value);
public static explicit operator T(Nullable<T> value) => value!.Value;
// ...
```

Note that the class constraint restricts the type parameter to reference types including interface, delegate, or array types (and, not, as the keyword might seem to imply, only class types).

In C# 8.0, a class constraint defaults to not nullable (assuming, of course, that nullable reference types are enabled). Specifying a nullable reference type parameter will trigger a warning by the compiler. You can change the generic type to allow nullable reference types by including the nullable modifier on the class constraint. Consider the WeakReference<T> class introduced in Chapter 10. Since only reference types are garbage collected, this type includes the class constraint as follows:

```
public sealed partial class WeakReference<T> : ISerializable
{ ... }
```

This restricts the type parameter, T, to be a reference type—which may be nullable.

In contrast to the class constraint, the struct constraint does not allow the nullable modifier. Instead, you can specify nullability when using the parameter. In Listing 12.25, for example, the implicit and explicit conversion operators, for example, use T and T? to identify whether a non-nullable or nullable version of T is allowed. As such, the type parameter is constrained when it is used in member declarations, rather than with a type constraint.

Because a class constraint requires a reference type, using a struct constraint with a class type would be contradictory. Therefore, you cannot combine struct and class constraints.

The struct constraint has one special characteristic: Nullable value types do not satisfy the constraint. Why? Nullable value types are implemented as the generic type Nullable<T>, which itself applies the struct constraint to T. If nullable value types satisfied thatatraint, it would be possible to define the nonsense type