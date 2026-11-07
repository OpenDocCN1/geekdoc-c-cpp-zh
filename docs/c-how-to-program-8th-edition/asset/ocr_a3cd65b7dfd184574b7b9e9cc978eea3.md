+   - Function isalpha (p. 811) determines if its argument is an uppercase (A–Z) or lowercase letter (a–z).

+   - Function isalnum (p. 811) determines if its argument is an uppercase letter (A–Z), a lowercase letter (a–z), or a digit (0–9).

+   - Function isxdigit (p. 811) determines if its argument is a hexadecimal digit (A–F, a–f, 0–9).

+   - Function toupper (p. 812) converts a lowercase letter to an uppercase letter. Function tolower (p. 812) converts an uppercase letter to a lowercase letter.

+   - Function isspace (p. 813) determines if its argument is one of the following white-space characters: ' ' (space), '\f', '\n', '\r', '\t' or '\v'.

+   - Function iscntrl (p. 813) determines if its argument is a control character, such as '\t', '\v', '\f', '\a', '\b', '\r' or '\n'.

+   - Function ispunct (p. 813) determines if its argument is a printing character other than a space, a digit or a letter.

+   - Function isprint (p. 813) determines if its argument is any printing character, including space.

+   - Function isgraph (p. 813) determines if its argument is a printing character other than space.

# Section 21.8 Pointer-Based String Manipulation Functions

+   - Function strcpy (p. 816) copies its second argument into its first argument. You must ensure that the target array is large enough to store the string and its terminating null character.

+   - Function strncpy (p. 817) is equivalent to strcpy, but it specifies the number of characters to be copied from the string into the array. The terminating null character will be copied only if the number of characters to be copied is at least one more than the length of the string.

+   - Function strcat (p. 818) appends its second string argument—including the terminating null character—to its first string argument. The first character of the second string replaces the null ('\0') character of the first string. You must ensure that the target array used to store the first string is large enough to store both the first string and the second string.

+   - Function strncat (p. 818) is equivalent to strcat, but it appends a specified number of characters from the second string to the first string. A terminating null character is appended to the result.

+   - Function strcmp (p. 818) compares its first string argument with its second string argument character by character. The function returns zero if the strings are equal, a negative value if the first string is less than the second string and a positive value if the first string is greater than the second string.

+   - Function strncmp is equivalent to strcmp, but it compares a specified number of characters. If the number of characters in one of the strings is less than the number of characters specified, strncmp compares characters until the null character in the shorter string is encountered.

+   - A sequence of calls to strtok (p. 820) breaks a string into tokens that are separated by characters contained in a second string argument. The first call specifies the string to be tokenized as the first argument, and subsequent calls to continue tokenizing the same string specify NULL as the first argument. The function returns a pointer to the current token from each call. If there are no more tokens when strtok is called, NULL is returned.

+   - Function strlen (p. 822) takes a string as an argument and returns the number of characters in the string—the terminating null character is not included in the length of the string.

# Section 21.9 Pointer-Based String-Conversion Functions

+   - Function atof (p. 823) converts its argument—a string beginning with a series of digits that represents a floating-point number—to a double value.

+   - Function atoi (p. 824) converts its argument—a string beginning with a series of digits that represents an integer—to an int value.