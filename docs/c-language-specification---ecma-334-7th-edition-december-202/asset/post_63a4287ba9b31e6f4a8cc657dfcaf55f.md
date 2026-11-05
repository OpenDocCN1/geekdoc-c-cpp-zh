
```csharp
    public static long F(T t)
    {
        return (long)t;            // Error
    }
```

If the direct explicit conversion of t to long were permitted, one might easily expect that `X<int>.F(7)` would return 7L. However, it would not, because the standard numeric conversions are only considered when the types are known to be numeric at binding-time. In order to make the semantics clear, the above example must instead be written:

```csharp
class X<T>
{
    public static long F(T t)
    {
        return (long)(object)t;        // Ok, but will only work when T is long
    }
}
```

This code will now compile but executing `X<int>.F(7)` would then throw an exception at run-time, since a boxed int cannot be converted directly to a long.

*end example*

### 10.3.10 User-defined explicit conversions

A user-defined explicit conversion consists of an optional standard explicit conversion, followed by execution of a user-defined implicit or explicit conversion operator, followed by another optional standard explicit conversion. The exact rules for evaluating user-defined explicit conversions are described in §10.5.5.

## 10.4 Standard conversions

### 10.4.1 General

The standard conversions are those pre-defined conversions that can occur as part of a user-defined conversion.

### 10.4.2 Standard implicit conversions

The following implicit conversions are classified as standard implicit conversions:

- Identity conversions (§10.2.2)
- Implicit numeric conversions (§10.2.3)
- Implicit nullable conversions (§10.2.6)
- Null literal conversions (§10.2.7)
- Implicit reference conversions (§10.2.8)
- Boxing conversions (§10.2.9)
- Implicit constant expression conversions (§10.2.11)
- Implicit conversions involving type parameters (§10.2.12)

The standard implicit conversions specifically exclude user-defined implicit conversions.

### 10.4.3 Standard explicit conversions

The standard explicit conversions are all standard implicit conversions plus the subset of the explicit conversions for which an opposite standard implicit conversion exists.

> Note: In other words, if a standard implicit conversion exists from a type A to a type B, then a standard explicit conversion exists from type A to type B and from type B to type A. end note

## 10.5 User-defined conversions

### 10.5.1 General

C# allows the pre-defined implicit and explicit conversions to be augmented by user-defined conversions. User-defined conversions are introduced by declaring conversion operators (§15.10.4) in class and struct types.

### 10.5.2 Permitted user-defined conversions

C# permits only certain user-defined conversions to be declared. In particular, it is not possible to redefine an already existing implicit or explicit conversion.

For a given source type S and target type T, if S or T are nullable value types, let S₀ and T₀ refer to their underlying types, otherwise S₀ and T₀ are equal to S and T respectively. A class or struct is permitted to declare a conversion from a source type S to a target type T only if all of the following are true:

- S₀ and T₀ are different types.
- Either S₀ or T₀ is the class or struct type in which the operator declaration takes place.
- Neither S₀ nor T₀ is an interface type.
- Excluding user-defined conversions, a conversion does not exist from S to T or from T to S.

The restrictions that apply to user-defined conversions are specified in §15.10.4.

### 10.5.3 Evaluation of user-defined conversions

A user-defined conversion converts a source expression, which may have a source type, to another type, called the target type. Evaluation of a user-defined conversion centers on finding the most-specific user-defined conversion operator for the source expression and target type. This determination is broken into several steps:

- Finding the set of classes and structs from which user-defined conversion operators will be considered. This set consists of the source type and its base classes, if the source type exists, along with the target type and its base classes. For this purpose it is assumed that only classes and structs can declare user-defined operators, and that non-class types have no base classes. Also, if either the source or target type is a nullable-value-type, their underlying type is used instead.
- From that set of types, determining which user-defined and lifted conversion operators are applicable. For a conversion operator to be applicable, it shall be possible to perform a standard conversion (§10.4) from the source expression to the operand type of the operator, and it shall be possible to perform a standard conversion from the result type of the operator to the target type.
- From the set of applicable user-defined operators, determining which operator is unambiguously the most-specific. In general terms, the most-specific operator is the operator whose operand type is "closest" to the source expression and whose result type is "closest" to the target type. User-defined conversion operators are preferred over lifted conversion operators. The exact rules for establishing the most-specific user-defined conversion operator are defined in the following subclauses.

Once a most-specific user-defined conversion operator has been identified, the actual execution of the user-defined conversion involves up to three steps:

- First, if required, performing a standard conversion from the source expression to the operand type of the user-defined or lifted conversion operator.
- Next, invoking the user-defined or lifted conversion operator to perform the conversion.
- Finally, if required, performing a standard conversion from the result type of the user-defined conversion operator to the target type.

Evaluation of a user-defined conversion never involves more than one user-defined or lifted conversion operator. In other words, a conversion from type S to type T will never first execute a user-defined conversion from S to X and then execute a user-defined conversion from X to T.

- Exact definitions of evaluation of user-defined implicit or explicit conversions are given in the following subclauses. The definitions make use of the following terms:
  - If a standard implicit conversion (§10.4.2) exists from a type A to a type B, and if neither A nor B are interface types, then A is said to be encompassed by B, and B is said to encompass A.
  - If a standard implicit conversion (§10.4.2) exists from an expression E to a type B, and if neither B nor the type of E (if it has one) are interface types, then E is said to be encompassed by B, and B is said to encompass E.
  - The most-encompassing type in a set of types is the one type that encompasses all other types in the set. If no single type encompasses all other types, then the set has no most-encompassing type. In more intuitive terms, the most-encompassing type is the "largest" type in the set—the one type to which each of the other types can be implicitly converted.
  - The most-encompassed type in a set of types is the one type that is encompassed by all other types in the set. If no single type is encompassed by all other types, then the set has no most-encompassed type. In more intuitive terms, the most-encompassed type is the "smallest" type in the set—the one type that can be implicitly converted to each of the other types.

### 10.5.4 User-defined implicit conversions

A user-defined implicit conversion from an expression E to a type T is processed as follows:

- Determine the types S₀ and T₀ and Tₑ.
  - If E has a type, let S be that type.
  - If S or T are nullable value types, let S₁ and T₁ be their underlying types, otherwise let S₁ and T₁ be S and T, respectively.
  - If S₁ or T₁ are type parameters, let S₀ and T₀ be their effective base classes, otherwise let S₀ and T₀ be S₁ and T₁, respectively.
- Find the set of types, D, from which user-defined conversion operators will be considered. This set consists of S₀ (if S₀ exists and is a class or struct), the base classes of S₀ (if S₀ exists and is a class),
