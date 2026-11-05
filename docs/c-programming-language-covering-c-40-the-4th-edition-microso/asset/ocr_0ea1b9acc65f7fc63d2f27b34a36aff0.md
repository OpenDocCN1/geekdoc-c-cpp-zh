# 4. Types

Certain predefined class types have special meaning in the C# language, as described in the table below.

| Class Type | Description |
|---|---|
| `System.Object` | The ultimate base class of all other types. (See §4.2.2.) |
| `System.String` | The string type of the C# language. (See §4.2.3.) |
| `System.ValueType` | The base class of all value types. (See §4.1.1.) |
| `System.Enum` | The base class of all enum types. (See §14.) |
| `System.Array` | The base class of all array types. (See §12.) |
| `System.Delegate` | The base class of all delegate types. (See §15.) |
| `System.Exception` | The base class of all exception types. (See §16.) |

# 4.2.2  The object Type

The object class type is the ultimate base class of all other types. Every type in C# directly or indirectly derives from the object class type.

The keyword object is simply an alias for the predefined class System.Object.

# 4.2.3  The dynamic Type

The dynamic type, like object, can reference any object. When operators are applied to expressions of type dynamic, their resolution is deferred until the program is run. Thus, if the operator cannot legally be applied to the referenced object, no error is given during compilation. Instead, an exception will be thrown when resolution of the operator fails at runtime.

The dynamic type is further described in §4.7, and dynamic binding in §7.2.2.

# 4.2.4  The string Type

The string type is a sealed class type that inherits directly from object. Instances of the string class represent Unicode character strings.

Values of the string type can be written as string literals (§2.4.4.5).

The keyword string is simply an alias for the predefined class System.String.