This Parse method accepts three parameters. For convenience, many types offer additional overloads of Parse so you don't have to pass as many arguments. For example, Int32 offers four overloads of the Parse method.

```
// Parse NumberStyles.Integer for style
// and thread's culture's provider information.
public static Int32 Parse(String s);
```

```
// Parses thread's culture provider information.
public static Int32 Parse(String s, NumberStyles styles);
```

```
// Parse NumberStyles.Integer for the style parameter.
public static Int32 Parse(String s, IFormatProvider provider);
```

```
// This is the method I've been talking about in this section.
public static Int32 Parse(String s, NumberStyles styles,
IFormatProvider provider);
```

The DateTime type also offers a Parse method.

```
public static DateTime Parse(String s,
IFormatProvider provider, DateTime styles);
```

This method works just as the Parse method defined on the number types except that DateTime's Parse takes a set of bit flags defined by the System.Globalization.DateTimeStyles enumerated instead of the NumberStyles enumerated type. The .NET Framework SDK documentation for a complete description of the bit symbols and common the DateTimeStyles types.

For convenience, the DateTime type offers three overloads of the Parse method.

```
// Parses thread's culture's provider information
// and DateTimeStyles.None for the style
public static Int32 Parse(String s);
```

```
// Parses DateTimeStyles.None for the style
public static DateTime Parse(String s, IFormatProvider provider);
```

```
// This is the method I've been talking about in this section.
public static DateTime Parse(String s,
IFormatProvider provider, DateTimeStyles styles);
```

Parsing dates and times is complex. Many developers have found the Parse method of the DateTime too forgiving that it sometimes parses strings that don't contain dates or times. For this reason, the DateTime type also offers a ParseExact method that accepts a picture format string that indicates exactly how the date/time string should be formatted and how it should be parsed. For more information about picture format strings, see the DateTimeFormat class in the .NET SDK.