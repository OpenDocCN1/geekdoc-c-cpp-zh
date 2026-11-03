You're probably surprised that the output doesn't look like this:

```
The value %d is an integer.
The value %f is a float.
```

It doesn't, because the text included in a printf() function isn't merely text — it's a formatting string.

The printf() function's formatting string can contain plain text, escape sequences, and conversion characters, such as the %d in Line 5 and the %f in Line 6. These conversion characters act as placeholders for values and variables (arguments) that follow the formatting string.

For the %d placeholder, the integer value 986 is substituted. The %d conversion character represents decimal integer values.

For the %f placeholder, the float value 98.6 is substituted. The %f conversion character represents floating-point values. Of course, 98.6 isn't displayed. Instead, you see 98.600000. This issue is addressed in the later section "Minding the extra zeros."

The %d and %f are only two of many placeholders for the printf() function's formatting string. The rest are covered in Chapter 7.

# Exercise 5-2: Create a project that uses the appropriate conversion characters, either %d or %f, in a printf() function to display the following values:

+   - 127
+   - 3.1415926535
+   - 122013
+   - 0.00008

![](bbox=[0.15, 0.75, 0.25, 0.9])

Do not type a comma when specifying a value in your C language source code.

When typing a small floating-point value, remember to prefix the decimal point with a zero, as just shown, with 0.00008. Likewise, when typing a float value without a decimal part, type the decimal and a zero anyway:

```
1000000.0
```