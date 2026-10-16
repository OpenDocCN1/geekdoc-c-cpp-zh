Variables of the three char types can be freely assigned to each other. However, assigning a toolarge value to a signed char (§10.5.2.1) is still undefined. For example:

```
void g(char c, signed char sc, unsigned char uc)
{
c = 255; // implementation-defined if plain chars are signed and have8bits
```

# Section 6.2.3.1 Signed and Unsigned Characters 143

```
c = sc; // OK
c = uc; // implementation-defined if plain chars are signed and if uc’svalue is too large sc = uc; // implementation defined if uc’svalue is too large
uc = sc; // OK: conversion to unsigned
sc = c; // implementation-defined if plain chars are unsigned and if c’svalue is too large uc = c; // OK: conversion to unsigned
}
```

To be concrete, assume that a char is 8 bits:

```
signed char sc = -160;
unsigned char uc = sc; // uc == 116 (because 256-160==116)
cout << uc; // print‘t’
```

```
char count[256]; // assume 8-bit chars
++count[sc]; // likely disaster:out-of-range access
++count[uc]; // OK
```

None of these potential problems and confusions occur if you use plain char throughout and avoid negative character values.

# 6.2.3.2 Character Literals

A character literal is a single character enclosed in single quotes, for example, ‘a’ and ‘0’. The type of a character literal is char. A character literal can be implicitly converted to its integer value in the character set of the machine on which the C++ program is to run. For example, if you are running on a machine using the ASCII character set, the value of ‘0’ is 48. The use of character literals rather than decimal notation makes programs more portable.

A few characters have standard names that use the backslash, \, as an escape character:

# Name ASCII Name C++ Name

+   Newline NL (LF) \n
+   Horizontal tab HT \t
+   Vertical tab VT \v
+   Backspace BS \b
+   Carriage return CR \r
+   Form feed FF \f
+   Alert BEL \a
+   Backslash \ \
+   Question mark ? \?
+   Single quote ‘ \’