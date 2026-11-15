# Guidelines for Conversion Operators

The difference between defining an implicit and an explicit conversion operator centers on preventing an unintentional implicit conversion that results in undesirable behavior. You should be aware of two possible consequences of using the explicit conversion operator. First, conversion operators that throw exceptions should always be explicit. For example, it is highly likely that a string will not conform to the appropriate format that a conversion from string to Coordinate requires. Given the chance of a failed conversion, you should define the particular conversion operator as explicit, thereby requiring that you be intentional about the conversion and that you ensure that the format is correct, or that you provide code to handle the possible exception. Frequently, the pattern for conversion is that one direction (string to Coordinate) is explicit and the reverse (Coordinate to string) is implicit.

A second consideration is the fact that some conversions will be lossy. Converting from a float (4.2) to an int is entirely valid, assuming an awareness of the fact that the decimal portion of the float will be lost. Any conversions that will lose data and not successfully convert back to the original type should be defined as explicit.

# Referencing Other Assemblies

Instead of placing all code into one monolithic binary file, C# and the underlying CLI platform allow you to spread code across multiple assemblies. This enables you to reuse assemblies across multiple executables.

# BEGINNER TOPIC

# Class Libraries

The HelloWorld.exe program is one of the most trivial programs you can write. Real-world programs are more complex, and as complexity increases, it helps to organize the complexity by breaking programs into multiple parts. To do this, developers move portions of a program into separate compiled units called class libraries or, simply, libraries. Programs then reference and rely on class libraries to provide parts of their functionality. The