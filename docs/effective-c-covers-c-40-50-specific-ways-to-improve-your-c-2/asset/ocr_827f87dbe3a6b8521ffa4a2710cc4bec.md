# Item 2: Prefer readonly to const

C# has two different versions of constants: compile-time constants and runtime constants. They have very different behaviors, and using the wrong one will cost you performance or correctness. Neither problem is a good one to have, but if you must pick one, a slower, correct program is better than a faster, broken program. For that reason, you should prefer runtime constants over compile-time constants. Compile-time constants are slightly faster, but far less flexible, than runtime constants. Reserve the compile-time constants for when performance is critical and the value of the constant will never change between releases.

You declare runtime constants with the readonly keyword. Compile-time constants are declared with the const keyword:

```
// Compile time constant:
public const int Millennium = 2000;
```

```
// Runtime constant:
public static readonly int ThisYear = 2004;
```

The code above shows both kinds of constants at the class or struct scope. Compile-time constants can also be declared inside methods. Read-only constants cannot be declared with method scope.

The differences in the behavior of compile-time and runtime constants follow from how they are accessed. A compile-time constant is replaced with the value of that constant in your object code. This construct:

```
if (myDateTime.Year == Millennium)
```

compiles to the same IL as if you had written this:

```
if (myDateTime.Year == 2000)
```

Runtime constants are evaluated at runtime. The IL generated when you reference a read-only constant references the readonly variable, not the value.

This distinction places several restrictions on when you are allowed to use either type of constant. Compile-time constants can be used only for primitive types (built-in integral and floating-point types), enums, or strings. These are the only types that enable you to assign meaningful constant values in initializers. These primitive types are the only ones that can be