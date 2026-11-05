```
non-array-type:
    value-type
    class-type
    interface-type
    delegate-type
    dynamic
    type-parameter

rank-specifiers:
    rank-specifier
    rank-specifiers rank-specifier

rank-specifier:
    [ dim-separators_opt ]

dim-separators:
    ,
    dim-separators ,

delegate-type:
    type-name
```

A reference type value is a reference to an instance of the type, the latter known as an *object*. The special value *null* is compatible with all reference types and indicates the absence of an instance.

# 9.2.2 Class types

A class type defines a data structure that contains data members (constants and fields), function members (methods, properties, events, indexers, operators, instance constructors, finalizers, and static constructors), and nested types. Class types support inheritance, a mechanism whereby derived classes can extend and specialize base classes. Instances of class types are created using *object-creation-expressions* (§12.7.11.2).

Class types are described in §15.

Certain predefined class types have special meaning in the C# language, as described in the table below.

| Class type | Description |
|---|---|
| System.Object | The ultimate base class of all other types. See §9.2.3. |
| System.String | The string type of the C# language. See §9.2.5. |
| System.ValueType | The base class of all value types. See 9.3.2. |
| System.Enum | The base class of all enum types. See §19.5. |
| System.Array | The base class of all array types. See §17.2.2. |
| System.Delegate | The base class of all delegate types. See §20.1. |
| System.Exception | The base class of all exception types. See §21.3. |

# 9.2.3 The object type

The *object* class type is the ultimate base class of all other types. Every type in C# directly or indirectly derives from the *object* class type.

The keyword *object* is simply an alias for the predefined class System.Object.

# 9.2.4 The dynamic type

The *dynamic* type, like *object*, can reference any object. When operations are applied to expressions of type *dynamic*, their resolution is deferred until the program is run. Thus, if the operation cannot