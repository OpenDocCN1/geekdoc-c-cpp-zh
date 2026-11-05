
Category. Dictionary definitions of the word “type” run something like this: a kind of group that can be differentiated from other kinds of groups by a particular set of characteristics. Example 2–1 should help you build on your understanding of what a type is and the importance of using the correct type.

### Example 2.1

You might have or plan to own a certain type of vehicle, such as a Hummer or a Corvette. Hummer vehicle types have different characteristics from those of the Corvette. A Corvette can travel at a faster pace than a Hummer. But the Hummer can travel over much rougher terrain. You would not take the Corvette into a mountainous hiking region with the expectation that it could travel over large rocks, whereas a Hummer might do the trick. You would not want to transport four people in a Corvette, but four people could easily fit into a Hummer. Each is considered a vehicle. If you owned both, you could decide which one to use depending on the situation or destination.

For C# there is more than one type of number. One number is called an **integer**, or **int**. The **int** type is a whole number, between a certain range of values, and contains no decimal point. Another type of number is a **floating-point value**, which can contain a fractional portion. C# supports two types of floating-point types: `float` and `double`. If you wanted to store your grade point average, it would not be appropriate to put that value in an `int` because an `int` only lets you store the whole number portion. It would be like trying to put more than two people in the Corvette. They just do not fit. If your grade point average is 3.87 and you place the value in an `int` type, it chops off, or **truncates**, the .87 and your grade point average becomes 3. You would not be very happy with that, would you?

## Classes

Types are actually implemented through classes in C#. The Framework class library, which is part of .NET, includes over 2000 classes that you can use in your programs. For simplicity, you can think of there being a one-to-one correspondence between a class and a type in C#. C# was designed from the ground up to be a true object-oriented language. As you learned in Chapter 1, every program must include a class. C# is a strongly typed language. There are a number of types built into the language and C# also enables you to write or create your own user-defined data types or classes. In Chapter 11, Advanced Object-Oriented Programming Features, you will also read about another data type called an anonymous data type. In C#, a simple built-in numeric data type such as a whole number is also sometimes referred to as a **primitive type**.

## Objects

As previously mentioned, an object is an instance of a class. It is an occurrence of the class. For simplicity purposes, you can think of an instance of the base type int as 21 or 3421. However, a class includes more than just the data associated with the type. Class is the term used to denote the encapsulation of data and behaviors into a single package or unit. The characteristics of the class's behavior and data can be described. The data portion of the int, as indicated previously, is always a whole number value. An int data type can store values that do not have a decimal portion. The behavior of the int data type can be described by identifying basic arithmetic operations such as addition and subtraction that can be performed on the type. Logical comparisons can determine which is larger than the other, and values can be displayed. These are all behaviors of the int data type. Encapsulating (packaging) these data and behavior characteristics into a single unit allows you to describe the type.

### Example 2.2

Your current grade point average might be named using an identifier such as gradePointAverage. Grade point average normally takes the form of a real number with a fractional component, such as 3.42. In C#, real numbers with decimals are represented using the double data type. Your name is another data item composed of a string of characters. In C#, the data type string is used to represent a grouping of characters. To represent a single character, such as the first initial of your last name, a char data type is used. Your age, for example 21, is a whole number without a fractional part. The data type most often used to represent a number without a fractional part is an int.

Table 2-7 shows some examples of different data types, with examples of what might be stored in each of these data items.

**Table 2-7 Sample data types**

| Description | Identifier | Data type | Data |
|---|---|---|---|
| Grade point average | gradePointAverage | double | 3.99 |
| Current age | age | int | 19 |
| Full name | studentName | string | Elizabeth Hill |
| Final grade in a course | courseGrade | char | A |

You learned in Chapter 1 that every program must define a class. There are thousands of classes that make up the .NET Framework class library. The next section describes some of the predefined data types that are considered primitive data types in most languages. These value and reference types will be explored: int, double, decimal, bool, char, and string.

## Predefined Data Types

The .NET Framework includes a common type system (CTS) that is supported by all .NET languages, including C#. This enables cross-language integration of code, meaning a single application can be written using multiple languages, such as C#, Visual C++, and Visual Basic. The types in the CTS are referred to as common types and are divided into two major categories, as seen in Figure 2-3: value types and reference types.

![](img/36e48639a06772bcb0fa1ea2525b33a3_118_0.png)

**FIGURE 2-3** .NET common types

When placed in memory, value types contain their own copy of data, in binary notation. The data is stored in the actual memory cell that is addressed by the value type’s identifier. In contrast, the contents of reference type memory cells are much different. Reference types contain the address or location in which the sequence of bits is stored. Figure 2-4 shows the difference between how value types are stored and how reference types are stored. An integer value type, such as 2012, representing the year a car was manufactured, is stored directly in the memory cell. To store a string of characters, such as the kind of vehicle, the memory location would contain the address in which “Corvette” is located. The string data type is a reference type. The memory location associated with the identifier does not contain the characters “Corvette”, but instead the address in which “Corvette” is stored.

C# also supports pointer types to a limited extent. A pointer is a variable that holds the memory address of another type. In C#, pointers can only be declared to hold value types and arrays. You will read more about arrays in Chapter 8.

![](img/36e48639a06772bcb0fa1ea2525b33a3_119_0.png)

**FIGURE 2-4** Memory representation for value and reference types

## Value Types

The **value types** are often called the fundamental data types or primitive data types of the language. They are the common types needed by most applications. In C#, these fundamental types are further subdivided into the following categories:

- Struct types
- Enumerated types

As you look down the hierarchy of Figure 2-5, at the lowest level you find that Integral, Floating-point, and Decimal make up the Numeric types.

![](img/36e48639a06772bcb0fa1ea2525b33a3_120_0.png)

**FIGURE 2-5** Value type hierarchy

Twelve types belong to the numeric value type. Nine of them are Integral (whole number types), two are floating-point (numbers that can have a fractional value), and one is a decimal type. The decimal type is a fairly new data type; it is not found with C++, C, or Java. It was added to C# to eliminate the problems of loss of precision in mathematical operations that occurred in previous languages. The basic C# types all have aliases in the System namespace. Table 2-8 shows the keywords for the built-in C# types, including the numeric type each belongs to in the hierarchy, and the aliases in the System namespace.

**Table 2-8 C# value data types with .NET alias**

| C# type | Numeric type | .NET alias type |
|---|---|---|
| byte | Integral | System.Byte |
| sbyte | Integral | System.SByte |
| char | Integral | System.Char |
| decimal | Decimal | System.Decimal |
| double | Floating-point | System.Double |

(continues)
