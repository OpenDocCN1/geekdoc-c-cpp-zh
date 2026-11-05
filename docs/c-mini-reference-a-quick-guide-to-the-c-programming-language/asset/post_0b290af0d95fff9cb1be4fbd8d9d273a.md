
### 12.2.10. Base class type constraints

```
class C<T> where T : B1 { }
```

The type argument must be, or derive, from the specified base class, e.g., T must be a non-nullable reference type derived from

```
class C<T> where T : B1? { }
```

Likewise, the type argument must be, or derive, from the specified base class, T may be a nullable or non-nullable type.

### 12.2.11. Specific type constraints

```
class C<T, U> where T : U { }
```

The type argument T must be, or derive from, the type U.

If U is a non-nullable reference type, T must be non-nullable reference type.

If U is a nullable reference type, T may be nullable or non-nullable.

## 12.3. Type Variance in Generics

In C#, type variance enables implicit reference conversion for array types, delegate types, and generic type parameters so that broader, or more specific, types can be used. Variances, either covariance or contravariance, are supported for reference types, but they are not supported for value types.

### 12.3.1. Covariance

Covariance enables you to use a more derived type than that specified by the generic parameter. This allows for implicit conversion of classes that implement covariant interfaces and implicit conversion of delegate types. An [interface](#) that has a covariant type parameter enables its methods to return more derived types than those specified by the type parameter.

As an example, because [type T is covariant in IEnumerable](#) and string inherits from an object of the IEnumerable type, for instance, can be implicitly assigned to an object of the IEnumerable
