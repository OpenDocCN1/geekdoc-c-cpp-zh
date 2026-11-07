
## Header File `cctype` (`ctype.h`)

The following table shows various functions from the header file `cctype` (`ctype.h`).

| Function Name and Parameters | Parameter(s) Types | Function Return Value |
|---|---|---|
| `isalnum(ch)` | ch is a `char` value | Function returns an `int` value as follows:<br>• If ch is a letter or a digit character, that is (`'A'–'Z'`, `'a'–'z'`, `'0'–'9'`), it returns a nonzero value (`true`)<br>• 0 (`false`), otherwise |
| `iscntrl(ch)` | ch is a `char` value | Function returns an `int` value as follows:<br>• If ch is a control character (in ASCII, a character value 0–31 or 127), it returns a nonzero value (`true`)<br>• 0 (`false`), otherwise |
| `isdigit(ch)` | ch is a `char` value | Function returns an `int` value as follows:<br>• If ch is a digit (`'0'–'9'`), it returns a nonzero value (`true`)<br>• 0 (`false`), otherwise |
| `islower(ch)` | ch is a `char` value | Function returns an `int` value as follows:<br>• If ch is lowercase (`'a'–'z'`), it returns a nonzero value (`true`)<br>• 0 (`false`), otherwise |
| `isprint(ch)` | ch is a `char` value | Function returns an `int` value as follows:<br>• If ch is a printable character, including blank (in ASCII, `' '` through `'~'`), it returns a nonzero value (`true`)<br>• 0 (`false`), otherwise |
| `ispunct(ch)` | ch is a `char` value | Function returns an `int` value as follows:<br>• If ch is a punctuation character, it returns a nonzero value (`true`)<br>• 0 (`false`), otherwise |
| `isspace(ch)` | ch is a `char` value | Function returns an `int` value as follows:<br>• If ch is a whitespace character (blank, newline, tab, carriage return, form feed), it returns a nonzero value (`true`)<br>• 0 (`false`), otherwise |
| `isupper(ch)` | `ch` is a `char` value | Function returns an `int` value as follows:<br>• If `ch` is an uppercase letter (`'A'–'Z'`), it returns a nonzero value (`true`)<br>• `0` (`false`), otherwise |
| `tolower(ch)` | `ch` is a `char` value | Function returns an `int` value as follows:<br>• If `ch` is an uppercase letter, it returns the ASCII value of the lowercase equivalent of `ch`<br>• ASCII value of `ch`, otherwise |
| `toupper(ch)` | `ch` is a `char` value | Function returns an `int` value as follows:<br>• If `ch` is a lowercase letter, it returns the ASCII value of the uppercase equivalent of `ch`<br>• ASCII value of `ch`, otherwise |

## Header File `cfloat` (`float.h`)

In Chapter 2, we listed the largest and smallest values belonging to the floating-point data types. We also remarked that these values are system dependent. These largest and smallest values are stored in named constants. The header file cfloat contains many such named constants. The following table lists some of these constants.

| Named Constant | Description |
|---|---|
| `FLT_DIG` | Approximate number of significant digits in a `float` value |
| `FLT_MAX` | Maximum positive `float` value |
| `FLT_MIN` | Minimum positive `float` value |
| `DBL_DIG` | Approximate number of significant digits in a `double` value |
| `DBL_MAX` | Maximum positive `double` value |
| `DBL_MIN` | Minimum positive `double` value |
| `LDBL_DIG` | Approximate number of significant digits in a `long double` value |
| `LDBL_MAX` | Maximum positive `long double` value |
| `LDBL_MIN` | Minimum positive `long double` value |

A program similar to the following can print the values of these named constants on your system.

```cpp
#include <iostream>
#include <cfloat>

using namespace std;

int main()
{
    cout << "Approximate number of significant digits "
         << "in a float value " << FLT_DIG << endl;
    cout << "Maximum positive float value " << FLT_MAX
         << endl;
    cout << "Minimum positive float value " << FLT_MIN
         << endl;
    cout << "Approximate number of significant digits "
         << "in a double value " << DBL_DIG << endl;
    cout << "Maximum positive double value " << DBL_MAX
         << endl;
    cout << "Minimum positive double value " << DBL_MIN
         << endl;
    cout << "Approximate number of significant digits "
         << "in a long double value " << LDBL_DIG << endl;
    cout << "Maximum positive long double value " << LDBL_MAX
         << endl;
    cout << "Minimum positive long double value " << LDBL_MIN
         << endl;

    return 0;
}
```

## Header File `climits` (`limits.h`)

In Chapter 2, we listed the largest and smallest values belonging to the integral data types. We also remarked that these values are system dependent. These largest and smallest values are stored in named constants. The header file `climits` contains many such named constants. The following table lists some of these constants.

| Named Constant | Description |
|---|---|
| `CHAR_BIT` | Number of bits in a byte |
| `CHAR_MAX` | Maximum char value |
| `CHAR_MIN` | Minimum char value |
| `SHRT_MAX` | Maximum short value |
| `SHRT_MIN` | Minimum short value |
| `INT_MAX` | Maximum `int` value |
| `INT_MIN` | Minimum `int` value |
| `LONG_MAX` | Maximum `long` value |
| `LONG_MIN` | Minimum `long` value |
| `UCHAR_MAX` | Maximum `unsigned char` value |
| `USHRT_MAX` | Maximum `unsigned short` value |
| `UINT_MAX` | Maximum `unsigned int` value |
| `ULONG_MAX` | Maximum `unsigned long` value |

A program similar to the following can print the values of these named constants on your system.

```cpp
#include <iostream>
#include <climits>

using namespace std;

int main()
{
    cout << "Number of bits in a byte " << CHAR_BIT << endl;
    cout << "Maximum char value " << CHAR_MAX << endl;
    cout << "Minimum char value " << CHAR_MIN << endl;
    cout << "Maximum short value " << SHRT_MAX << endl;
    cout << "Minimum short value " << SHRT_MIN << endl;
    cout << "Maximum int value " << INT_MAX << endl;
    cout << "Minimum int value " << INT_MIN << endl;
    cout << "Maximum long value " << LONG_MAX << endl;
    cout << "Minimum long value " << LONG_MIN << endl;
    cout << "Maximum unsigned char value " << UCHAR_MAX
         << endl;
    cout << "Maximum unsigned short value " << USHRT_MAX
         << endl;
    cout << "Maximum unsigned int value " << UINT_MAX << endl;
    cout << "Maximum unsigned long value " << ULONG_MAX
         << endl;

    return 0;
}
```

| Function Name and Parameters | Parameter(s) Type | Function Return Value |
|---|---|---|
| `sqrt(x)` | x is a floating-point expression, in which x ≥ 0.0 | Square root of x |
| `tan(x)` | x is a floating-point expression; x is measured in radians | Trigonometric tangent of the angle |
| `tanh(x)` | x is a floating-point expression | Hyperbolic tangent of x |

## Header File `cstddef` (`stddef.h`)

Among others, this header file contains the definition of the following symbolic constant:

`NULL`: The system-dependent null pointer (usually 0)

## Header File `cstring` (`string.h`)

The following table shows various string functions.

| Function Name and Parameters | Parameter(s) Type | Function Return Value |
|---|---|---|
| `strcat(destStr, srcStr)` | destStr and srcStr are null-terminated char arrays; destStr must be large enough to hold the result | The base address of destStr is returned; srcStr, including the null character, is concatenated to the end of destStr |
| `strcmp(str1, str2)` | str1 and str2 are null-terminated char arrays | The returned value is as follows:<br>- An int value < 0 if `str1 < str2`<br>- An int value 0 if `str1 = str2`<br>- An int value > 0 if `str1 > str2` |
| `strcpy(destStr, srcStr)` | `destStr` and `srcStr` are null-terminated `char` arrays | The base address of `destStr` is returned; `srcStr` is copied into `destStr` |
| `strlen(str)` | `str` is a null-terminated `char` array | An integer value ≥ 0 specifying the length of the `str` (excluding the `\0`) is returned |

## Header File `string`

This header file—not to be confused with the header file `cstring`—supplies a programmer-defined data type named `string`. Associated with the string type are a data type `string::size_type` and a named constant `string::npos`. These are defined as follows:

|  |  |
|---|---|
| `string::size_type` | An unsigned integer type |
| `string::npos` | The maximum value of type `string::size_type` |

The type `string` contains several functions for string manipulation. In addition to the string functions listed in Table 8-1, the following table describes additional string functions. In this table, we assume that `strVar` is a string variable and `str` is a string variable, a string constant, or a character array.

| Expression | Effect |
|---|---|
| `getline(istreamVar, strVar);` | `istreamVar` is an input stream variable (of type `istream` or `ifstream`). Characters until the newline character are input from `istreamVar` and stored in `strVar`. (The newline character is read but not stored into `strVar`.) The value returned by this function is usually ignored. |
| `strVar.append(str, n)` | The first n characters of the character array `str` are appended to `strVar`. |
| `strVar.c_str()` | The base address of a null-terminated C-string corresponding to the characters in `strVar`. |
