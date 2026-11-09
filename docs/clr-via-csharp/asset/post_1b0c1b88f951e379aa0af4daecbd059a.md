
## Specific Formats and Cultures

The parameterless **ToString** method has two problems. First, the caller has no control over the formatting of the string. For example, an application might want to format a number into a currency string, decimal string, percent string, or hexadecimal string. Second, the caller can’t easily choose to format a string by using a specific culture. This second problem is more troublesome for server-side application code than for client-side code. On rare occasions, an application needs to format a string by using a culture other than the culture associated with the calling thread. To have more control over string formatting, you need a version of the **ToString** method that allows you to specify precise formatting and culture information.

Types that offer the caller a choice in formatting and culture implement the **System.IFormattable** interface:

```csharp
public interface IFormattable {
    String ToString(String format, IFormatProvider formatProvider);
}
```

In the FCL, all of the base types (**Byte**, **SByte**, **Int16/UInt16**, **Int32/UInt32**, **Int64/UInt64**, **Single**, **Double**, **Decimal**, and **DateTime**) implement this interface. In addition, some other types, such as **Guid**, implement it. Finally, every enumerated type definition will automatically implement the **IFormattable** interface so that a meaningful string symbol from an instance of the enumerated type can be obtained.

**IFormattable**’s **ToString** method takes two parameters. The first, **format**, is a string that tells the method how the object should be formatted. **ToString**’s second parameter, **formatProvider**, is an instance of a type that implements the **System.IFormatProvider** interface. This type supplies specific culture information to the **ToString** method. I’ll discuss how shortly.

The type implementing the **IFormattable** interface’s **ToString** method determines which format strings it’s going to recognize. If you pass a format string that the type doesn’t recognize, the type is supposed to throw a **System.FormatException**.

Many of the types Microsoft has defined in the FCL recognize several formats. For example, the **DateTime** type supports “d” for short date, “D” for long date, “g” for general, “M” for month/day, “s” for sortable, “T” for long time, “u” for universal time in ISO 8601 format, “U” for universal time in full date format, “Y” for year/month, and others. All enumerated types support “G” for general, “F” for flags, “D” for decimal, and “X” for hexadecimal. I’ll cover formatting enumerated types in more detail in Chapter 15, “Enumerated Types and Bit Flags.”

Also, all of the built-in numeric types support “C” for currency, “D” for decimal, “E” for exponential (scientific) notation, “F” for fixed-point, “G” for general, “N” for number, “P” for percent, “R” for round-trip, and “X” for hexadecimal. In fact, the numeric types also support picture format strings just in case the simple format strings don’t offer you exactly what you're looking for. Picture format strings contain special characters that tell the type's **ToString** method exactly how many digits to show, exactly where to place a decimal separator, exactly how many digits to place after the decimal separator, and so on. For complete information about format strings, see "Formatting Types" in the .NET Framework SDK.

For most types, calling **ToString** and passing **null** for the format string is identical to calling **ToString** and passing "G" for the format string. In other words, objects format themselves using the "General format" by default. When implementing a type, choose a format that you think will be the most commonly used format; this format is the "General format." By the way, the **ToString** method that takes no parameters assumes that the caller wants the "General format."

So now that format strings are out of the way, let's turn to culture information. By default, strings are formatted using the culture information associated with the calling thread. The parameterless **ToString** method certainly does this, and so does **IFormattable's ToString** if you pass **null** for the **formatProvider** parameter.

Culture-sensitive information applies when you're formatting numbers (including currency, integers, floating point, percentages, dates, and times). The **Guid** type has a **ToString** method that returns only a string representing its value. There's no need to consider a culture when generating the **Guid's** string because GUIDs are used for programmatic purposes only.

When formatting a number, the **ToString** method sees what you've passed for the **formatProvider** parameter. If **null** is passed, **ToString** determines the culture associated with the calling thread by reading the **System.Threading.Thread.CurrentThread.CurrentCulture** property. This property returns an instance of the **System.Globalization.CultureInfo** type.

Using this object, **ToString** reads its **NumberFormat** or **DateTimeFormat** property, depending on whether a number or date/time is being formatted. These properties return an instance of **System.Globalization.NumberFormatInfo** or **System.Globalization.DateTimeFormatInfo**, respectively. The **NumberFormatInfo** type defines a bunch of properties, such as **CurrencyDecimalSeparator**, **CurrencySymbol**, **NegativeSign**, **NumberGroupSeparator**, and **PercentSymbol**. Likewise, the **DateTimeFormatInfo** type defines an assortment of properties, such as **Calendar**, **DateSeparator**, **DayNames**, **LongDatePattern**, **ShortTimePattern**, and **TimeSeparator**. **ToString** reads these properties when constructing and formatting a string.

When calling **IFormattable's ToString** method, instead of passing **null**, you can pass a reference to an object whose type implements the **IFormatProvider** interface:

```csharp
public interface IFormatProvider {
    Object GetFormat(Type formatType);
}
```

Here’s the basic idea behind the **`IFormatProvider`** interface: when a type implements this interface, it is saying that an instance of the type is able to provide culture-specific formatting information and that the culture information associated with the calling thread should be ignored.

The **`System.Globalization.CultureInfo`** type is one of the very few types defined in the FCL that implements the **`IFormatProvider`** interface. If you want to format a string for, say, Vietnam, you’d construct a **`CultureInfo`** object and pass that object in as **`ToString`**’s **`formatProvider`** parameter. The following code obtains a string representation of a **`Decimal`** numeric value formatted as currency appropriate for Vietnam:

```csharp
Decimal price = 123.54M;
String s = price.ToString("C", new CultureInfo("vi-VN"));
MessageBox.Show(s);
```

If you build and run this code, the message box shown in Figure 14-5 appears.

![](img/3c46ff5b170881db4209d365b1f7a808_370_0.png)

**FIGURE 14-5** Numeric value formatted correctly to represent Vietnamese currency

Internally, **`Decimal`**’s **`ToString`** method sees that the **`formatProvider`** argument is not **`null`** and calls the object’s **`GetFormat`** method as follows:

```csharp
NumberFormatInfo nfi = (NumberFormatInfo)
    formatProvider.GetFormat(typeof(NumberFormatInfo));
```

This is how **`ToString`** requests the appropriate number-formatting information from the (**`CultureInfo`**) object. Number types (such as **`Decimal`**) request only number-formatting information. But other types (such as **`DateTime`**) could call **`GetFormat`** like this:

```csharp
DateTimeFormatInfo dtfi = (DateTimeFormatInfo)
    formatProvider.GetFormat(typeof(DateTimeFormatInfo));
```

Actually, because **`GetFormat`**’s parameter can identify any type, the method is flexible enough to allow any type of format information to be requested. The types in the **`.NET Framework`** call **`GetFormat`**, requesting only number or date/time information; in the future, other kinds of formatting information could be requested.
