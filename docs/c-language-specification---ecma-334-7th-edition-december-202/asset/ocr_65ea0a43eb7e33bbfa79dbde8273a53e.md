| Format Specifier | Description |
|---|---|
|  | Values are formatted using fixed-point format if *exponent* < precision specifier, where *exponent* is the exponent of the value in scientific format. For all other values, scientific format is used.

If the precision specifier is omitted, a default precision equal to the field width required to display the maximum value for the data type is used, which results in the value being formatted in fixed-point format. The default precisions for integral types are as follows:

`System.Int16, System.UInt16 : 5`
`System.Int32, System.UInt32 : 10`
`System.Int64, System.UInt64 : 19`

For Single, Decimal and Double types:

Values are formatted using fixed-point format if *exponent* ≥ -4 and *exponent* < precision specifier, where *exponent* is the exponent of the value in scientific format. For all other values, scientific format is used. Results are rounded to the nearest representable value when necessary.

If the precision specifier is omitted, the following default precisions are used:

`System.Single : 7`
`System.Double : 15`
`System.Decimal : 29`

For all types:
- The number of digits that appear in the result (not including the exponent) will not exceed the value of the precision specifier; values are rounded as necessary.
- The decimal point and any trailing zeros after the decimal point are removed whenever possible.
- The case of the format specifier ('G' or 'g') determines whether 'E' or 'e' prefixes the scientific format exponent. |
| N
n | **Number Format:** Used for strings in the following form:

`[-]d,ddd,ddd.dd...d`

The representation of negative values is determined by the `System.Globalization.NumberFormatInfo.NumberNegativePattern` property. If the pattern includes a negative number symbol ('-'), this symbol is supplied by the `System.Globalization.NumberFormatInfo.NegativeSign` property.

At least one non-zero decimal digit (*d*) precedes the decimal separator ('.'), which is supplied by the `System.Globalization.NumberFormatInfo.NumberDecimalSeparator` property. Digits between the decimal point and the most significant digit in the value are grouped using the group size specified by the `System.Globalization.NumberFormatInfo.NumberGroupSizes` property. The group |