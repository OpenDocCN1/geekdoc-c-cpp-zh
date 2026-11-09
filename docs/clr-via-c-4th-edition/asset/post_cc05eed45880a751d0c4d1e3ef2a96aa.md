
| Member | Member Type | Description |
|---|---|---|
| Append | Method | Appends a single object to the end of the character array, growing the array if necessary. The object is converted to a string by using the general format and the culture associated with the calling thread. |
| Insert | Method | Inserts a single object into the character array, growing the array if necessary. The object is converted to a string by using the general format and the culture associated with the calling thread. |
| AppendFormat | Method | Appends the specified objects to the end of the character array, growing the array if necessary. The objects are converted to strings by using the formatting and culture information provided by the caller. AppendFormat is one of the most common methods used with StringBuilder objects. |
| AppendLine | Method | Appends a blank line or a string with a blank line to the end of the character array, increasing the capacity of the array if necessary. |
| Replace | Method | Replaces one character with another or one string with another from within the character array. |
| Remove | Method | Removes a range of characters from the character array. |
| Equals | Method | Returns true only if both StringBuilder objects have the same maximum capacity, capacity, and characters in the array. |
| CopyTo | Method | Copies a subset of the StringBuilder's characters to a Char array. |

One important thing to note about StringBuilder's methods is that most of them return a reference to the same StringBuilder object. This allows a convenient syntax to chain several operations together.

```csharp
StringBuilder sb = new StringBuilder();
String s = sb.AppendFormat("{0} {1}", "Jeffrey", "Richter").
    Replace(' ', '-').Remove(4, 3).ToString();
Console.WriteLine(s);  // "Jeff-Richter"
```

You'll notice that the String and StringBuilder classes don't have full method parity; that is, String has ToLower, ToUpper, EndsWith, PadLeft, PadRight, Trim, and so on. The StringBuilder class doesn't offer any of these methods. On the other hand, the StringBuilder class offers a richer Replace method that allows you to replace characters or strings in a portion of the string (not the whole string). It's unfortunate that there isn't complete parity between these two classes because now you must convert between String and StringBuilder to accomplish certain tasks. For example, to build up a string, convert all characters to uppercase, and then insert a string requires code like the following.

```csharp
// Construct a StringBuilder to perform string manipulations.
StringBuilder sb = new StringBuilder();

// Perform some string manipulations by using the StringBuilder.
sb.AppendFormat("{0} {1}", "Jeffrey", "Richter").Replace(" ", "-");

// Convert the StringBuilder to a String in
// order to uppercase all the characters.
String s = sb.ToString().ToUpper();

// Clear the StringBuilder (allocates a new Char array).
sb.Length = 0;

// Load the uppercase String into the StringBuilder,
// and perform some manipulations.
sb.Append(s).Insert(8, "Marc-");

// Convert the StringBuilder back to a String.
s = sb.ToString();

// Display the String to the user.
Console.WriteLine(s); // "JEFFREY-Marc-RICHTER"
```

It’s inconvenient and inefficient to have to write this code just because StringBuilder doesn’t offer all of the operations that String does. In the future, I hope that Microsoft will add more string operation methods to StringBuilder to make it a more complete class.

## Obtaining a String Representation of an Object: ToString

You frequently need to obtain a string representation of an object. Usually, this is necessary when you want to display a numeric type (such as Byte, Int32, and Single) or a DateTime object to the user. Because the .NET Framework is an object-oriented platform, every type is responsible for providing code that converts an instance’s value to a string equivalent. When designing how types should accomplish this, the designers of the FCL devised a pattern that would be used consistently throughout. In this section, I’ll describe this pattern.

You can obtain a string representation for any object by calling the ToString method. A public, virtual, parameterless ToString method is defined by System.Object and is therefore callable using an instance of any type. Semantically, ToString returns a string representing the object’s current value, and this string should be formatted for the calling thread’s current culture; that is, the string representation of a number should use the proper decimal separator, digit-grouping symbol, and other elements associated with the culture assigned to the calling thread.

System.Object’s implementation of ToString simply returns the full name of the object’s type. This value isn’t particularly useful, but it is a reasonable default for the many types that can’t offer a sensible string. For example, what should a string representation of a FileStream or a Hashtable object look like?

All types that want to offer a reasonable way to obtain a string representing the current value of the object should override the ToString method. Many of the core types built into the FCL (Byte, Int32, UInt64, Double, and so on) override their ToString method and return a culturally aware string. In the Visual Studio debugger, a datatype is displayed when the mouse is placed over a particular variable. The text shown in the datatip is obtained by calling the object’s ToString method. So, when you define a class, you should always override the ToString method so that you get good debugging support.

### Specific Formats and Cultures

The parameterless ToString method has two problems. First, the caller has no control over the formatting of the string. For example, an application might want to format a number into a currency string, decimal string, percent string, or hexadecimal string. Second, the caller can't easily choose to format a string by using a specific culture. This second problem is more troublesome for server-side application code than for client-side code. On rare occasions, an application needs to format a string by using a culture other than the culture associated with the calling thread. To have more control over string formatting, you need a version of the ToString method that allows you to specify precise formatting and culture information.

Types that offer the caller a choice in formatting and culture implement the System.IFormattable interface.

```csharp
public interface IFormattable {
    String ToString(String format, IFormatProvider formatProvider);
}
```

In the FCL, all of the base types (Byte, SByte, Int16/UInt16, Int32/UInt32, Int64/UInt64, Single, Double, Decimal, and DateTime) implement this interface. In addition, some other types, such as Guid, implement it. Finally, every enumerated type definition will automatically implement the IFormattable interface so that a meaningful string symbol from an instance of the enumerated type can be obtained.

IFormattable's ToString method takes two parameters. The first, format, is a string that tells the method how the object should be formatted. ToString's second parameter, formatProvider, is an instance of a type that implements the System.IFormatProvider interface. This type supplies specific culture information to the ToString method. I'll discuss how shortly.

The type implementing the IFormattable interface's ToString method determines which format strings it's going to recognize. If you pass a format string that the type doesn't recognize, the type is supposed to throw a System.FormatException.

Many of the types Microsoft has defined in the FCL recognize several formats. For example, the DateTime type supports "d" for short date, "D" for long date, "g" for general, "M" for month/day, "s" for sortable, "t" for long time, "u" for universal time in ISO 8601 format, "U" for universal time in full date format, "Y" for year/month, and others. All enumerated types support "G" for general, "F" for flags, "D" for decimal, and "X" for hexadecimal. I'll cover formatting enumerated types in more detail in Chapter 15, "Enumerated Types and Bit Flags."

Also, all of the built-in numeric types support "C" for currency, "D" for decimal, "E" for exponential (scientific) notation, "F" for fixed-point, "G" for general, "N" for number, "P" for percent, "R" for round-trip, and "X" for hexadecimal. In fact, the numeric types also support picture format strings just in case the simple format strings don't offer you exactly what you're looking for. Picture format strings contain special characters that tell the type's ToString method exactly how many digits to
