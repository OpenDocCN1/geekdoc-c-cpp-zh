# 10 Data and Types

# 5.3 Conversion

For a given type there may exist an implicit or explicit conversion of type ts into a value of another type tt. If there is an implicit conversion from type ts to type tt, then an expression of type ts can be used wherever an expression of type tt is expected. In particular, any v of type ts may be bound to a variable or field of type tt, for instance, by the assignment x = v.

If there is an explicit conversion from ts to tt, then a cast expression (section 12.20) can be used to obtain a value of type tt from the value of type ts.

# 5.3.1 Standard Conversions between Simple Types

The standard conversions between simple types are shown in the table below. There are standard conversions between all the simple types except

+   A conversion marked I is an implicit conversion (no cost required), and one marked E is an explicit conversion (cost required). More precisely, an implicit conversion cannot lose precision, whereas one marked IL lose precision; neither can throw.

+   An explicit marked ER rounds the source value and so lose precision or produce an infinity, but it has no exception. An explicit marked ET truncates the source value to the nearest integer number (rounds toward zero); in a checked context (section 12.3) it throws OverflowException if the result is too large, and in an unchecked context it produces an unspecified value of the target type. An explicit marked ED rounds the source value, and throws OverflowException if the source value is too large or a NaN.

+   Finally, an explicit marked EB works on the bit representing the source value. In a checked context (section 12.3) the conversion throws OverflowException if the source value is larger than the target type (in bits; see page 7), in an unchecked context no exception is thrown. If, the source is larger than the target type, the most significant bits are discarded from the source value. If the source type is smaller than the target type, the source value is padded (extended with most significant bits) to fit the target type, padding with the sign bit if the type is signed, and with zeros if it is unsigned.

| Source Type | Target Type (tt) |
|---|---| char byte short uint int long float double decimal |
| char | I | EB | EB | I | EB | EB | I | I | I | I | I |
| sbyte | EB | EB | I | EB | I | EB | EB | I | I | I |
| byte | EB | EB | I | I | EB | I | EB | I | I | I | I |
| short | EB | EB | EB | I | EB | EB | I | I | I | I |
| ushort | INT | EB | EB | EB | EB | I | EB | EB | IL | I |
| uint | EB | EB | EB | EB | I | I | I | I | I | I |
| long | EB | EB | EB | EB | EB | EB | IL | IL | I |
| ulong |long | EB | EB | EB | EB | EB | EB | IL | I |
 |
| float | ET | ET | ET | ET | ET | ET | ET | I | I | ED |
| double | ET | ET | ET | ET | ET | ET | ET | ER | ED |
| decimal | ET | ET | ET | ET | ET | ET | ET | ER | ER | I |