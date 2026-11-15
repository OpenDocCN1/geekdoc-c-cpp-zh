System.Convert supports only a predefined number of types and it is not extensible. It allows conversion from any primitive type (bool, char, sbyte, short, int, long, ushort, uint, ulong, float, double, decimal, DateTime, and string) to any other primitive type.

Furthermore, all types support a ToString() method that can be used to provide a string representation of a type. Listing 2.28 demonstrates how to use this method. The resultant output is shown in Output 2.18.

# Listing 2.28: Using ToString() to Convert to a string

```
bool boolean = true;
string text = boolean.ToString();
// Display "True"
System.Console.WriteLine(text);
```

# OUTPUT 2.18:

![](bbox=[0.18, 0.4, 0.88, 0.44])

For the majority of types, the ToString() method will return the name of the data type rather than a string representation of the data. The string representation is returned only if the type has an explicit implementation of ToString(). One last point to make is that it is possible to code custom conversion methods, and many such methods are available for classes in the runtime.

# ADVANCED TOPIC

# TryParse()

Starting with C# 2.0 (.NET 2.0), all the numeric primitive types include a static TryParse() method. (In C# 1.0, only double includes such a method.) This method is very similar to the Parse() method, except that instead of throwing an exception if the conversion fails, the TryParse() method returns false, as demonstrated in Listing 2.29.

# Listing 2.29: Using TryParse() in Place of an Invalid Cast Exception

```
double number;
string input;
```