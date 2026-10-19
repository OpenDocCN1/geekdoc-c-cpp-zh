# ISO/IEC 14882:2020(E)

Table 100: Meaning of parse flags (continued)

| Flag | Parsed value |
|---|---|
| %M | The minutes as a decimal number. The modified command %N M specifies the maximum number of characters to read. If N is not specified, the default is 2. Leading zeroes are permitted but not required. The modified command %O M interprets the locale’s alternative representation. |
| %n | Matches one white space character.
[Note 1: %n, %t, and a space can be combined to match a wide range of white-space patterns. For example, "%n " matches one or more white space characters, and "%n%t%x" matches one to three white space characters. — end note] |
| %p | The locale’s equivalent of the AM/PM designations associated with a 12-hour clock. |
| %r | The locale’s 12-hour clock time. |
| %R | Equivalent to %H:%M. |
| %S | The seconds as a decimal number. The modified command %N S specifies the maximum number of characters to read. If N is not specified, the default is 2 if the input time has a precision convertible to seconds. Otherwise the default width is determined by the decimal precision of the input and the field is interpreted as a long double in a fixed format. If encountered, the locale determines the decimal point character.
Leading zeroes are permitted but not required. The modified command %O S interprets the locale’s alternative representation. |
| %t | Matches zero or one white space characters. |
| %T | Equivalent to %H:%M:%S. |
| %u | The ISO weekday as a decimal number (1-7), where Monday is 1. The modified command %N u specifies the maximum number of characters to read. If N is not specified, the default is 1. Leading zeroes are permitted but not required. |
| %U | The week number of the year as a decimal number. The first Sunday of the year is the first day of week 01. Days of the same year prior to that are in week 00. The modified command %N U specifies the maximum number of characters to read. If N is not specified, the default is 2. Leading zeroes are permitted but not required. The modified command %O U interprets the locale’s alternative representation. |
| %V | The ISO week-based week number as a decimal number. The modified command %N V specifies the maximum number of characters to read. If N is not specified, the default is 2. Leading zeroes are permitted but not required. |
| %w | The weekday as a decimal number (0-6), where Sunday is 0. The modified command %N w specifies the maximum number of characters to read. If N is not specified, the default is 1. Leading zeroes are permitted but not required. The modified command %O w interprets the locale’s alternative representation. |
| %W | The week number of the year as a decimal number. The first Monday of the year is the first day of week 01. Days of the same year prior to that are in week 00. The modified command %N W specifies the maximum number of characters to read. If N is not specified, the default is 2. Leading zeroes are permitted but not required. The modified command %O W interprets the locale’s alternative representation. |
| %x | The locale’s date representation. The modified command %E x interprets the locale’s alternate date representation. |
| %X | The locale’s time representation. The modified command %E X interprets the locale’s alternate time representation. |
| %y | The last two decimal digits of the year. If the century is not otherwise specified (e.g. with %C), values in the range [69, 99] are presumed to refer to the years 1969 to 1999, and values in the range [00, 68] are presumed to refer to the years 2000 to 2068. The modified command %N y specifies the maximum number of characters to read. If N is not specified, the default is 2. Leading zeroes are permitted but not required. The modified commands %E y and %O y interpret the locale’s alternative representation. |
| %Y | The year as a decimal number. The modified command %N Y specifies the maximum number of characters to read. If N is not specified, the default is 4. Leading zeroes are permitted but not required. The modified command %E Y interprets the locale’s alternative representation. |