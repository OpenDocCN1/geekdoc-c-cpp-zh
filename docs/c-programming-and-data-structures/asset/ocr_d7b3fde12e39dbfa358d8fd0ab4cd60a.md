# # 1.62 Computer Programming

+   1. First character must be an alphabet (or underscore).
+   2. Must consist of only letters, digits or underscore.
+   3. Only first 31 characters are significant.
+   4. Cannot use a keyword.
+   5. Must not contain white space.

# ## 1.29 CONSTANTS

Constants in C refer to fixed values that do not change during the execution of a program. C supports several types of constants as illustrated in Fig. 1.67.

![](bbox=[0.12, 0.32, 0.88, 0.56])

# ## 1.29.1 Integer Constants

An integer constant refers to a sequence of digits. There are three types of integers, namely, decimal integer, octal integer and hexadecimal integer.

Decimal integers consist of a set of digits, 0 through 9, preceded by an optional – or + sign. Valid examples of decimal integer constants are:

+   123
+   -321
+   0
+   654321
+   +78

Embedded spaces, commas, and non-digit characters are not permitted between digits. For example, 15 750 20,000 $1000 are illegal numbers.

> *NOTE: ANSI C supports unary plus which was not defined earlier.

An octal integer constant consists of any combination of digits from the set 0 through 7, with a leading 0. Some examples of octal integer are:

+   037
+   0
+   0435
+   0551