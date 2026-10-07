
## Chapter 2: Data Types

## Implicit Conversion

In other instances, as when going from an int type to a long type, there is no loss of precision, and no fundamental change in the value of the type occurs. In these cases, the code needs to specify only the assignment operator; the conversion is implicit. In other words, the compiler can determine that such a conversion will work correctly. The code in Listing 2.30 converts from an int to a long by simply using the assignment operator.

Listing 2.30: Not Using the Cast Operator for an Implicit Conversion

```
int intNumber = 31416;
long longNumber = intNumber;
```

Even when no explicit cast operator is required (because an implicit conversion is allowed), it is still possible to use the cast operator (see Listing 2.31).

Listing 2.31: Using the Cast Operator for an Implicit Cast

```c
int intNumber = 31416;
long longNumber = (long)intNumber;
```

## Type Conversion without Casting

No conversion is defined from a string to a numeric type, so methods such as Parse() are required. Each numeric data type includes a Parse() function that enables conversion from a string to the corresponding numeric type. Listing 2.32 demonstrates this call.

Listing 2.32: Using float.Parse() to Convert a string to a Numeric Data Type

```csharp
string text = $"9.11E-31";
float kgElectronMass = float.Parse(text);
```

Another special type is available for converting one type to the next. This type is System.Convert, and an example of its use appears in Listing 2.33.

## Conversions between Data Types

LISTING 2.33: Type Conversion Using System.Convert

```csharp
string middleCText = "261.626";
double middleCText = Convert.ToDouble(middleCText);
bool boolean = Convert.ToBoolean(middleCText);
```

System.Convert supports only a small number of types and is not extensible. It allows conversion of any of the types bool, char, sbyte, short, int, long, ushort, uint, ulong, float, double, decimal, DateTime, and string to any of other types.

All types support a ToString() method that can be used to provide a string representation of a type. Listing 2.34 demonstrates how to use this method. The result output is shown in Output 2.18.

LISTING 2.34: ToString() to Convert to a string

```csharp
bool boolean = true;
string text = boolean.ToString();
// Display "True"
Console.WriteLine(text);
```

OUTPUT 2.18

| True |

For the majority of types, the ToString() method returns the name of the data type rather than a string representation of the data. The string representation is returned only if the type has an explicit implementation of ToString(). One last point to make is that it is possible to code custom conversion methods, and many such methods are available for classes in the runtime.

## Chapter 2: Data Types

## ADVANCED TOPIC

### TryParse()

All numeric primitive types include a static TryParse() method. All numeric primitive types include a static TryParse() method. This method is similar to the Parse() method, except instead of throwing an exception if the conversion fails, the TryParse() method returns false, as demonstrated in Listing 2.35 and Output 2.19.

LISTING 2.35: Using TryParse() in Place of an Invalid Exception

```csharp
double number;
string input;

Console.Write("Enter a number: ");
input = Console.ReadLine();
if (double.TryParse(input, out number))
{
    // Converted correctly, now use number
    // ...
}
else{
    Console.WriteLine("The text entered was not a valid number.");
}
```

# OUTPUT 2.19

Enter a number: forty-two
The text entered was not a valid string

The result value that the code parses from the input string is returned an out parameter (see "Output Parameters (out)") in Chapter 5 (https://essentialcsharp.com/output-parameters-out)) in this case, number.

In addition to the various number types, the TryParse() method is available for enums.

- 7. Starting with C# 2.0.

Starting with C# 7.0, it is no longer necessary to declare a variable before using it as an out argument. Using this feature, the declaration for number is shown in Listing 2.36.

# LISTING 2.36: TryParse() with Inline Declaration in C# 7.0

```csharp
// double number;
string input;

Console.Write("Enter a number: ");
input = Console.ReadLine();
if (double.TryParse(input, out double number))
{
    Console.WriteLine($"{input was parsed successfully to {number}.");
}
else
{
    // Note: number scope is here too (although not assigned)
    Console.WriteLine("The text entered was not a valid number.");
}

Console.WriteLine($"{number} currently has the value: {number}");
```

Notice that the data type of number is specified following the out modifier before the variable it declares. The result is that the number variable is available from both the true and false consequences of the if statement and even outside the if statement.

The key difference between Parse() and TryParse() is that TryParse() won't throw an exception if it fails. Frequently, the conversion from a string to a numeric type depends on a user entering the text. It is expected, in such scenarios, that the user will enter invalid data that will not parse successfully. By using TryParse() rather than Parse(), you can avoid throwing exceptions in expected situations. (The expected situation in this case is that the user will enter invalid data, and we try to avoid throwing exceptions for expected scenarios.)

## Summary

Even for experienced programmers, C# introduces several new programming constructs. For example, as part of the section on data types, this chapter covered the type decimal, which can be used to perform financial calculations without floating-point anomalies. In addition, the chapter introduced the fact that the Boolean type, bool, does not convert implicitly to or from the integer type, thereby preventing the mistaken use of the assignment operator in a conditional expression. Other characteristics of C# that distinguish it from many of its predecessors are the verbatim string qualifier and raw string literals (both force a string to ignore the escape character); string interpolation, which makes code easier to read by embedding it into the string; and the immutable nature of the string data type.

In Chapter 3, we continue the topic of data types by elaborating more on the two types of data types: value types and reference types. In addition, we look at combining data elements together.

## More with Data Types

In Chapter 2, we covered the types of types and briefly touched on reference types versus value types. In this chapter, we continue the discussion of types. To begin, let's delve further into understanding value types and reference types.

| Declaring | Value Types |
| --- | --- |
| Instantiating and Assigning 5. Arrays | 1. Categories of Types Reference Types |
| Using | 2. Declaring That allow null |
| Strings as Arrays 4. Tuples | 3. Implicitly Typed Local Variables |

## Categories of Types

All types fall into one of two categories: **value types** and **reference types**. The differences between the types in each category stem from how they are copied: Value type data is always copied by value, whereas reference type data is always copied by reference.

## Chapter 3: More with Data Types

## Value Types

Except for string, all the predefined types so far have been value types. Variables of value types contain the value directly. In other words, the variable refers to the same location where the value is stored. Because, when a different variable is assigned the same value, a copy of the original variable's value is made to the location of the new variable. A second variable of the same type cannot refer to the same location in memory as the first. Consequently, changing the value of the first variable will not affect the value in the second variable, as Figure 3.1 demonstrates. In the figure, number1 refers to a location in memory that contains the value 42. After assigning number1 to number2, both variables will contain 42. However, modifying either variable's value will not affect the other.

![](img/ffe0f34eac7523830420733690014d17_128_0.png)

FIGURE 3.1: Value types contain the data directly

Similarly, passing a value type to a method such as Console.WriteLine() will result in a memory copy, and any changes to the parameter inside the method will not affect the original value within the calling function. Since value types require a memory copy, they generally should be defined to consume a small amount of memory; value types should almost always be less than 16 bytes in size

## Reference Types

By contrast, the value of a reference type is a reference to a location that contains data. Reference types store the reference where the data is located instead of storing the data directly, as value types do. Therefore, to access the data, the runtime reads the memory location out of the variable and then “jumps” to
