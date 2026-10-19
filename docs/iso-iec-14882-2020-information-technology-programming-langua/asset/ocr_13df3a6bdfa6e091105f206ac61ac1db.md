5 The sign option applies to floating-point infinity and NaN.

> [Example 2:

```
double inf = numeric_limits<double>::infinity();
double nan = numeric_limits<double>::quiet_NaN();
string s0 = format("{0:},{0:+},{0:-},{0: }", 1);    // value of s0 is "1,+1,1, 1"
string s1 = format("{0:},{0:+},{0:-},{0: }", -1);   // value of s1 is "-1,-1,-1,-1"
string s2 = format("{0:},{0:+},{0:-},{0: }", inf);  // value of s2 is "inf,+inf,inf, inf"
string s3 = format("{0:},{0:+},{0:-},{0: }", nan);  // value of s3 is "nan,+nan,nan, nan"
```

— end example

6 The # option causes the alternate form to be used for the conversion. This option is valid for arithmetic types other than charT and bool or when an integer presentation type is specified, and not otherwise. For integral types, the alternate form inserts the base prefix (if any) specified in Table 62 into the output after the sign character (possibly space) if there is one, or before the output of to_chars otherwise. For floating-point types, the alternate form causes the result of the conversion of finite values to always contain a decimal-point character, even if no digits follow it. Normally, a decimal-point character appears in the result of these conversions only if a digit follows it. In addition, for g and G conversions, trailing zeros are not removed from the result.

7 If { arg-id_opt } is used in a width or precision, the value of the corresponding formatting argument is used in its place. If the corresponding formatting argument is not of integral type, or its value is negative for precision or non-positive for width, an exception of type format_error is thrown.

8 The positive-integer in width is a decimal integer defining the minimum field width. If width is not specified, there is no minimum field width, and the field width is determined based on the content of the field.

9 The width of a string is defined as the estimated number of column positions appropriate for displaying it in a terminal.

> [Note 5: This is similar to the semantics of the POSIX wcwidth function. — end note]

10 For the purposes of width computation, a string is assumed to be in a locale-independent, implementation-defined encoding. Implementations should use a Unicode encoding on platforms capable of displaying Unicode text in a terminal.

> [Note 6: This is the case for Windows226-based and many POSIX-based operating systems. — end note]

11 For a string in a Unicode encoding, implementations should estimate the width of a string as the sum of estimated widths of the first code points in its extended grapheme clusters. The extended grapheme clusters of a string are defined by UAX #29. The estimated width of the following code points is 2:

+   (11.1) — U+1100–U+115F
+   (11.2) — U+2329–U+232A
+   (11.3) — U+2E80–U+303E
+   (11.4) — U+3040–U+A4CF
+   (11.5) — U+AC00–U+D7A3
+   (11.6) — U+F900–U+FAFF
+   (11.7) — U+FE10–U+FE19
+   (11.8) — U+FE30–U+FE6F
+   (11.9) — U+FF00–U+FF60
+   (11.10) — U+FFE0–U+FFE6
+   (11.11) — U+1F300–U+1F64F
+   (11.12) — U+1F900–U+1F9FF
+   (11.13) — U+20000–U+2FFFD
+   (11.14) — U+30000–U+3FFFD

The estimated width of other code points is 1.