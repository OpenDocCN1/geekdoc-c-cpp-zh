cater to both cultures as follows:

Click here to view code image

```
enum Season { Spring, Summer, Fall, Autumn = Fall, Winter }
```

# Choosing an enumeration’s underlying type

When you declare an enumeration, the enumeration literals are given values of type int. You can also choose to base your enumeration on a different underlying integer type. For example, to declare that the underlying type for Season is a short rather than an int, you can write this:

Click here to view code image

```
enum Season : short { Spring, Summer, Fall, Winter }
```

The main reason for using short is to save memory; an int occupies more memory than a short, and if you do not need the entire range of values available to an int, using a smaller data type can make sense.

You can base an enumeration on any of the eight integer types: byte, sbyte, short, ushort, int, uint, long, or ulong. The values of all the enumeration literals must fit within the range of the chosen base type. For example, if you base an enumeration on the byte data type, you can have a maximum of 256 literals (starting at 0).

Now that you know how to declare an enumeration, the next step is to use it. In the following exercise, you will work with a console application to declare and use an enumeration that represents the months of the year.

# Create and use an enumeration

+   1. Start Microsoft Visual Studio 2015 if it is not already running.
+   2. Open the StructsAndEnums project, which is located in the \Microsoft Press\VCSBS\Chapter 9\StructsAndEnums folder in your Documents folder.
+   3. In the Code and Text Editor window, display the Month.cs file.
+      The source file is empty apart from the declaration of a namespace called StructsAndEnums and a // TODO: comment.
+   4. Replace the // TODO: comment with the enumeration named Month within the StructsAndEnums namespace, as shown in bold in the code that follows. This enumeration models the months of the year. The 12 enumeration literals for Month are January through December.

Click here to view code image

```
namespace StructsAndEnums
{
    enum Month
    {
        January, February, March, April,
```