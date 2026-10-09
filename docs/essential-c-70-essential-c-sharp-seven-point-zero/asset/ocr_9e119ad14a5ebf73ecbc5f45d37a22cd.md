Language Contrast: Visual Basic—Returning void Is Like Defining a Subroutine

The Visual Basic equivalent of returning a void in C# is to define a subroutine (Sub/End Sub) rather than a function that returns a value.

# Conversions between Data Types

Given the thousands of types predefined in the various CLI implementations and the unlimited number of types that code can define, it is important that types support conversion from one type to another where it makes sense. The most common operation that results in a conversion is **casting**.

Consider the conversion between two numeric types: converting from a variable of type long to a variable of type int. A long type can contain values as large as 9,223,372,036,854,775,808; however, the maximum size of an int is 2,147,483,647. As such, that conversion could result in a loss of data—for example, if the variable of type long contains a value greater than the maximum size of an int. Any conversion that could result in a loss of magnitude or an exception because the conversion failed requires an **explicit cast**. Conversely, a conversion operation that will not lose magnitude and will not throw an exception regardless of the operand types is an **implicit conversion**.

# Explicit Cast

In C#, you cast using the **cast operator**. By specifying the type you would like the variable converted to within parentheses, you acknowledge that if an explicit cast is occurring, there may be a loss of precision and data, or an exception may result. The code in Listing 2.20 converts a long to an int and explicitly tells the system to attempt the operation.

```
**LISTING 2.20: Explicit Cast Example**

long longNumber = 50918309109;
int intNumber = (int) longNumber;
Cast Operator
```

With the cast operator, the programmer essentially says to the compiler, “Trust me, I know what I am doing. I know that the value will fit into the