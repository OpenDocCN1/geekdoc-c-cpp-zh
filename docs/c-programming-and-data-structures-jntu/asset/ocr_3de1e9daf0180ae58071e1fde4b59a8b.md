# Backslash Character Constants

C supports some special backslash character constants that are used in output functions. For example, the symbol `\n` stands for newline character. A list of such backslash character constants is given in Table 3.3. Note that each one of them represents one character, although they consist of two characters. These character combinations are known as *escape sequences*.

# Table 3.3 Backslash Character Constants

| Constant | Meaning |
| --- | --- |
| `\a` | audible alert (bell) |
| `\b` | back space |
| `\f` | form feed |
| `\n` | new line |
| `\r` | carriage return |
| `\t` | horizontal tab |
| `\v` | vertical tab |
| `\'` | single quote |
| `\"` | double quote |
| `\?` | question mark |
| `\\` | backslash |
| `\0` | null |

# 3.6 VARIABLES

A *variable* is a data name that may be used to store a data value. Unlike constants that remain unchanged during the execution of a program, a variable may take different values at different times during execution. In Chapter 2, we used several variables. For instance, we used the variable **amount** in Sample Program 3 to store the value of money at the end of each year (after adding the interest earned during that year).

A variable name can be chosen by the programmer in a meaningful way so as to reflect its function or nature in the program. Some examples of such names are:

+   - Average
+   - height
+   - Total
+   - Counter_1
+   - class_strength

As mentioned earlier, variable names may consist of letters, digits, and the underscore(_) character, subject to the following conditions:

+   1. They must begin with a letter. Some systems permit underscore as the first character.
+   2. ANSI standard recognizes a length of 31 characters. However, the length should not normally be more than eight characters, since only the first eight characters are treated as significant by many compilers.