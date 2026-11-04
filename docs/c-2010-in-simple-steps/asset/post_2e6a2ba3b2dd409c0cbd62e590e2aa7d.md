
Next, let's learn about implicit line continuations.

## Implicit Line Continuations

There may be situations where you might need to continue a single statement over multiple lines. In such situations, you can implicitly continue a statement in the next line, as shown in the following code snippet:

```
Console.WriteLine(
CalculateArea(length: 10, breadth: 5));
```

Now, let's proceed towards exploring keywords in C# 2010.

## Exploring C# 2010 Keywords

Keywords are those words or identifiers, which are reserved to be used for a specific task. You cannot use a keyword to define the name of a variable or method. Keywords are the reserved words whose meanings are predefined to the C# compiler. They are used in all the programming languages. A keyword is an essential part of a language definition. However, there are some keywords that have special meaning in the context of code but such keywords are not reserved keywords. These keywords are known as contextual keywords. Table 2.1 lists the reserved and contextual keywords:

**Table 2.1: Reserved and Contextual Keywords in C# 2010**

**Reserved Keywords**

|            |            |         |        |
| ---------- | ---------- | ------- | ------ |
| abstract   | as         | base    | bool   |
| break      | byte       | case    | catch  |
| char       | checked    | class   | const  |
| continue   | decimal    | default | delegate |
| do         | double     | else    | enum   |
| event      | explicit   | extern  | false  |
| finally    | fixed      | float   | for    |
| foreach    | goto       | if      | implicit |
| in         | in (generic modifier) | int | interface |
| internal   | is         | lock    | long   |
| namespace  | new        | null    | object |
| operator   | out        | out (generic modifier) | override |
| params     | private    | protected | public |
| readonly   | ref        | return  | sbyte  |
| sealed     | short      | sizeof  | stackalloc |
| static     | string     | struct  | switch |
| this       | throw      | true    | try    |
| typeof     | uint       | ulong   | unchecked |
| unsafe     | ushort     | using   | virtual |
| volatile   | void       | while   |        |

**Contextual Keywords**

|            |            |           |          |
| ---------- | ---------- | --------- | -------- |
| add        | alias      | ascending | descending |
| dynamic    | from       | get       | global   |

**Table 2.2: Value Types in C#**

| Value Type | What a Value Type Represents | Ranges | Default Value |
| --- | --- | --- | --- |
| bool | Boolean type, represents Boolean value | True or False | false |
| byte | 8-bit unsigned integer type | 0 to 255 | 0 |
| char | Single 16-bit Character type, a char value is a Unicode character | U+0000 to U+ffff | '\0' |
| decimal | 128-bit Precise decimal type with 28-29 significant digits | ±1.0 × 10^-28 to ±7.9 × 10^28 | 0.0M |
| double | 64-bit Double-precision floating-point type | ±5.0 × 10^-324 to ±1.7 × 10^308 | 0.0D |
| float | 32-bit Single-precision floating-point type | ±1.5 × 10^-45 to ±3.4 × 10^38 | 0.0F |
| int | 32-bit signed integer type | -2,147,483,648 to 2,147,483,647 | 0 |
| long | 64-bit signed integer type | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 | 0L |
| sbyte | 8-bit signed integer type | -128 to 127 | 0 |
| short | 16-bit signed integral type | -32,768 to 32,767 | 0 |
| uint | 32-bit unsigned integer type | 0 to 4,294,967,295 | 0 |
| ulong | 64-bit unsigned integer type | 0 to 18,446,744,073,709,551,615 | 0 |
| ushort | 16-bit unsigned integer type | 0 to 65,535 | 0 |

Value types can further be categorized into two parts: Struct types and Enumeration types, which are discussed next.

## Struct Types

The struct type is a value type and is stored on a stack. These types can encapsulate a small group of related variables, such as the name, rollno, age, class, and section of a student. The members of struct types, such as constructors, methods, properties, operators, events, nested types, indexers, constants, and fields cannot be declared as protected.

Moreover, struct types are created using the struct keyword. When you create a struct object and assign it to a variable, the variable holds the complete value of the struct object. As you know struct type is a value type; so any changes made in the new copy of struct type variable do not affect the old copy.

The struct types are categorized into the following five categories:

- Integral type: Implies that C# uses a set of basic data types, which are known as integral types. This set consists of the types, such as sbyte, byte, short, ushort, int, uint, long, ulong, and char. Integral types hold whole numbers, such as 123, -123, and 3456.

- Floating-Point type: Represents values in fractions, for example -123.45 and 123.56. The floating-point types are divided into two types: float and double.

    > **Note**
    > 
    > *To specify a number to a float type, you must append the character F (or f) to a value, such as 12.4F. If you omit F, the value is treated as double. The double data type contains a double-precision floating point number. It stores 64 bit floating-point values.*

- Decimal type: Specifies that decimal types are equivalent to long integer types, which behave as a floating-point type. Decimal values are intended to be used for the calculations in which truncation beyond the decimal point is not desired. The decimal types have more precision and smaller range as compared to the floating-point types. You must append character M (or m) to a value such as 123.45M to specify a number as a decimal type. If you omit M, the value is treated as double.

- **Boolean types (bool)**: Allows you to test a particular condition during the execution of a program. Boolean type takes only two values, **True** or **False**.

- **Nullable types**: Allows a user to assign a null value to a variable of any data type. The nullable types are often used with databases.

## Enumeration Types

An enumeration provides a way for attaching the integer type numbers to the names in a program, which in turn increases the readability of a code. Enumerations are the user-defined integer data types that are declared using the enum keyword. An enumeration makes code easier to maintain by assigning legitimate values to it. Moreover, enumeration is the most basic user-defined type, which makes a list of possible values for a given type. For instance, you might have a program that models a traffic light. Traffic lights have three possible states, the green (or go) light, the yellow (or warning) light, and the red (or stop) light; therefore, at any given point of time, a traffic light can be red, yellow, or green.

Now, let's learn about reference types in C#.

## Reference Types

Reference types have varied lengths and are stored on the heap of memory. When a value is assigned to a reference type variable, only the reference is copied and the actual value remains the same in the memory location. We can further categorize the reference types into two parts, pre-defined and user-defined types.

> **Note**
> 
> Heap is a data structure that is used to store reference types, such as objects in C#. Objects are stored arbitrarily in the heap and their existence or size cannot be determined until the application starts running.

Let's discuss pre-defined and user-defined types next.

### Pre-defined Types

Pre-defined reference types can be divided into two types:

- **Object type**: Refers to the ultimate base type of all the other pre-defined and user-defined data types in C#. You can use the Object type to convert a value type on a stack into an Object type to be placed on the heap.

- **String type**: Refers to the creation and manipulation of strings in C#. You can perform various operations, such as copy, compare, and concatenation on strings.

### User-defined Types

User-defined reference types refer to those types, which are defined using the pre-defined types. Following are the user-defined reference types:

- **Class**: Specifies that C# is purely an object-oriented language, so the base of all the C# programs is class. Using classes, you can group logically related data items and functions, which are required to work on data items.

- **Interface**: Refers to the collection of members, such as methods, delegates, events, and properties, which are implemented by classes. Interfaces cannot be instantiated but you can use them to offer a set of functionalities that is common to several classes. The concept of interface was introduced to support multiple inheritance because in C#, a class does not support multiple inheritance.
