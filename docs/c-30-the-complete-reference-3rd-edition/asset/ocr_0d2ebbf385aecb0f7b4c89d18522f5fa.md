| Method | Meaning |
|---|---|
| public string ToString(IFormatProvider fmtpvd r) | Returns the string representation of the value of the invoking object using the culture-specific information specified in fmtpvd r. |
| public string ToString(string format, IFormatProvider fmtpvd r) | Returns the string representation of the value of the invoking object using the culture-specific information specified in fmtpvd r and the format specified by format. |
| public static ushort ToUInt16(decimal v) | Returns the ushort equivalent of v. Any fractional component is truncated. An OverflowException occurs if v is not within the range of a ushort. |
| public static uint ToUInt32(decimal v) | Returns the uint equivalent of v. Any fractional component is truncated. An OverflowException occurs if v is not within the range of a uint. |
| public static ulong ToUInt64(decimal v) | Returns the ulong equivalent of v. Any fractional component is truncated. An OverflowException occurs if v is not within the range of a ulong. |
| public static decimal Truncate(decimal v) | Returns the whole-number portion of v. Thus, it truncates any fractional digits. |
| public static bool TryParse(string str, out decimal val) | Attempts to convert the numeric string in str into a decimal value. If successful, the value is stored in val and true is returned. If no conversion takes place, false is returned. This differs from Parse(), which throws an exception on failure. |
| public static bool TryParse(string str, NumberStyles styles, IFormatProvider fmtpvd r, out decimal val) | Attempts to convert the numeric string in str into a decimal value using the style information provided by styles and the culture-specific format information provided by fmtpvd r. If successful, the value is stored in val and true is returned. If no conversion takes place, false is returned. This differs from Parse(), which throws an exception on failure. |

# Char

The structure corresponding to the char type is Char. It is quite useful because it supplies a large number of methods that allow you to process and categorize characters. For example, you can convert a lowercase character to uppercase by calling ToUpper(). You can determine if a character is a digit by calling IsDigit().

The methods defined by Char are shown in Table 21-9. Notice that several, such as ConvertFromUtf32() and ConvertToUtf32(), give you the ability to work with both UTF-16 and UTF-32 Unicode characters. In the past, all Unicode characters could be represented by 16 bits, which is the size of a char. However, a few years ago the Unicode character set was expanded and more than 16 bits are required. Each Unicode character is represented by a code point. The way that a code point is encoded depends on the Unicode Transformation Format (UTF) being used. In UTF-16, the most common code points require one 16-bit value, but some need two 16-bit values. When two 16-bit values are needed, two char