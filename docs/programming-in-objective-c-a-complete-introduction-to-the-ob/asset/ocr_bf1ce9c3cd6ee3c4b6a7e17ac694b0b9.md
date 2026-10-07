# Chapter 15 Numbers, Strings, and Collections

It is typedef either to a long 64-bit or to an int for 32-bit builds. A similar typedef for NSInteger exists for working with unsigned integers in your program.
In the NSLog, we cast the NSInteger myInt to a long and use the format character %li to ensure that the value is passed and displayed correctly even if the program is compiled for a 32-bit architecture.

For each basic data type, a class method exists that allocates an NSNumber object and sets it to a specified value. These methods begin with numberWithLong:; numberWithFloat; and so on. In addition, instance methods can be used to set a value to a previously alloced NSNumber object to a specified value. These all begin with initWithLong:; and initWithFloat:.

Table 15.1 lists the class and instance methods for setting values for NSNumber objects and the corresponding instance methods for retrieving their values.

| Creation and Initialization Class Method | Initialization Instance Method | Retrieval Instance Method |
| :--- | :--- | :--- |
| numberWithChar: | initWithChar: | charValue |
| numberWithUnsignedChar: | initWithUnsignedChar: | unsignedCharValue |
| numberWithShort: | initWithShort: | shortValue |
| numberWithUnsignedShort: | initWithUnsignedShort: | unsignedShortValue |
| numberWithInteger: | initWithInteger: | integerValue |
| numberWithUnsignedInteger: | initWithUnsignedInteger: | unsignedIntegerValue |
| numberWithInt: | initWithInt: | intValue |
| numberWithUnsignedInt: | initWithUnsignedInt: | unsignedIntValue |
| numberWithLong: | initWithLong: | longValue |
| numberWithUnsignedLong: | initWithUnsignedLong: | unsignedLongValue |
| numberWithLongLong: | initWithLongLong: | longLongValue |
| numberWithUnsignedLongLong: | initWithUnsignedLongLong: | unsignedLongLongValue |
| numberWithFloat: | initWithFloat: | floatValue |
| numberWithDouble: | initWithDouble: | doubleValue |
| numberBool: | initWithBool: | boolValue |

Returning to Program 15.1, the program next uses the class methods to create char, float, and double NSNumber objects. Notice what happens after you create a double object with the line

```
myNumber = [NSNumber numberWithDouble: 12345e+05];
and try to (incorrectly) retrieve and display its value with the following:
NSLog("%li", (long) [myNumber integerValue]);
```