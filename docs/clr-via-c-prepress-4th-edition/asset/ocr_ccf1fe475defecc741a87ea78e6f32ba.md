```
```csharp
Console.WriteLine("{0,5:D}\t{0:G}", c);
}
```
```

The previous code produces the following output:

```
```
Number of symbols defined: 5
Value   Symbol
-----   ------
  0     White
  1     Red
  2     Green
  3     Blue
  4     Orange
```
```

Personally, I don’t like the GetValues and GetEnumValues methods because they both return an Array, which I then have to cast to the appropriate array type. So, I always define my own method:

```
```csharp
public static TEnum[] GetEnumValues<TEnum>() where TEnum : struct
{
    return (TEnum[])Enum.GetValues(typeof(TEnum));
}
```
```

With my generic GetEnumValues method, I can get better compile-time type-safety and simplify the first line of code in the previous example to this:

```
```csharp
Color[] colors = GetEnumValues<Color>();
```
```

This discussion shows some of the cool operations that can be performed on enumerated types. I suspect that the ToString method with the general format will be used quite frequently to show symbolic names in a program’s user interface elements (list boxes, combo boxes, and the like), as long as the strings don’t need to be localized (since enumerated types offer no support for localization). In addition to the GetValues method, the System.Enum type and the System.Type type also offer the following methods that return an enumerated type’s symbols:

```
```csharp
// Returns a String representation for the numeric value
public static String GetName(Type enumType, Object value);    // Defined in System.Enum
public          String GetEnumName(Object value);              // Defined in System.Type

// Returns an array of Strings: one per symbol defined in the enum
public static String[] GetNames(Type enumType);                // Defined in System.Enum
public          String[] GetNames();                           // Defined in System.Type
```
```

I’ve discussed a lot of methods that you can use to look up an enumerated type’s symbol. But you also need a method that can look up a symbol’s equivalent value, an operation that could be used to convert a symbol that a user enters into a text box, for example. Converting a symbol to an instance of an enumerated type is easily accomplished by using one of Enum’s static Parse and TryParse methods:

```
```csharp
public static Object Parse(Type enumType, String value);
public static Object Parse(Type enumType, String value, Boolean ignoreCase);
public static Boolean TryParse<TEnum>(String value, out TEnum result) where TEnum : struct;
public static Boolean TryParse<TEnum>(String value, Boolean ignoreCase, out TEnum result)
```
```