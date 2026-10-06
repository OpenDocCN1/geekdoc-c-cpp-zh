# 34 — 2 Elementary C++ Programming

"CHINA" C H I N A \ 0

"a" a \0

'a' a

> Fig. 2.1: Memory presentation of string and character.

For example, the hexadecimal ASCII code of 'a' is 61, so 'a' can also be written as '\x61'.
Since single quotes are the boundary of a character, a single quote itself needs to be represented using escape sequence '\'.

Character data is stored in ASCII code in memory. Each character needs 1 byte, using the last 7 binary bits of the byte.

# 4. String Constants

String is short for string constants, using a pair of double quotes to enclose the character sequence. For example: "abcd", "China", and "This is a string" are all constants. Since double quotes are the boundary of characters, a double quote itself needs to be represented using the escape sequence. For example:

"Please \"Yes\" or \"No\"

means:

Please enter "Yes" or "No"

A string is different from a character. String is stored in memory as a sequence of characters in the order of the characters it owns. Each character takes up one byte, and at the end of the string '\0' should be added as an end mark. Figure 2.1 is an example. From the figure we can find out string "a" and character 'a' are not the same.

# 5. Bool Constants

There are only two bool constants: false and true.

# 2.2.3 Variables

Variables have values that can change during the process of a program, and they need names to be identified.

# 1. Declaration and Definition of Variables

Just like constants, variables have various data types. We have to first declare the type and name of a variable before using it. Variables' names are also identifiers; thus to