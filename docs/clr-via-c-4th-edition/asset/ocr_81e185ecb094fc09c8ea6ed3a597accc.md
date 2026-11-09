every type supports assignment and calls to methods defined by Object (such as ToString and Equals).

Now look at the following method.

```
```csharp
private static T Min<T>(T o1, T o2) {
    if (o1.CompareTo(o2) < 0) return o1;
    return o2;
}
```
```

The Min method attempts to use the o1 variable to call the CompareTo method. But there are lots of types that do not offer a CompareTo method, and therefore, the C# compiler can't compile this code and guarantee that this method would work for all types. If you attempt to compile the above code, the compiler issues the following message: error CS1061: 'T' does not contain a definition for 'CompareTo' accepting a first argument of type 'T' could be found (are you missing a using directive or an assembly reference?)

So it would seem that when using generics, you can declare variables of a generic type, perform some variable assignments, call methods defined by Object, and that's about it! This makes generics practically useless. Fortunately, compilers and the CLR support a mechanism called constraints that you can take advantage of to make generics useful again.

A constraint is a way to limit the number of types that can be specified for a generic argument. Limiting the number of types allows you to do more with those types. Here is a new version of the Min method that specifies a constraint (in bold).

```
```csharp
public static T Min<T>(T o1, T o2) where T : IComparable<T> {
    if (o1.CompareTo(o2) < 0) return o1;
    return o2;
}
```
```

The C# where token tells the compiler that any type specified for T must implement the generic IComparable interface of the same type (T). Because of this constraint, the compiler now allows the method to call the CompareTo method because this method is defined by the IComparable<T> interface.

Now, when code references a generic type or method, the compiler is responsible for ensuring that a type argument that meets the constraints is specified. For example, the following code causes the compiler to issue the following message: error CS0311: The type 'object' cannot be used as type parameter 'T' in the generic type or method 'SomeType.Min<T>(T, T)'. There is no implicit reference conversion from 'object' to 'System.IComparable<object>'.

```
```csharp
private static void CallMin() {
    Object o1 = "Jeff", o2 = "Richter";
    Object oMin = Min<Object>(o1, o2);   // Error CS0311
}
```
```

The compiler issues the error because System.Object doesn't implement the IComparable<Object> interface. In fact, System.Object doesn't implement any interfaces at all.