
Here is an example that uses is:

```
// Demonstrate is.
using System;
class A {}
class B : A {}
class UseIs {
    static void Main() {
        A a = new A();
        B b = new B();
        if(a is A) Console.WriteLine("a is an A");
        if(b is A)
            Console.WriteLine("b is an A because it is derived from A");
        if(a is B)
            Console.WriteLine("This won't display -- a not derived from B");
        if(b is B) Console.WriteLine("B is a B");
        if(a is object) Console.WriteLine("a is an object");
    }
}
```

The output is shown here:

```
a is an A
b is an A because it is derived from A
B is a B
a is an object
```

Most of the is expressions are self-explanatory, but two may need a little discussion.

First, notice this statement:

```
if(b is A)
    Console.WriteLine("b is an A because it is derived from A");
```

The if succeeds because b is an object of type B, which is derived from type A. Thus, b is an A. However, the reverse is not true. When this line is executed,

```
if(a is B)
    Console.WriteLine("This won't display -- a not derived from B");
```

the if does not succeed, because a is of type A, which is not derived from B. Thus, a is not B.

## Using as

Sometimes you will want to try a conversion at runtime, but not throw an exception if the conversion fails (which is the case when a cast is used). To do this, use the as operator, which has this general form:

```
expr as type
```

Here, *expr* is the expression being converted to *type*. If the conversion succeeds, then a reference to *type* is returned. Otherwise, a null reference is returned. The *as* operator can be used to perform only reference, boxing, unboxing, or identity conversions.

The *as* operator offers a streamlined alternative to *is* in some cases. For example, consider the following program that uses *is* to prevent an invalid cast from occurring:

```csharp
// Use is to avoid an invalid cast.

using System;

class A { }
class B : A { }

class CheckCast {
    static void Main() {
        A a = new A();
        B b = new B();

        // Check to see if a can be cast to B.
        if(a is B)  // if so, do the cast
            b = (B) a;
        else // if not, skip the cast
            b = null;

        if(b==null)
            Console.WriteLine("The cast in b = (B) a is NOT allowed.");
        else
            Console.WriteLine("The cast in b = (B) a is allowed");
    }
}
```

This program displays the following output:

```
The cast in b = (B) a is NOT allowed.
```

As the output shows, since *a* is not a *B*, the cast of *a* to *B* is invalid and is prevented by the *if* statement. However, this approach requires two steps. First, the validity of the cast must be confirmed. Second, the cast must be made. These two steps can be combined into one through the use of *as*, as the following program shows:

```csharp
// Demonstrate as.

using System;

class A { }
class B : A { }

class CheckCast {
    static void Main() {
        A a = new A();
        B b = new B();

        b = a as B; // cast, if possible
        if(b==null)
          Console.WriteLine("The cast in b = (B) a is NOT allowed.");
        else
          Console.WriteLine("The cast in b = (B) a is allowed");
    }
}
```

Here is the output, which is the same as before:

```
The cast in b = (B) a is NOT allowed.
```

In this version, the as statement checks the validity of the cast and then, if valid, performs the cast, all in one statement.

## Using typeof

Although useful in their own ways, the as and is operators simply test the compatibility of two types. Often, you will need to obtain information about a type. To do this, C# supplies the typeof operator. It retrieves a System.Type object for a given type. Using this object, you can determine the type's characteristics.

The typeof operator has this general form:

```csharp
typeof(type)
```

Here, type is the type being obtained. The Type object returned encapsulates the information associated with type.

Once you have obtained a Type object for a given type, you can obtain information about it through the use of various properties, fields, and methods defined by Type. Type is a large class with many members, and a discussion is deferred until the next section, where reflection is examined. However, to briefly demonstrate Type, the following program uses three of its properties: FullName, IsClass, and IsAbstract. To obtain the full name of the type, use FullName. IsClass returns true if the type is a class. IsAbstract returns true if a class is abstract.

```csharp
// Demonstrate typeof.

using System;
using System.IO;

class UseTypeof {
  static void Main() {
    Type t = typeof(StreamReader);

    Console.WriteLine(t.FullName);

    if(t.IsClass) Console.WriteLine("Is a class.");
    if(t.IsAbstract) Console.WriteLine("Is abstract.");
    else Console.WriteLine("Is concrete.");
  }
}
```

This program outputs the following:

```text
System.IO.StreamReader
Is a class.
Is concrete.
```

This program obtains a Type object that describes StreamReader. It then displays the full name, and determines if it is a class and whether it is abstract.

## Reflection

Reflection is the feature that enables you to obtain information about a type. The term reflection comes from the way the process works: A Type object mirrors the underlying type that it represents. To obtain information, you ask the Type object questions, and it returns (reflects) the information associated with the type back to you. Reflection is a powerful mechanism because it allows you to learn and use the capabilities of types that are known only at runtime.

Many of the classes that support reflection are part of the .NET Reflection API, which is in the System.Reflection namespace. Thus, you will normally include the following in programs that use reflection:

```
using System.Reflection;
```

### The Reflection Core: System.Type

System.Type is at the core of the reflection subsystem because it encapsulates a type. It contains many properties and methods that you will use to obtain information about a type at runtime. Type is derived from an abstract class called System.Reflection.MemberInfo. MemberInfo defines the following read-only properties:

| Property | Description |
|---|---|
| Type DeclaringType | Obtains the type of the class or interface in which the member is declared. |
| MemberTypes MemberType | Obtains the kind of the member. This value indicates if the member is a field, method, property, event, or constructor. |
| int MetadataToken | Obtains a value associated with a specific metadata. |
| Module Module | Obtains a Module object that represents the module (an executable file) in which the reflected type resides. |
| string Name | The name of the type. |
| Type ReflectedType | The type of the object being reflected. |

Notice that the return type of MemberType is MemberTypes. MemberTypes is an enumeration that defines values that indicate the various member types. Among others, these include

- MemberTypes.Constructor
- MemberTypes.Method
- MemberTypes.Field
- MemberTypes.Event
- MemberTypes.Property

Thus, the type of a member can be determined by checking MemberType. For example, if MemberType equals MemberTypes.Method, then that member is a method.

MemberInfo includes two abstract methods: GetCustomAttributes() and IsDefined(). These both relate to attributes. The first obtains a list of the custom attributes associated with the invoking object. The second determines if an attribute is defined for the invoking object. (Attributes are described later in this chapter.)

To the methods and properties defined by MemberInfo, Type adds a great many of its own. For example, here are several commonly used methods defined by Type:

| Method | Purpose |
|---|---|
| ConstructorInfo[] GetConstructors() | Obtains a list of the constructors for the specified type. |
| EventInfo[] GetEvents() | Obtains a list of events for the specified type. |
| FieldInfo[] GetFields() | Obtains a list of the fields for the specified type. |
| Type[] GetGenericArguments() | Obtains a list of the type arguments bound to a closed constructed generic type or the type parameters if the specified type is a generic type definition. For an open constructed type, the list may contain both type arguments and type parameters. (See Chapter 18 for a discussion of generics.) |
| MemberInfo[] GetMembers() | Obtains a list of the members for the specified type. |
| MethodInfo[] GetMethods() | Obtains a list of methods for the specified type. |
| PropertyInfo[] GetProperties() | Obtains a list of properties for the specified type. |

Here are several commonly used, read-only properties defined by Type:

| Property | Purpose |
|---|---|
| Assembly Assembly | Obtains the assembly for the specified type. |
| TypeAttributes Attributes | Obtains the attributes for the specified type. |
| Type BaseType | Obtains the immediate base type for the specified type. |
| string FullName | Obtains the complete name of the specified type. |
| bool IsAbstract | Is true if the specified type is abstract. |
| bool IsArray | Is true if the specified type is an array. |
| bool IsClass | Is true if the specified type is a class. |
| bool IsEnum | Is true if the specified type is an enumeration. |
| bool IsGenericParameter | Is true if the specified type is a generic type parameter. (See Chapter 18 for a discussion of generics.) |
| bool IsGenericType | Is true if the specified type is a generic type. (See Chapter 18 for a discussion of generics.) |
| string Namespace | Obtains the namespace of the specified type. |
