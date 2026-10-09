
In addition, extension methods have the following restrictions:

- The `out` keyword cannot be used on the first argument of an extension method.
- The `ref` keyword cannot be used on the first argument of an extension method when the argument is not a struct, or a generic type not constrained to be a struct.
- The `in` keyword cannot be used unless the first argument is a struct. The `in` keyword cannot be used on any generic type, even when constrained to be a struct.

## Declaring out parameters

Declaring a method with `out` arguments is a classic workaround to return multiple values. One can use value tuples in similar scenarios.

## Calling a method with an out argument

In C# 6 and earlier, you must declare a variable in a separate statement before you pass it as an `out` argument.

You can declare the `out` variable in the argument list of the method call, rather than in a separate variable declaration. This produces more compact, readable code, and also prevents you from inadvertently assigning a value to the variable before the method call.

## Override Modifier (override)

The `override` modifier is required to extend or modify the abstract or virtual implementation of an inherited method, property, indexer, or event.

An `override` method provides a new implementation of the method inherited from a base class. The method that is overridden by an `override` declaration is known as the overridden base method. An `override` method must have the same signature as the overridden base method.

`override` methods support covariant return types. In particular, the return type of an `override` method can derive from the return type of the corresponding base method.

You cannot override a non-virtual or static method. The overridden base method must be `virtual`, `abstract`, or `override`.

An `override` declaration cannot change the accessibility of the virtual method. Both the `override` method and the virtual method must have the same access level modifier.

You cannot use the `new`, `static`, or `virtual` modifiers to modify an `override` method.

An overriding property declaration must specify exactly the same access modifier, type, and name as the inherited property. Read-only overriding properties support covariant return types. The overridden property must be `virtual`, `abstract`, or `override`.

## Params Keyword (params)

By using the `params` keyword, you can specify a method parameter that takes a variable number of arguments. The parameter type must be a single-dimensional array.

No additional parameters are permitted after the `params` keyword in a method declaration, and only one `params` keyword is permitted in a method declaration.

If the declared type of the `params` parameter is not a single-dimensional array, a compiler error occurs.

When you call a method with a `params` parameter, you can pass in:

- A comma-separated list of arguments of the type of the array elements.
- An array of arguments of the specified type.
- No arguments. If you send no arguments, the length of the `params` list is zero.

## Private Access Modifier (private)

The `private` keyword is a member access modifier.

Private access is the least permissive access level. Private members are accessible only within the body of the class or the struct in which they are declared, as in this example:

```cpp
class Employee
{
    private int i;
    double d;   // private access by default
}
```

Nested types in the same body can also access those private members.

It is a compile-time error to reference a private member outside the class or the struct in which it is declared.

## Protected Access Modifier (protected)

The `protected` keyword is a member access modifier.

A protected member is accessible within its class and by derived class instances.

## Public Access Modifier (public)

The `public` keyword is an access modifier for types and type members. Public access is the most permissive access level. There are no restrictions on accessing public members, as in this example:

```
class SampleClass
{
    public int x; // No access restrictions.
}
```

## Readonly Modifier (readonly)

The `readonly` keyword is a modifier that can be used in four contexts:

- In a field declaration, `readonly` indicates that assignment to the field can only occur as part of the declaration or in a constructor in the same class. A `readonly` field can be assigned and reassigned multiple times within the field declaration and constructor.
- A `readonly` field can't be assigned after the constructor exits. This rule has different implications for value types and reference types:
  - Because value types directly contain their data, a field that is a `readonly` value type is immutable.
  - Because reference types contain a reference to their data, a field that is a `readonly` reference type must always refer to the same object. That object isn't immutable. The `readonly` modifier prevents the field from being replaced by a different instance of the reference type. However, the modifier doesn't prevent the instance data of the field from being modified through the read-only field.
- In a `readonly struct` type definition, `readonly` indicates that the structure type is immutable.
- In an instance member declaration within a structure type, `readonly` indicates that an instance member doesn't modify the state of the structure.
- In a `ref readonly` method return, the `readonly` modifier indicates that method returns a reference and writes aren't allowed to that reference.

You can assign a value to a `readonly` field only in the following contexts:

- When the variable is initialized in the declaration, for example:
  ```
  public readonly int y = 5;
  ```
- In an instance constructor of the class that contains the instance field declaration.
- In the static constructor of the class that contains the static field declaration.

These constructor contexts are also the only contexts in which it's valid to pass a readonly field as an `out` or `ref` parameter.

### Ref readonly return example

The `readonly` modifier on a `ref` return indicates that the returned reference can't be modified.

The type returned doesn't need to be a `readonly` struct. Any type that can be returned by `ref` can be returned by `ref readonly`.

## Ref Parameter Modifier (ref)

The `ref` keyword indicates a value that is passed by reference. It is used in four different contexts:

- In a method signature and in a method call, to pass an argument to a method by reference.
- In a method signature, to return a value to the caller by reference.
- In a member body, to indicate that a reference return value is stored locally as a reference that the caller intends to modify or, in general, a local variable accesses another value by reference.
- In a struct declaration to declare a `ref struct` or a `readonly ref struct`.

### Passing an argument by reference

When used in a method's parameter list, the `ref` keyword indicates that an argument is passed by reference, not by value. The `ref` keyword makes the formal parameter an alias for the argument, which must be a variable. In other words, any operation on the parameter is made on the argument. For example, if the caller passes a local variable expression or an array element access expression, and the called method replaces the object to which the `ref` parameter refers, then the caller's local variable or the array element now refers to the new object when the method returns.

> Do not confuse the concept of passing by reference with the concept of reference types. The two concepts are not the same. A method parameter can be modified by `ref` regardless of whether it is a value type or a reference type. There is no boxing of a value type when it is passed by reference.

To use a `ref` parameter, both the method definition and the calling method must explicitly use the `ref` keyword.

An argument that is passed to a `ref` or `in` parameter must be initialized before it is passed. This differs from `out` parameters, whose arguments do not have to be explicitly initialized before they are passed.

Members of a class can't have signatures that differ only by `ref`, `in`, or `out`. A compiler error occurs if the only difference between two members of a type is that one of them has a `ref` parameter and the other has an `out`, or `in` parameter. The following code, for example, doesn't compile.

```
class CS0663_Example
{
    // Compiler error CS0663: "Cannot define overloaded
    // methods that differ only on ref and out".
    public void SampleMethod(out int i) { }
    public void SampleMethod(ref int i) { }
}
```
