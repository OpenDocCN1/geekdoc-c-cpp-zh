
```cpp
for (Entry ee; cin>>ee; )
cout << ee << "\n";
// read from cin ee
// write ee to cout
```

The output is:

Click here to code image

"John Marwood Cleese, 123456\n\"Michael Edward Palin, 987654"

See §10.4 for a more systematic tranche for recognizing patterns in streams of characters (regular expression matching).

# 11.6 Output Formatting

The iostream and format libraries provide operations for controlling the format of input and numbers. The iostream facilities are as old as C++ and focus on streaming of numbers. The format facilities (§11.6.2) are recent (C++20) and focus on printf()-style (§11.8) specification of the formatting of combinations of values. Output formatting also supports unicode, but that’s beyond the scope of this book.

## 11.6.1 Stream Formatting

The simplest controls are called manipulators and are found in <ios>, <iostream>, <ostream>, and <iomanip> (for manipulators that take arguments). For example, we can output integers as decimal (the default), oct, or hexadecimal numbers:

Click here to code image

```cpp
cout << 1234 << " hex " << 1234 << " ' ' << oct << dec << 1234 << "\n"; // 1234 4d2 2322 1234
```

We can specify the format for floating-point numbers:

Click here to code image

```cpp
constexpr double d = 123456;
```

| cout << d << " , " | // use the default format for d |
| << scientific << d << " , " | // use 1.234e6 style format for d |
| << hexfloat << d << " , " | // use hexadecimal notation for d |
| << fixed << d << " , " | // use 123.456 style format for d |
| << default << d << "\n"; | // use the default format for d |

This produces:

Click here to code image

123.456; 1.23456e+002; 0xedd2f2p6; 123.456000; 123.456

Precision is an integer that determines the number of digits used to display a floating-point number:

- The general format (defaultfloat) lets the implementation choose a format that presents a value in the style that best preserves the value in available. The precision specifies the maximum number of digits.
- The scientific format (scientific) presents a value with one digit before a decimal point and an exponent. The precision specifies the maximum number of digits after the decimal point.
- The fixed format (fixed) presents a value as an integer part followed by a decimal point and a fractional part. The precision specifies the maximum number of digits after the decimal point.

Floating-point values are rounded rather than just truncated, and precision() doesn't affect integer output. For example:

Click here to view code image

```cpp
out.precision(8);
out << "precision(8):" << 123.56789 << ' ' << 123.56789 << ' ' << 123456 << endl;

out.precision(4);
out << "precision(4):" << 123.56789 << ' ' << 123.56789 << ' ' << 123456 << endl;
cout << 123.56789 << endl;
```

This produces:

Click here to view code image

precision(8): 123.56789 123456
precision(4): 123.5679 12345
1235

These floating-point manipulators are "sticky"; they have effects for subsequent floating-point operations. That is, they are designed for formatting streams of values. We can also specify the size of the field that a number is to be placed into and its alignment in that field.

In addition to the basic numbers, << can also handle time and dates: duration, time_point, month_date, weekday, month, and zoned_time (§16.2). For example:

Click here to code image

```cpp
cout << "birthday: " << 2021/11/28 << endl;
cout << "zt: " << zoned_time(system_clock::now()) << endl;
```

This produces:

birthday: 2021/11/28
zt: 2021-11-28 03:59:4638

The standard also defines for complex numbers, bitsets, and pointers. Stream I/O is extensible, so we can define our own user-defined types.

## 11.6.2 printf()-style Formatting

It has been widely argued that printf() is the most popular function in C and a significant factor in its success. For example:

Click here to code image

```cpp
printf("%g%s\n", "Hello");
```

Format string followed by -style was adopted into C++ and has always suffered from lack of safety and extensibility to handle user-defined types. In <format>, the standard library provides a type-safe, extensible mechanism. The basic function format() produces a string; "Ordinary characters" in the format string are simply put into the output. The simplest format is {}, which takes the next argument and inserts it into the string. So, if val is "World", we get "Hello, World". To see how this works, let's repeat the examples from:

Click here to code image

```cpp
cout << format("{:x}: {:o}: {:d}", 1234, 1234, 1234);
```

This gives the same output as the integer example in §11.6.1, except that b for binary is not directly supported by ostream. A formatting directive is preceded by a colon. The integer formatting alternatives are x for hexadecimal, o for octal, d for decimal, and b for binary. By default, format takes its arguments in order. However, we can specify an arbitrary order. For example:

Click here to code image

```cpp
cout << format("{:3}: {:1}: {:2}", 000, 111, 222);
```

This prints 333. The number before the colon is the number of the argument to be formatted. In C++, the numbering starts at zero. This allows us to format more than one:

```cpp
cout << format("{:0x}: {:0o}: {:0d}", 1234); // If default, hexadecimal, octal, decimal, binary
```

The ability to place arguments into the output "out of order" is highly praised by people composing messages in different natural languages. Floating-formats are the same as ostream: e for scientific, a for hexfloat, f for fixed, and g for default. For example:

Click here to code image

```cpp
cout << format("{0:e}; {0:a}; {0:f}; {0:g}", 123456); // default, scientific, hexfloat, fixed, default
```

The result was identical to ostream except that the hexadecimal number was not preceded by 0x:

Click here to code image

```cpp
123456; 1.234560e+002; 1.2eddf2p+6; 123456000; 123456
```

A dot precedes a precision specifier:

Click here to view code image

```cpp
cout << format("{0:8} {} {0n}", 1234.56789, 1234.56789, 123456);
cout << format("{0:precision(4):-4f}", 1234.56789, 1234.56789, 123456);
cout << format("{0:0n}", 1234.56789);
```

Unlike ostream, formatters are not "sticky": so you can

Click here to view code image

```
precision(8): 1234.56789 1234.56789 123456
precision(4): 1235 1234.56789 123456
123456789
```

As with stream formatters, you can also specify the size of the field where a number is to be placed and its alignment in that field. Like stream formatters, format can also handle time and dates (§16.2) for example:

Click here to view code image

```cpp
auto ymd = 2021/March/30;
cout << format("{{0:ymd}}: {0:%A}, {0:%B} {0:%d}, {0:%Y}", ymd.month(), ymd.day(), ymd.year()); //
```

This produced:

ymd: Tuesday, March 30, 2021

The default formatting of values is identical to that of stream formatting. However, format provides a mini-language of about 60 format specifiers allowing very detailed control over formatting of numbers and dates. All time and date format strings start with %.

The flexibility offered by the many format specifiers can be important, but it comes with many opportunities for mistakes. Some specifiers come with optional or locale dependent semantics. If a formatting error is caught at runtime, a format_error exception is thrown. For example:

Click here to view code image
