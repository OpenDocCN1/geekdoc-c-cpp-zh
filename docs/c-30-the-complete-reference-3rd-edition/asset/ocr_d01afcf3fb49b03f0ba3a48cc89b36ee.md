# Strings and Formatting

This chapter examines the String class, which underlies C#’s string type. As all programmers know, string handling is a part of almost any program. For this reason, the String class defines an extensive set of methods, properties, and fields that give you detailed control over the construction and manipulation of strings. Closely related to string handling is the formatting of data into its human-readable form. Using the formatting subsystem, you can format the C# numeric types, date and time, and enumerations.

# Strings in C#

An overview of C#’s string handling was presented in Chapter 7, and that discussion is not repeated here. However, it is worthwhile to review how strings are implemented in C# before examining the String class.

In all computer languages, a string is a sequence of characters, but precisely how such a sequence is implemented varies from language to language. In some computer languages, such as C++, strings are arrays of characters, but this is not the case with C#. Instead, C# strings are objects of the built-in string data type. Thus, string is a reference type. Moreover, string is C#’s name for System.String, the standard .NET string type. Thus, a C# string has access to all of the methods, properties, fields, and operators defined by String.

Once a string has been created, the character sequence that comprises a string cannot be altered. This restriction allows C# to implement strings more efficiently. Though this restriction probably sounds like a serious drawback, it isn’t. When you need a string that is a variation on one that already exists, simply create a new string that contains the desired changes, and discard the original string if it is no longer needed. Because unused string objects are automatically garbage-collected, you don’t need to worry about what happens to the discarded strings. It must be made clear, however, that string reference variables may, of course, change the object to which they refer. It is just that the character sequence of a specific string object cannot be changed after it is created.

To create a string that can be changed, C# offers a class called StringBuilder, which is in the System.Text namespace. For most purposes, however, you will want to use string, not StringBuilder.