| DATA TYPE | MEANING | RANGE |
|---|---|---|
| ushort | Unsigned short integer | 0 to 65,535 |
| int | Integer | -2,147,483,648 to 2,147,483,647 |
| uint | Unsigned integer | 0 to 4,294,967,295 |
| long | Long integer | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| ulong | Unsigned long integer | 0 to 18,446,744,073,709,551,615 |
| float | Floating point | Roughly -3.4e38 to 3.4e38 |
| double | Double-precision floating point | Roughly -1.8e308 to 1.8e308 |
| decimal | Higher precision and smaller range than floating-point types | See the following section, "Float, Double, and Decimal Data Types." |
| char | Character | A single Unicode character. (Unicode characters use 16 bits to hold data for text in scripts such as Arabic, Cyrillic, Greek, and Thai, in addition to the Roman alphabet.) |
| string | Text | A string of Unicode characters. |
| bool | Boolean | Can be true or false. |
| object | An object | Can point to almost anything. |

Some of these data types are a bit confusing but the most common data types (int, long, float, double, and string) are fairly straightforward, and they are the focus of most of this lesson. Before moving on to further details, however, it's worth spending a little time comparing the float, double, and decimal data types.

# Float, Double, and Decimal Data Types

The computer represents values of every type in binary using bits and bytes, so some values don't fit perfectly in a particular data type. In particular, real numbers such as 1/7 don't have exact binary representations, so the float, double, and decimal data types often introduce slight rounding errors.

For example, a float represents 1/7 as approximately 0.142857149. Usually the fact that this is not exactly 1/7 isn't a problem, but once in a while if you compare two float values to see if they are exactly equal, roundoff errors can make them appear different even though they should be the same.

The decimal data type helps reduce this problem for decimal values such as 1.5 (but not non-decimal real values such as 1/7) by storing an exact representation of a decimal value. Instead of storing a value as a binary number the way float and double do, decimal stores the number's digits and its exponent separately as integral data types with no rounding. That lets it hold 28 or 29 significant digits (depending on the exact value) for numbers between roughly -7.9e28 and 7.9e28.