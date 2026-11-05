
## 3. Basic Concepts

creation and termination. The execution environment is free to change the order of execution of a C# program, subject to the following constraints:

- Data dependence is preserved within a thread of execution. That is, the value of each variable is computed as if all statements in the thread were executed in original program order.
- Initialization ordering rules are preserved (§10.5.4 and §10.5.5).
- The ordering of side effects is preserved with respect to volatile reads and writes (§10.5.3). Additionally, the execution environment need not evaluate part of an expression if it can deduce that that expression's value is not used and that no needed side effects are produced (including any caused by calling a method or accessing a volatile field). When program execution is interrupted by an asynchronous event (such as an exception thrown by another thread), it is not guaranteed that the observable side effects will be visible in the original program order.

## 4. Types

The types of the C# language are divided into two main categories: *value types* and *reference types*. Both value types and reference types may be *generic types*, which take one or more *type parameters*. Type parameters can designate both value types and reference types.

```
type:
    value-type
    reference-type
    type-parameter
```

A third category of types, pointers, is available only in unsafe code. This issue is discussed further in §18.2.

Value types differ from reference types in that variables of the value types directly contain their data, whereas variables of the reference types store *references* to their data, the latter being known as *objects*. With reference types, it is possible for two variables to reference the same object, and thus possible for operations on one variable to affect the object referenced by the other variable. With value types, the variables each have their own copy of the data, so it is not possible for operations on one to affect the other.

C#'s type system is unified such that *a value of any type can be treated as an object*. Every type in C# directly or indirectly derives from the `object` class type, and `object` is the ultimate base class of all types. Values of reference types are treated as objects simply by viewing the values as type `object`. Values of value types are treated as objects by performing boxing and unboxing operations (§4.3).

> **ERIC LIPPERT** We normally do not think of interface types or the types associated with type parameters as having a “base class” per se. What this discussion is getting at is that every concrete object—no matter how you are treating it at compile time—may be treated as an instance of object at runtime.

### 4.1 Value Types

A value type is either a struct type or an enumeration type. C# provides a set of pre-defined struct types called the *simple types*. The simple types are identified through reserved words.

```
value-type:
    struct-type
    enum-type

struct-type:
    type-name
    simple-type
    nullable-type

simple-type:
    numeric-type
    bool

numeric-type:
    integral-type
    floating-point-type
    decimal

integral-type:
    sbyte
    byte
    short
    ushort
    int
    uint
    long
    ulong
    char

floating-point-type:
    float
    double

nullable-type:
    non-nullable-value-type ?

non-nullable-value-type:
    type

enum-type:
    type-name
```

Unlike a variable of a reference type, a variable of a value type can contain the value `null` only if the value type is a nullable type. For every non-nullable value type, there is a corresponding nullable value type denoting the same set of values plus the value `null`.

Assignment to a variable of a value type creates a *copy* of the value being assigned. This differs from assignment to a variable of a reference type, which copies the reference but not the object identified by the reference.

### 4.1.1 The System.ValueType Type

All value types implicitly inherit from the class `System.ValueType`, which in turn inherits from class `object`. It is not possible for any type to derive from a value type, and value types are thus implicitly sealed (§10.1.2).

Note that `System.ValueType` is not itself a *value-type*. Rather, it is a *class-type* from which all *value-types* are automatically derived.

> **ERIC LIPPERT** This point is frequently confusing to novices. I am often asked, “But how is it possible that a value type derives from a reference type?” I think the confusion arises as a result of a misunderstanding of what “derives from” means. Derivation does not imply that the layout of the bits in memory of the base type is somewhere found in the layout of bits in the derived type. Rather, it simply implies that some mechanism exists whereby members of the base type may be accessed from the derived type.

### 4.1.2 Default Constructors

All value types implicitly declare a public parameterless instance constructor called the *default constructor*. The default constructor returns a zero-initialized instance known as the *default value* for the value type:

- For all *simple-types*, the default value is the value produced by a bit pattern of all zeros:
  - For `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, and `ulong`, the default value is `0`.
  - For `char`, the default value is `'\x0000'`.
  - For `float`, the default value is `0.0f`.
  - For `double`, the default value is `0.0d`.
  - For `decimal`, the default value is `0.0m`.
  - For `bool`, the default value is `false`.
- For an enum-type E, the default value is 0, converted to the type E.
- For a struct-type, the default value is the value produced by setting all value type fields to their default values and all reference type fields to null.

> VLADIMIR RESHETNIKOV Obviously, the wording “all fields” here means only instance fields (not static fields). It also includes field-like instance events, if any exist.

- For a nullable-type, the default value is an instance for which the HasValue property is false and the Value property is undefined. The default value is also known as the null value of the nullable type.

Like any other instance constructor, the default constructor of a value type is invoked using the new operator. For efficiency reasons, this requirement is not intended to actually have the implementation generate a constructor call. In the example below, variables i and j are both initialized to zero.

```csharp
class A
{
    void F() {
        int i = 0;
        int j = new int();
    }
}
```

Because every value type implicitly has a public parameterless instance constructor, it is not possible for a struct type to contain an explicit declaration of a parameterless constructor. A struct type is, however, permitted to declare parameterized instance constructors (§11.3.8).

> ERIC LIPPERT Another good way to obtain the default value of a type is to use the default(type) expression.

> JON SKEET This is one example of where the C# language and the underlying platform may have different ideas. If you ask the .NET platform for the constructors of a value type, you usually won’t find a parameterless one. Instead, .NET has a specific instruction for initializing the default value for a value type. Usually these small impedance mismatches have no effect on developers, but it’s good to know that they’re possible—and that they don’t represent a fault in either specification.

### 4.1.3 Struct Types

A struct type is a value type that can declare constants, fields, methods, properties, indexers, operators, instance constructors, static constructors, and nested types. The declaration of struct types is described in §11.1.

### 4.1.4 Simple Types

C# provides a set of predefined struct types called the *simple types*. The simple types are identified through reserved words, but these reserved words are simply aliases for pre-defined struct types in the System namespace, as described in the table below.

| Reserved Word | Aliased Type |
| --- | --- |
| sbyte | System.SByte |
| byte | System.Byte |
| short | System.Int16 |
| ushort | System.UInt16 |
| int | System.Int32 |
| uint | System.UInt32 |
| long | System.Int64 |
| ulong | System.UInt64 |
| char | System.Char |
| float | System.Single |
| double | System.Double |
| bool | System.Boolean |
| decimal | System.Decimal |

Because a simple type aliases a struct type, every simple type has members. For example, int has the members declared in System.Int32 and the members inherited from System.Object, and the following statements are permitted:

```csharp
int i = int.MaxValue;        // System.Int32.MaxValue constant
string s = i.ToString();     // System.Int32.ToString() instance method
string t = 123.ToString();   // System.Int32.ToString() instance method
```
