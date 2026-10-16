CultureInfo instance (code file NumberAndDateFormatting\Program.cs):

```
public static void NumberFormatDemo()
{
    int val = 1234567890;

    // culture of the current thread
    WriteLine(val.ToString("N"));

    // use IFormatProvider
    WriteLine(val.ToString("N", new CultureInfo("fr-FR")));

    // change the current culture
    CultureInfo.CurrentCulture = new CultureInfo("de-DE");
    WriteLine(val.ToString("N"));
}
```

> NOTE Before to .NET 4.6, the CurrentCulture property of the CultureInfo was read-only. With previous editions of .NET, you can set the culture using Thread .CurrentThread.CurrentCulture.

You can compare the following different output for U.S. English, French, and German, respectively, shown here:

```
1,234,567,890.00
1 234 567 890,00
1.234.567.890,00
```

# Date Formatting

The same support for numbers is available for dates. The DateTime structure has some overloads of the ToString method for date-to-string conversions. You can pass a string format and assign a different culture:

```
public string ToString();
public string ToString(IFormatProvider);
public string ToString(string);
public string ToString(string, IFormatProvider);
```

With the string argument of the ToString method, you can specify a predefined format character or a custom format string for converting the date to a string. The class DateTimeFormatInfo specifies the possible values. With DateTimeFormatInfo, the case of the format strings has a different meaning. D defines a long date format; d defines a short date format. Other examples of possible formats are ddd for the abbreviated day of the week, dddd for the full day of the week, yyyy for the year, T for a long time, and t for a short time. With the IFormatProvider argument, you can specify the culture. Using an overloaded method without the IFormatProvider argument implies that the current culture is used:

```
public static void DateFormatDemo()
{
    var d = new DateTime(2015, 09, 27);

    // current culture
    WriteLine(d.ToLongDateString());
```