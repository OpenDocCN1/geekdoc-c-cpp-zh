
### 4.3.2. The using static directive

A using static directive imports the nested types and static members of a type so that the names of the members and types can be used without qualification.

```csharp
using static TYPE_NAME;
```

For example,

```csharp
namespace Arithmetic {
    public class Adder {
        public static void Add(int a, int b) => a + b;
    }
}
namespace App {
    using static Arithmetic.Adder;
    class Calculator {
        public int Sum(int a, int b) => Add(a, b);
    }
}
```

### 4.3.3. The using alias directive

A using alias directive introduces an identifier, or an alias, for a namespace or type within the innermost containing namespace (or, within the compilation unit). The identifiers introduced by the using alias directive can be used to reference the given namespace or type.

```csharp
using IDENTIFIER = NAMESPACE_OR_TYPE_NAME ;
```

For instance,

```csharp
namespace Europe.Ukraine {
    public class Citizen ()
}
namespace World {
    using Person = Europe.Ukraine.Citizen;
    class Farmer: Person ()
}
```

## 4.4. Global using

The using declarations can be made effective across an entire program, using the keyword global. The global using declarations can be used for any of the three using declaration types, using namespace, using static and using alias. But, global using can only be used in a compilation unit, but not within an explicitly declared namespace, and its scope extends over the entire program. For example,

```csharp
global using Machine;
global using static Robot.Arm;
global using Orange = Modern.Black;
```

## 4.5. Implicit using

Starting with C# 10, one can automatically add common global using directives for the C# project you are building, using the implicit usings feature. The "implicit" aspect refers to the fact that the global using directives are added to a generated file in the project’s obj directory.

In case of the for example, the following namespaces are implicitly declared with global

- System
- System.Collections.Generic
- System.IO
- System.Linq
- System.Net.Http
- System.Threading
- System.Threading.Tasks

## 4.6. Member Declarations

As indicated before, as of C# 9 and later, top-level statements can be used in one of the source code files in a program in lieu of a type that includes the Main method, e.g., as an entry point to the program. With this exception (which is merely a syntactic sugar), all statements in a namespace (explicitly declared or otherwise) must be either other (nested) namespace declarations or type declarations.

A type declaration is

- A class declaration,
- A struct declaration,
- A record declaration,
- An enum declaration,
- An interface declaration, or
- A delegate declaration.

Access to these namespace top-level type declarations can be explicitly controlled using the access modifier. Otherwise, their default access level is

## 5. C# Type System

C#, and .NET, has a unified type system. Every type in the C# language inherits, either directly or indirectly, from the object base type on .NET).

The types in C# are divided into two main categories, reference types and value types. Variables of the value types may directly contain their data, whereas variables of the reference types store references to their data. Values of reference types are treated as objects simply by viewing the values as type object. On the other hand, values of value types are treated as objects by performing boxing and unboxing operations.

Generic types are discussed later. Generic type parameters can designate either a value type or a reference type.

### 5.1. Value Types

C#'s value types can be divided into simple, enum, struct types (including record structs), and nullable types. Simple types comprise the builtin bool type and other numeric types. Nullable value types can contain a null value.

By default, when assigning a value, passing an argument to a method, or returning a method result, the values are copied. Note, however, that if a value type contains a data member of a reference type, the reference to the instance of the reference type is copied.

### 5.1.1. The System.ValueType type

A value type cannot explicitly derive from other types. All value types implicitly inherit from the class which itself is not a value type. in turn, inherits from the ultimate base class,

### 5.1.2. Default constructors

All value types implicitly declare a public parameterless instance constructor called the default constructor. The default constructor returns a zero-initialized instance known as the type’s default value

### 5.1.3. Boxing and Unboxing

Through boxing and unboxing, a value of any type, value type or reference type, can be treated as an object. This provides a unified view of the C# type system. Boxing a value of a value type creates an object on the heap, which can be referenced via a reference variable. Unboxing does the reverse operation. That is, it returns the value contained in the object referenced by the given variable.

### 5.1.4. Nullable value types

A nullable value type T? can represent a null value in addition to all values of its underlying (non-nullable) value type. This syntax T? is shorthand for the generic System.Nullable struct. For example, you can assign any of the following three values to a bool? variable: or An instance of a nullable value type T? has two public readonly properties:

```csharp
public bool HasValue { get; }
public T Value { get; }
```

### 5.2. Reference Types

All types in C#, including reference types, derive from the .NET base class. With value types, each variable has its own copy of the data. With reference types, on the other hand, two variables can reference the same object. Operations on one variable can therefore affect the object referenced by other variables.

C# provides three built-in reference types, and Furthermore, custom reference types can be declared with the following keywords:

record (or, record

and

Array types are somewhat special in that they do not have to be declared before they are used. Array types are constructed by appending square brackets to a type name. For example, int[] is a (single-dimensional) array of int, int[,] is a two-dimensional array of int, and int[][] is an array of arrays of int.

### 5.2.1. Nullable reference types

In the nullable reference types context all variables of a reference type are non-nullable. You can explicitly declare a nullable variable by appending the type name with the ? symbol, which denotes a nullable reference type. For example,

```csharp
string firstName = "Pele";
string? middleName = null;
```

①

The variable firstName is non-nullable.

②

string? is a nullable counterpart of the reference type string. The variable middleName is nullable.

For nullable reference types, the compiler uses flow analysis to ensure that any variable of a nullable reference type is checked against null before it’s accessed or assigned to a non-nullable reference type.

### 5.3. Dynamic Types

All C# types, builtin or user-defined, use static binding. That is, the type of a variable or an expression is determined at compile time. The dynamic type is an exception. It uses dynamic binding at run time. In most cases, dynamic can be considered identical to object (since all types ultimately inherit from object).

For example,

```csharp
dynamic theSecret = 42;
dynamic theGreatestUnknown = "meh";
```

Syntactically, an expression of the dynamic type can be implicitly converted to any type at run time. If the conversion fails, however, a runtime exception is thrown. If dynamic binding is not desired, the expression can be converted to object first, and then to the desired type. For instance,

```csharp
dynamic realSecret = 42 * 42 * 42;
int huh = realSecret;
string cops = realSecret;
```

①

This implicit conversion will succeed at run time.

## 6. Constants

A constant is a variable representing a constant value, that is, a value that can be computed at compile time. Constant members are discussed later, e.g., in the class constant member section.

Local constants can be declared using a local constant declaration statement.

```csharp
const TYPE NAME = EXPR ;
```

①

A constant is declared with the keyword const. The words with all upper case letters, in notations like this, are placeholders. That is, TYPE, NAME, and EXPR will need to be replaced with a type, name (or, identifier), and expression in a real statement. In the local constant declaration, the right hand side EXPR must be a constant expression.

More than one constant can be declared in a single statement. For example,

```csharp
const TYPE NAME1 = EXPR1 , NAME2 = EXPR2 ;
```
