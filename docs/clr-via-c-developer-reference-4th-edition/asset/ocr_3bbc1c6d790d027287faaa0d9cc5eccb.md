type instance. Furthermore, the C# compiler allows you to explicitly cast instances of an enumerated type to a different enumerated type. You can also explicitly cast an enumerated type instance to a numeric type.

Given an instance of an enumerated type, it's possible to map that value to one of several string representations by calling the ToString inherited from System.Enum.

```
Color c = Color.Blue;
Console.WriteLine(c);               // "Blue" (General format)
Console.WriteLine(c.ToString());      // "Blue" (General format)
Console.WriteLine(c.ToString("G"));   // "Blue" (General format)
Console.WriteLine(c.ToString("D"));   // "3" (Decimal format)
Console.WriteLine(c.ToString("X"));   // "03" (Hex format)
```

When using hex formatting, ToString always outputs uppercase letters. The number of digits output depends on the enum's underlying type: 2 digits for byte/sbyte, 4 digits for short/ushort, 8 digits for int/uint, and 16 digits for long/ulong. Leading zeros are output if necessary.

In addition to the ToString method, the System.Enum offers a static Format method that you call to format an enumerated type's value.

```
public static String Format(Type enumType, Object value, String format);
```

Generally, I prefer to call the ToString method because it requires less code and its easier to call. By using Format has one advantage over ToString: Format passes you a numeric value for the value parameter; you don't have to have an instance of the enumerated type. For example, the following code will display "Blue".

```
// The following line displays "Blue".
Console.WriteLine(Enum.Format(typeof(Color), (Byte)3, "G"));
```

> It is possible to declare an enumerated type that has multiple symbols, all with the same numeric value. When converting a numeric value to a symbol by using general formatting, Enum's methods return one of the symbols. However, there's no guarantee of which symbol name is returned. Also, if no symbol is defined for the numeric value you're looking up, a string containing the numeric value is returned.

It's also possible to call System.Enum's static GetValues method or System.type GetEnumValues to obtain an array contains one element for each symbolic name in an enumerated type; each element contains the symbolic name's numeric value.

```
public static Array GetValues(Type enumType);   // Defined in System.Enum
public Array GetEnumValues();               // Defined in System.Type
```