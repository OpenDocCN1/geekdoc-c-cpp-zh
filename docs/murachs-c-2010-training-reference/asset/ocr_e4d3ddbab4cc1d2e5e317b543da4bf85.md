# How to work with the built-in value types

To start, this chapter shows how to work with the built-in data types that the .NET Framework provides. As you will see, these consist of value types and reference types.

# The built-in value types

Figure 4-1 summarizes the value types that the .NET Framework provides. To refer to each of these data types, C# provides a keyword. You can use the first eleven data types to store numbers, and you can use the last two data types to store characters and true or false values.

The first eight data types are used to store integers, which are numbers that don't contain decimal places (whole numbers). When you use one of the integer type, you should select an appropriate size. Most of the time, you can use the int type. However, you may need to use the long type if the value is too large for the int type. On the other hand, if you're working with smaller numbers and you need to save resources, you can use the short or byte type. these types.

You can use the next three data types to store numbers that contain decimal places. Since the decimal type is more accurate than the double and float types, it's commonly used for monetary values. If you need to save system resources, however, the double and float types are adequate for most situations.

You can use the char type to store a single character. Since C# supports the two-byte Unicode character set, it can store practically any character from any language around the world. As a result, you can use C# to create programs that read and print Greek or Chinese characters. In practice, though, you'll usually work with the characters that are stored in the older one-byte ASCII character set. These characters are the first 256 characters of the Unicode character set.

Last, you can use the bool type to store a true value or false value. This type of value is known as a Boolean value.