be dealt with in the chapter on arrays and strings. Moreover, the format string has some extra attributes to cope with the problems of reading and data writing, which are described below. However, almost all of the conversion specifiers, or format specifiers, listed in connection with `printf()` can be used with `scanf()` also.

As with `printf()`, the format string in `scanf()` is enclosed in a set of quotation marks and it may contain the following:

**White space**  This causes the input stream to be read up to the next non-white-space character.

**Ordinary character string**  Anything except white space or `%` characters. The next character in the input stream must match this character.

**Conversion specifier field**  This is a `%` character, followed by an optional `*` character, which suppresses the conversion, followed by an optional non-zero decimal integer specifying the maximum field width, an optional `h`, `l` or `L` to control the length of the conversion, and finally a non-optional conversion specifier. Note that the use of `h`, `l` or `L` will affect the type of pointer that must be used.

# Format specifiers in `scanf()`

The format string in `scanf()` has the following general form:

`< character string × % conversion specifier field >`

Here, character string is optional and has to be used with care. Each conversion specifier field is coded as follows:

`%[*][<width><size><conversion-code>]`

Each conversion (or format) specifier begins with the per cent character, `%`, after which come the following, in the given order.

+   1. An optional assignment-suppression character, `*`, which states that the value being read will not be assigned to an argument, but will be dropped.
+   2. An optional width specifier, `<width>`, which designates the maximum number of characters to be read that compose the value for the associated argument. Encountering white space, before the entire width is scanned, terminates the input of this value and moves to the next.
+   3. An optional conversion-code modifier, `<size>`, which modifies the conversion code to accept format for a type of:
+      - `h` = short int,
+      - `l` = long int, if the format specifiers provide for an integer conversion,
+      - `l` = double, if the format specifiers provide for a floating-point conversion, and
+      - `L` = long double, which is valid only with floating-point conversions.

The format specifiers in `scanf()` are shown in Fig. 9.2.

![](bbox=[0.56, 0.084, 0.974, 0.146])

**Fig. 9.2**  Parts of conversion specifier field for `scanf()`

The format specifiers, or the conversion code, that apply to `scanf()` are given in Table 9.6.

**Table 9.6  Format specifiers for `scanf()`**

| Conversion code | Usual variable type | Action |
|---|---|---|
| `%c` | char | Reads a single character. |
| `%d(%i)` | int | Reads a signed decimal integer. |
| `%e(%E)` | float or double | Reads signed decimal. |
| `%f` | float or double | Reads signed decimal. |
| `%g(%G)` | float or double | Reads signed decimal. |
| `%o` | int | Reads octal value. |
| `%p` | pointer | Reads in hex address stored in pointer. |
| `%s` | array of char | Reads sequence of characters (string). |
| `%u` | int | Reads unsigned decimal integer. |
| `%x(%X)` | int | Reads unsigned hex value. |
| `%%` | none | A single `%` character in the input stream is expected. There is no corresponding argument. |
| `%n` | pointer to int | No characters in the input stream are matched. The corresponding argument is a pointer to an integer into which the number of characters read is placed. |
| `[...]` | array of char | Reads a string of matching characters. |

# Formatted input in `scanf()`

Typically, the format string for a `scanf()` will not contain constant text. If it does, that means the input must contain the same text in the same position. For example, consider the following simple program.

# EXAMPLE

```
20.  #include <stdio.h>
     int main(void)
     {
         int x;
         scanf("Number=%d", &x);
         printf("The value of x is %d.\n", x);
         return 0;
     }
```

If the user wants the value of x to be 25, the user would have to type `Number=25` exactly, or the behaviour of this little program is