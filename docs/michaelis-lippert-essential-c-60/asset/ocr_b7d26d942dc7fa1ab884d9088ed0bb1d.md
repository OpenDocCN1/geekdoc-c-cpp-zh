> **NOTE**
> When implementing a conversion operator, either the return or the parameter must be of the enclosing type—in support of encapsulation. C# does not allow you to specify conversions outside the scope of the converted type.

# Guidelines for Conversion Operators

The difference between defining an implicit and an explicit conversion operator centers on preventing an unintentional implicit conversion that results in undesirable behavior. You should be aware of two possible consequences of using the explicit conversion operator. First, conversion operators that throw exceptions should always be explicit. For example, it is highly likely that a string will not conform to the format that a conversion from string to Coordinate requires. Given the chance of a failed conversion, you should define the particular conversion operator as explicit, thereby requiring that you be intentional about the conversion and ensure that the format is correct or, alternatively, that you provide code to handle the possible exception. Frequently, the pattern for conversion is that one direction (string to Coordinate) is explicit and the reverse (Coordinate to string) is implicit.

A second consideration is the fact that some conversions will be lossy. Converting from a float (4.2) to an int is entirely valid, assuming an awareness of the fact that the decimal portion of the float will be lost. Any conversions that will lose data and will not successfully convert back to the original type should be defined as explicit. If an explicit cast is unexpectedly lossy or invalid, consider throwing a System.InvalidCastException.

> **Guidelines**
> **DO NOT** provide an implicit conversion operator if the conversion is lossy.
> **DO NOT** throw exceptions from implicit conversions.

# Referencing Other Assemblies

Instead of placing all code into one monolithic binary file, C# and the underlying CLI platform allow you to spread code across multiple