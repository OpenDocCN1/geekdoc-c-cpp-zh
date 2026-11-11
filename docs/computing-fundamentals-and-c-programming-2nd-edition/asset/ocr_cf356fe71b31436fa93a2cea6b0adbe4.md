**Table 4.5** *Backslash Character Constants*

| Constant | Meaning |
|---|---|
| `'\a'` | audible alert (bell) |
| `'\b'` | back space |
| `'\f'` | form feed |
| `'\n'` | new line |
| `'\r'` | carriage return |
| `'\t'` | horizontal tab |
| `'\v'` | vertical tab |
| `'\''` | single quote |
| `'\"'` | double quote |
| `'\?'` | question mark |
| `'\\'` | backslash |
| `'\0'` | null |

# ## 4.6 VARIABLES

**LO 4.2**

A *variable* is a data name that may be used to store a data value. A variable may take different values at different times during execution.

+   - Average
+   - height
+   - Total
+   - Counter_1
+   - class_strength

As mentioned earlier, variable names may consist of letters, digits, and the underscore(_) character, subject to the following conditions:

+   1. They must begin with a letter. Some systems permit underscore as the first character.
+   2. ANSI standard recognizes a length of 31 characters. However, length should not be normally more than eight characters, since only the first eight characters are treated as significant by many compilers. (In C99, at least 63 characters are significant.)
+   3. Uppercase and lowercase are significant. That is, the variable **Total** is not the same as **total** or **TOTAL**.
+   4. It should not be a keyword.
+   5. White space is not allowed.

Some examples of valid variable names are:

|  |  |  |
|---|---|---|
| John | Value | T_raise |
| Delhi | x1 | ph_value |
| mark | sum1 | distance |