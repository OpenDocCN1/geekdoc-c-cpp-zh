such, it can have only two values, either true or false. It is important to understand this type, especially when using logical operators such as the 'if' statement. By default, its value is false.

**Byte:** This data type represents an 8-bit integer that is unsigned. It has a range of 0 to 255 when it comes to storing numbers. By default, the value of this data type is 0.

**Int:** This is actually short for the integer which is a data type used for storing numbers that do not have decimals like the byte type. However, unlike byte, Int has a range of -2,147,483,648 to 2,147,483,647. If you are working with numbers, you are more likely than not to end up using this type.

**Char:** This data type represents 16-bit Unicode character, and it is used for storing only one character.

**String:** This can be said to be an upgraded version of the char data type as it can be used for storing text. That is, it can store multiple chars instead of a single one. In C#, this data type is immutable. In other words, after the creation of a string, they are never changed. If you use methods which change a string, a new string is actually returned. The original one is not changed.

# An Introduction to Variables

Variables are crucial to programming. In any programming language, a variable is actually a storage location which has been associated name (referred to an identifier) and it contains some quantity of information which may be unknown or known. This information is referred to as the value. The identifier is used for referencing the stored value. During runtime, the identifier can be linked to a value, but this value may change as the program is executed.

In C#, each variable has a specific type, which determines the size and layout of the variable's memory range of values that can be stored within that memory and the set of operations that can be applied to the variable. (Tutorials Point)

The following table shows categorization of the basic value types in C#