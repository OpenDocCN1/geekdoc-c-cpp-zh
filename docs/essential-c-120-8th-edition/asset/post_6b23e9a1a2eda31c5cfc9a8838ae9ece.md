
# 82 Chapter 2: Data Types

null can also be used as a type of "literal". The null value indicates that a variable is set to nothing. Code that sets a variable to null explicitly assigns a "nothing" value. In fact, it is even possible to check whether a variable refers to a null value.

Assigning the null value is not equivalent to assigning it to all. In other words, a variable that has been assigned null still has been set, whereas a variable with no assignment has not been set and, therefore, will often cause a compile error if used prior to assignment.

Note that assigning the null to a string variable is distinctly different from assigning an empty string, "". Use of null indicates that the variable has no value, whereas " " indicates that there is a value—an empty string. This type of distinction can be quite useful. For example, the programming logic could interpret a string named homePhone of null to mean that the phone number value of " " could indicate that there is no home phone number.

![](img/ffe0f34eac7523830420733690014d17_116_0.png)

# ADVANCED Modifier

## Nullable Modifier

Listing 2.25 demonstrates assigning null to an integer variable by adding nullable modifier—a question mark (?)—to the type declaration.

LISTING 2.25: Assigning null to a String

```csharp
public static void Main() {
    int? age;
    //...

    // Clear the value of age
    age = null;

    // ...
}
```

Prior to the nullable modifier, 6 there was no way to assign null to a variable of any of the types we have introduced so far (value types) except string (which is a reference type). (See Chapter 3 for more information on value types and reference types.)

Furthermore, prior to C# 8.0, reference types (like string) supported null assignment by default, and as such, you couldn't decorate a reference type with a nullable modifier. Since null could implicitly be assigned anyway, decorating it with a nullable modifier was redundant.

# ADVANCED Reference Types

Prior to C# 8.0, since all reference types were nullable by default, there was no concept of a nullable reference type—all reference types just were nullable. In C# 8.0, however the behavior became configurable such that reference types could be declared as a nullable modifier or default to null otherwise. In so doing, C# 8.0 introduced the concept of nullable reference types. Reference type variables with the nullable modifier are nullable reference types. And, when nullable reference types are enabled, a warning will appear when assigning null to a variable of reference type without the nullable modifier.

The only reference type covered so far in this book is string. If configured to support the nullable modifier on reference types, you could, for example, declare a string variable such as

```csharp
string? homeNumber = null;
```

To support nullability, be sure that the Nullable element in the .csproj file is set to enable.

- 6. Support for the nullable modifier was added in C# 2.0.

# Chapter 2: Data Types

## The void "Type"
Sometimes the C# syntax requires a data type to be specified, but no data is passed. For example, if no return from method is needed, C# allows you to specify void as the data type instead. The declaration of Main in the HelloWorld program (Listing 1.1) is an example. The use of void as the return type indicates that the method is not returning any data and tells the compiler not to expect a value. void is not a data type se but rather an indication that there is no data returned.

## Language Contrast: C++

In both C++ and C#, void has two meanings: as a marker that a method does not return any data and to represent a pointer to storage location of unknown type. In C++ programs, it is quite common to see pointer types as void*. C can also represent pointers to storage locations of unknown type using the same syntax, but this usage is comparatively rare in C# and typically encountered when writing programs that operate with unmanaged code libraries.

## Conversions between Data Types

Given the thousands of types predefined in .NET and the unlimited number of types that can define, it is important that types support conversion from one type to another where it makes sense. The most common operation that results in a conversion is casting.

Consider the conversion between two numeric types: converting a variable of type long to a variable of type int. A long type can contain values as large as 9,223,372,036,854,778; however, the maximum size of an int is 2,147,483,647. So, that conversion could result in a loss of data—example, if the variable of type long contains a value greater than the maximum size of an int. Any conversion that could result in a loss of data (such as magnitude and/or precision) or an exception because the conversion failed requires an explicit cast. Conversely, a numeric conversion will not lose magnitude and will not throw an exception regardless of the operand types is an implicit conversion.

# Conversions between Data Types

## Explicit Cast

In C#, you using the cast operator. By specifying the type, you would like the variable converted to within parentheses, you acknowledge that if an explicit cast is occurring, there may be a loss of precision and data, or an exception may result. The code in Listing 2.26 converts a long to an int and explicitly tells the system to attempt the operation.

- LISTING 2.26: Explicit Cast Example

```csharp
long longNumber = 9223372036854778;
int intNumber = (int)longNumber;
```

With the cast operator, the programmer essentially says to the compiler, "Trust me, I know what I am doing. I know that value will fit." However, with an explicit cast, there is still a chance that conversion fails.

# ADVANCED TOPIC

## Checked and Unchecked Conversions

C# provides special keywords for marking what should happen if the target type is too small. By default, this is unchecked, as shown in Listing 2.27.

-   LISTING 2.27: Overflowing an Integer

```csharp
long longNumber = 2147483647;
int intNumber = (int)longNumber;
```

# 86 Chapter 2: Data Types

- 2147483647

- 2.28: A Checked Example

```csharp
checked {
    long longNumber = 2147483647;
    int intNumber = (int)longNumber;
}
```

- 2147483648

- 2.29: An Unchecked Example

```csharp
unchecked {
    long longNumber = 2147483647;
    int intNumber = (int)longNumber;
}
```

- 2147483648

