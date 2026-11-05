+   - Then if N ≥ 1 for each number I from 0 to N-1:
+     - A placeholder specification:
+       - A left brace ({) character
+       - The decimal representation of I
+       - Then, if the corresponding regular_interpolation or verbatim_interpolation has a interpolation_minimum_width, a comma (,) followed by the decimal representation of the value of the constant_expression
+       - The characters of the Regular_Interpolation_Format or Verbatim_Interpolation_Format, if any, of the corresponding regular_interpolation or verbatim_interpolation
+       - A right brace (}) character
+     - The characters of the Interpolated_Regular_String_Mid or Interpolated_Verbatim_String_Mid immediately following the corresponding interpolation, if any
+   - Finally the characters of the Interpolated_Regular_String_End or Interpolated_Verbatim_String_End.

The subsequent arguments are the expressions from the interpolations, if any, in order.

When an interpolated_string_expression contains multiple interpolations, the expressions in those interpolations are evaluated in textual order from the left to right.

Example:

This example uses the following format specification features:

+   - the X format specification which formats integers as uppercase hexadecimal,
+   - the default format for a string value is the value itself,
+   - positive alignment values that right-justify within the specified minimum field width,
+   - negative alignment values that left-justify within the specified minimum field width,
+   - defined constants for the interpolation_minimum_width, and
+   - that {{ and }} are formatted as { and } respectively.

Given:

```
string text = "red";
int number = 14;
const int width = -4;
```

Then:

| Interpolated String Expression | Equivalent Meaning As string | Value |
|---|---|---|
| ${text} | string.Format("{0}", text) | "red" |
| ${{text}} | string.Format("{{text}}") | "{text}" |
| ${ text , 4 } | string.Format("{0,4}", text) | "  red" |
| ${ text , width } | string.Format("{0,-4}", text) | "red  " |
| ${number:X} | string.Format("{0:X}", number) | "E" |
| ${text + '?'} {number % 3} | string.Format("{0} {1}", text + '?', number % 3) | "red? 2" |