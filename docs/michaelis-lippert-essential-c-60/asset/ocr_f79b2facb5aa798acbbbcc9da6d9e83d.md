# Chapter 2: Data Types

```
**LISTING 2.1: Specifying Literal Values**

```csharp
System.Console.WriteLine(42);
System.Console.WriteLine(1.618034);
```
```

Output 2.1 shows the results of Listing 2.1.

```
**OUTPUT 2.1**

```
42
1.618034
```
```

# BEGINNER TOPIC

# Use Caution When Hardcoding Values

The practice of placing a value directly into source code is called **hardcoding**, because changing the values requires recompiling the code. Developers must carefully consider the choice between hardcoding values within their code and retrieving them from an external source, such as a configuration file, so that the values are modifiable without recompiling.

By default, when you specify a literal number with a decimal point, the compiler interprets it as a double type. Conversely, a literal value with no decimal point generally defaults to an int, assuming the value is not too large to be stored in an integer. If the value is too large, the compiler will interpret it as a long. Furthermore, the C# compiler allows assignment to a numeric type other than an int, assuming the literal value is appropriate for the target data type. short s = 42 and byte b = 77 are allowed, for example. However, this is appropriate only for constant values; b = s is not allowed without additional syntax, as discussed in the section Conversions between Data Types later in this chapter.

As previously discussed in the section Fundamental Numeric Types, there are many different numeric types in C#. In Listing 2.2, a literal value is placed within C# code. Since numbers with a decimal point will default to the double data type, the output, shown in Output 2.2, is 1.61803398874989 (the last digit, 5, is missing), corresponding to the expected accuracy of a double.