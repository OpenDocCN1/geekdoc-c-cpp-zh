# 1.29.4 String Constants

A string constant is a sequence of characters enclosed in double quotes. The characters may be letters, numbers, special characters and blank space. Examples are:

“Hello!” “1987” “WELL DONE” “?..!” “$+3” “X”

Remember that a character constant (e.g., 'X') is not equivalent to the single character string constant (e.g., "X"). Further, a single character string constant does not have an equivalent integer value while a character constant has an integer value. Character strings are often used in programs to build meaningful programs. Manipulation of character strings are considered in detail in Chapter 11.

# 1.29.5 Backslash Character Constants

C supports some special backslash character constants that are used in output functions. For example, the symbol '\n' stands for newline character. A list of such backslash character constants is given in Table 1.7. Note that each one of them represents one character, although they consist of two characters. These characters combinations are known as escape sequences.

Table 1.7 Backslash Character Constants

| Constant | Meaning |
|---|---|
| '\a' | audible alert (bell) |
| '\b' | back space |
| '\f' | form feed |
| '\n' | new line |
| '\r' | carriage return |
| '\t' | horizontal tab |
| '\v' | vertical tab |
| '\'' | single quote |
| '\"' | double quote |
| '\?' | question mark |
| '\\' | backslash |
| '\0' | null |

# 1.30 VARIABLES

A variable is a data name that may be used to store a data value. Unlike constants that remain unchanged during the execution of a program, a variable may take different values at different times during execution. In Chapter 3, we used several variables. For instance, we used the variable amount in Sample Program 3 to store the value of money at the end of each year (after adding the interest earned during that year).

A variable name can be chosen by the programmer in a meaningful way so as to reflect its function or nature in the program. Some examples of such names are:

+   - Average
+   - height