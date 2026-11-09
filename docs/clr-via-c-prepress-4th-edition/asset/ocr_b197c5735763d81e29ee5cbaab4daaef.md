For most types, calling `ToString` and passing `null` for the format string is identical to calling `ToString` and passing `"G"` for the format string. In other words, objects format themselves using the `"General format"` by default. When implementing a type, choose a format that you think will be the most commonly used format; this format is the `"General format."` By the way, the `ToString` method that takes no parameters assumes that the caller wants the `"General format."`

So now that format strings are out of the way, let's turn to culture information. By default, strings are formatted using the culture information associated with the calling thread. The parameterless `ToString` method certainly does this, and so does `IFormattable`'s `ToString` if you pass `null` for the `formatProvider` parameter.

Culture-sensitive information applies when you're formatting numbers (including currency, integers, floating point, percentages, dates, and times). The `Guid` type has a `ToString` method that returns only a string representing its value. There's no need to consider a culture when generating the `Guid`'s string because GUIDs are used for programmatic purposes only.

When formatting a number, the `ToString` method sees what you've passed for the `formatProvider` parameter. If `null` is passed, `ToString` determines the culture associated with the calling thread by reading the `System.Globalization.CultureInfo.CurrentCulture` property. This property returns an instance of the `System.Globalization.CultureInfo` type.

Using this object, `ToString` reads its `NumberFormat` or `DateTimeFormat` property, depending on whether a number or date/time is being formatted. These properties return an instance of `System.Globalization.NumberFormatInfo` or `System.Globalization.DateTimeFormatInfo`, respectively. The `NumberFormatInfo` type defines a bunch of properties, such as `CurrencyDecimalSeparator`, `CurrencySymbol`, `NegativeSign`, `NumberGroupSeparator`, and `PercentSymbol`. Likewise, the `DateTimeFormatInfo` type defines an assortment of properties, such as `Calendar`, `DateSeparator`, `DayNames`, `LongDatePattern`, `ShortTimePattern`, and `TimeSeparator`. `ToString` reads these properties when constructing and formatting a string.

When calling `IFormattable`'s `ToString` method, instead of passing `null`, you can pass a reference to an object whose type implements the `IFormatProvider` interface:

```
```csharp
public interface IFormatProvider {
    Object GetFormat(Type formatType);
}
```
```

Here's the basic idea behind the `IFormatProvider` interface: when a type implements this interface, it is saying that an instance of the type is able to provide culture-specific formatting information and that the culture information associated with the calling thread should be ignored.

The `System.Globalization.CultureInfo` type is one of the very few types defined in the FCL that implements the `IFormatProvider` interface. If you want to format a string for, say, Vietnam, you'd construct a `CultureInfo` object and pass that object in as `ToString`'s `formatProvider` parameter. The following code obtains a string representation of a `Decimal` numeric value formatted as currency appropriate for Vietnam: