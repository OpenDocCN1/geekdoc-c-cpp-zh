
## Mutable Strings Using StringBuilder

Because strings are immutable, every time you perform any string manipulation, you create new temporary strings. To allow mutable strings to be created and manipulated without creating new strings, C# provides the `StringBuilder` class. Using string concatenation is preferred if a fixed number of strings will be concatenated. If an arbitrary number of strings will be concatenated, such as inside an iteration statement, a `StringBuilder` is preferred.

`StringBuilder` supports appending data to the end of the current string, inserting data at a specified position, replacing data, and removing characters from the current string. Appending data uses one of the overloads of either the `Append` or `AppendFormat` methods.

The `Append` method adds text or a string representation of an object to the end of the current string. The `AppendFormat` method supports adding text to the end of the current string by using composite formatting. Because `AppendFormat` uses composite formatting, you can pass it a format string, which you learn about in the next section.

Listing 8.7 shows the same example of joining and splitting strings shown in Listing 8.6 but uses a `StringBuilder` rather than a string array.

**LISTING 8.7 Using StringBuilder**

```csharp
StringBuilder stringBuilder = new StringBuilder();
for (int i = 0; i < 10; i++)
{
    stringBuilder.AppendFormat("{0}#", i * 2);
}

// Remove the trailing '#' character.
stringBuilder.Remove(stringBuilder.Length - 1, 1);

string joined = String.Join("#", stringBuilder.ToString());
Console.WriteLine(joined);

foreach (string word in joined.Split(new char[] { '#' }))
{
    Console.WriteLine(word);
}
```

To insert data, one of the `Insert` overloads should be used. When you insert data, you must provide the position within the current `StringBuilder` string where the insertion will begin. To remove data, you use the Remove method and indicate the starting position where the removal begins and the number of characters to remove.

The Replace method, or one of its overloads, can be used to replace characters within the current StringBuilder string with another specified character. The Replace method also supports replacing characters within a substring of the current StringBuilder string, specified by a starting position and length.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_198_0.png)

### StringBuilder Capacity

Internally, the *StringBuilder* string is maintained in a buffer to accommodate concatenation. The *StringBuilder* needs to allocate additional memory only if the buffer does not have enough room to accommodate the new data.

The default size, or capacity, for this internal buffer is 16 characters. When the buffer reaches capacity, additional buffer space is allocated for an additional amount of characters as specified by the *capacity*. *StringBuilder* also has a maximum capacity, which is *Int32.MaxValue*, or $2^{31}$, characters.

The length of the current string can be set using the *Length* property. By setting the *length* to a value that is larger than the current capacity, the capacity is automatically changed. Similarly, by setting the *Length* to a value that is less than the current capacity, the current string is shortened.

## Type Formatting

Formatting allows you to convert an instance of a class, structure, or enumeration value to a string representation. Every type that derives from *System.Object* automatically inherits a parameterless *ToString* method, which, by default, returns the name of the type. All the predefined value types have overridden *ToString* to return a general format for the type.

Because getting the name of the type from *ToString* isn't generally useful, you can override the *ToString* method and provide a meaningful string representation of your type. Listing 8.8 shows the *Contact* class overriding the *ToString* method.

**LISTING 8.8 Overriding ToString**

```csharp
class Contact
{
    private string firstName;
    private string lastName;

    public override string ToString()
    {
        return firstName + " " + lastName;
    }
}
```

### Overriding ToString

Before you start adding ToString overrides to all your classes, be aware that the Visual Studio debugging tools use ToString extensively to determine what values to display for an object when viewed through a debugger.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_199_0.png)

The value of an object often has multiple representations, and ToString enables you to pass a format string as a parameter that determines how the string representation should appear. A format string contains one or more format specifiers that define how the string representation should appear.

### Standard Format Strings

A standard format string contains a single format specifier, which is a single character that defines a more complete format string, and an optional precision specifier that affects the number of digits displayed in the result. If supported, the precision specifier can be any integer value from 0 to 99. All the numeric types, date and time types, and enumeration types support a set of predefined standard format strings, including a “G” standard format specifier, which represents a general string representation of the value.

The standard format specifiers are shown in Table 8.4.

**TABLE 8.4 Standard Format Specifiers**

| Format Specifier | Description |
| :--- | :--- |
| “G”, “g” | Represents a general string representation. |
|  | For all numeric types, results in the most compact of either fixed-point or exponential notation. The precision specifier indicates the number of significant digits. |
|  | For all date and time types, represents the general date/time pattern. “G” represents the long time pattern, whereas “g” is the short time pattern. |
|  | For enumeration types, displays the enumeration entry as a string value, if possible, and otherwise displays the integer value of the current instance. If the enumeration is defined with the Flags attribute set, the string values of each valid entry are concatenated together, separated by commas. If the Flags attribute is not set, an invalid value is displayed as a numeric entry. |
| "X", "x" | For integral types, results in a hexadecimal string. The precision specifier indicates the number of digits in the result string. |
|  | For enumeration types, displays the enumeration entry as a hexadecimal value. The value is represented with leading zeros as necessary, to ensure that the value is a minimum eight digits in length. |
| "D", "d" | For integral types, results in a string of integer digits with an optional negative sign. The precision specifier indicates the minimum number of digits. |
|  | For enumeration types, displays the enumeration entry as an integer value in the shortest representation possible. |
| "E", "e" | Supported only by numeric types. Results in the exponential notation representation of the value. The precision specifier indicates the number of decimal digits, and the default is 6. |
| "F", "f" | For all numeric types, results in a string of integral and decimal digits with an optional negative sign. The precision specifier indicates the number of decimal digits. |
|  | For date and time types, represents the full date/time pattern. “F” represents the long time pattern, whereas “f” is the short time pattern. |
|  | For enumeration types, displays the enumeration entry as a string value, if possible. If the value can be completely displayed as a summation of the entries in the enumeration (even if the Flags attribute is not present), the string values of each valid entry are concatenated together, separated by commas. If the value cannot be completely determined by the enumeration entries, the value is formatted as the integer value. |
| "N", "n" | Supported only by numeric types. Results in a string of integral and decimal digits, group separators, and a decimal separator with an optional negative sign. The precision specifier indicates the desired number of decimal places. |
| "P", "p" | Supported only by numeric types. Results in the number multiplied by 100 and displayed with a percent symbol. The precision specifier indicates the desired number of decimal places. |
