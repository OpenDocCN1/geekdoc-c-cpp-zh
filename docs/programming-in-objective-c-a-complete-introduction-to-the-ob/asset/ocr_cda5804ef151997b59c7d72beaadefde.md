# Chapter 4 Data Types and Expressions

can't be used. (So the value 12000 is not a valid integer constant and must have a range written as 12000.)

Every value, whether it's a character, an integer, or a floating-point number, has a range of values associated with it. This range has to do with the amount of storage allocated to store a particular type of data. In general, that amount is not defined in the language; it typically depends on the computer you're running on and is therefore called implementation or machine dependent. For example, an integer variable might take 32 bits on your computer, or it might be stored in 64. If 64 bits were used, then much larger numbers can be stored integer variables if 32 bits were used instead.

> Note Under OS X, you are given the option of compiling an application as either a 32-bit or 64-bit application. In the former case, an int takes 32 bits; in the latter case, 64 bits are used.

# Type float

You can use a variable declared to be of float to store values containing decimal digits. A floating-point constant is distinguished by the presence of a decimal point. The values 3.,125.8, and .0001 are all examples of floating-point constants. To display a floating-point value, the NSLog conversion characters %f or %g can be used.

Floating-point constants can also be expressed in so-called scientific notation. 1.7e4 is a floating-point value expressed in this notation that represents the value 1.7 x10⁴. As noted, the double type is the same as type float, only with roughly twice the range.

# Type char

You can use a char variable to store a single character. A character constant is formed by enclosing the character within a pair of single quotation marks. So 'a','\'; and '0' are all examples of character constants. The first constant represents the letter a, the second is a semicolon; and the third is the character zero—which is not the same as the number zero. Do not confuse a character constant, which is a single character enclosed in single quotes, with a C-style string, which is any number of characters enclosed in double quotes. As mentioned in the last chapter, a string of characters enclosed in a pair of double quotes that is preceded by an @ is an NSString string object.

The character constant '\n', the newline, is a valid character even though it seems to contradict the rule cited previously. The reason for this is that the backslash is a special character. In other words, the Objective-C compiler treats the character '\n' as a single character, even though it is actually formed by two characters. Other special characters are initiated with the backslash character. The format characters %c can be used in an NSLog call to display the value of a char variable. Program 4.1 uses the basic Objective-C data types.