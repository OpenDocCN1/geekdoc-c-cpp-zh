If we look at the table with integral type precisions, we see that the absolute value doesn’t fit in an int, so we need a uint or some long instead. Therefore, we assign the result to a long, to pick one. However, the compiler types the literal passed in as a parameter to be an int, and hence the first method is chosen:

```
int Abs(int value);
```

Because this method does not know how to represent the value 2,147,483,648 as an int required by the return type, it blows up with a runtime exception, effectively terminating our program forcefully.

What we need here is a way to tell the compiler to treat the literal not as an int but as a long, for it to pick the other overload. Different workarounds exist, ranging from using an intermediate local variable to the use of a conversion (see further). However, the use of an integer type suffix is more appropriate here. Three such suffixes exist: u, l, and ul (all of which can be written using any casing you want). The first one, u, indicates to treat the literal as unsigned. Next, l, means to treat it as a long. And finally, ul means to treat it as an unsigned long.

Here’s our fixed example using an integer type suffix:

```
long res = Math.Abs(-2147483648L);
```

For the precise rules for determining the type of an integral literal, refer to the official C# specification, section 2.4.4.2.

# NON-CASE-SENSITIVE SUFFIXES

Why are those type suffixes not case-sensitive, while C# is a case-sensitive language? Every keyword being lowercased, the natural choice would be to only allow this natural feeling style for suffix characters. However, a problem exists for the lowercase letter l looking similar to numeral 1 in lots of fonts. It is clearer to write L to avoid this confusion. To allow this and keep the typical style of lowercase, characters occurring in integral literals (including 0x and the hexadecimal letters) are not case-sensitive. This makes more sense than having one exception to the lowercase rule (just for an L).

# Character Literals

The char type is used to represent a single Unicode character. Character literals consist of single quotes containing the character to be represented, or an escape sequence. A few examples not involving the use of escapes are shown here:

```
char c1 = 'A';
char c2 = 'b';
char c3 = '.';
char c4 = '#';
```

Some characters need escaping using the backslash character as a prefix. Those are \' (single quote), \" (double quote), \\ (backslash), \0 (null character), \'a\' (alert, beeping