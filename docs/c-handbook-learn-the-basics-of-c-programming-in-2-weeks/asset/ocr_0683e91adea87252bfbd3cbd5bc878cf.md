# Chapter 6: Literals and Constants

The term “literals” refers to fixed or unchangeable values: you cannot alter these values while the program is being executed. Literals are also known as constants. Literals can take the form of any basic data type (e.g. floating constant, integer constant, string constant, character constant, etc.). Additionally, you can use enumeration literals in your C# statements.

# *The Integer Constants*

Integer constants can be octal, decimal, or hexadecimal literals. You should use a prefix to specify the base (also known as radix). Check this list:

+   - Use 0 for octal literals
+   - Use 0X or 0x for hexadecimal literals
+   - Decimal literals don’t require prefixes

Integer literals may also have L and U as a suffix. L is used for long integers while U is used for unsigned integers. These suffixes are not case-sensitive.

The list below will show you valid and invalid integer constants:

+   - 131 – Valid
+   - 312u – Valid
+   - 0XYoU – Valid
+   - 218 – Invalid: The number 8 isn’t octal.
+   - 123UU – Invalid: You must not repeat suffixes.

Here’s a second list of examples. This one, however, will show you the different kinds of Integer Constants: