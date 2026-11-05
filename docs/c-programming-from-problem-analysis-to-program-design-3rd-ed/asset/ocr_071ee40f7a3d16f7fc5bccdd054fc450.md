sValue is a string variable that contains more than one character. The argument to char.Parse( ) must be a single-character string.

There is more than one way to convert from one base type to another. As part of the .NET Framework class library, in the System namespace, a number of static methods are found in the Convert class. These include Convert.ToDouble( ), Convert.ToDecimal( ), Convert.ToInt32( ), Convert.ToBoolean( ), and Convert.ToChar( ). Used like the Parse( ) method, they convert data from one base type to another base type. The following converts an entered string value to an int base type:

```
int newValue = Convert.ToInt32(stringValue);
```

These methods are all overloaded so that the argument to the method can be of varying type. If, for example, you send a char argument to the Convert.ToInt32( ) method, and store the result in an int variable, you get the Unicode numeric representation for that character.

> int.Parse( ) could be replaced by Int32.Parse( ). Int32 is the class in .NET. The int type is an alias for Int32. All .NET-supported languages recognize Int32.

You might be wondering whether you should use the Parse( ) methods or methods from the Convert class to convert your string values to their appropriate data types. It is really a matter of choice whichever you use. Both work well if the string is storing the correct data that you are attempting to convert. When you call the Convert.ToInt32( ), it actually calls the Int32.Parse( ) method. So, there is a little more overhead involved in the call to methods in the Convert class. The difference is that if you pass an empty string to the Convert class, it returns 0. If you pass an empty string (null string) to the Int32.Parse( ) method, it creates an error, similar to that illustrated in Figure 3-6, by throwing an ArgumentNullException. You will learn about how to handle exceptions in Chapter 11.

> You might also want to explore the TryParse( ) method. Int32.TryParse( ) attempts to convert a string to an int without throwing an exception.

One advantage the Convert class offers is it makes it easier to convert between all the base types—not just from a string to another data type. The Parse( ) method only works well for string conversions. For example, Int32.Parse( ) only converts strings to integers. Convert.ToInt32( ) converts any base type to an integer.

# Methods in the Math Class

The Math class has a number of predefined static methods you will find helpful. The Math class, like the Console class, is located in the System namespace. This class provides constants and methods for trigonometric, logarithmic, and other common mathematical functions. The Pow( ) method that you saw previously is a member of the Math