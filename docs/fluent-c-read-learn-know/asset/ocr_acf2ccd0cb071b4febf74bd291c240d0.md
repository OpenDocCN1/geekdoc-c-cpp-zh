# # THE DECIMAL TYPE

Like a floating point number, the .NET Framework Decimal is also used to store real numbers, but it is less likely to suffer from the rounding errors that plague floating points. Unfortunately, it's also huge, and not as efficient as floating points. It is most often used to represent currency values, and it exposes a set of methods that are useful in that context: Ceiling(), Floor() and FromOCurrency().

In addition, the Decimal type has four different versions of the Round() method that provide precise control over how rounding occurs, and a Truncate() method that ignores the fractional component completely:

Round(value) returns the nearest integer value. If value is half way between two integers, the even number is returned. This is known as Banker's Rounding, or Rounding To Even.

Round(value, places) returns the value rounded to the specified number of decimal places, using Rounding To Even.

Round(value, MidpointRounding) returns the value rounded to the nearest integer using the specified member of the MidPointRounding enumeration, which has two values: ToEven and AwayFromZero.

Round(value, places, MidpointRounding) rounds values to the specified number of decimal places, using the specified rounding method.

Truncate(value) simply discards the fractional component.

# ## INITIALIZING DECIMAL VALUES

Like any value type, decimals can be initialized by assigning them a value directly. Constructors exist for Single, Double, Int32, UInt32, Int64 and UInt64 values. The Decimal also supports a constructor that allows you to specify each component of the number individually, which can sometimes be clearer:

```
```
Decimal(Int32 lowBits, Int32 midBits, Int32 hiBits, Boolean isNegative, Byte Scale)
```
```