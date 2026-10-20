# Summary

# Section 16.2 Fundamentals of Characters and Strings

+   - A character literal's value (p. 673) is its integer value in Unicode (p. 673). Strings can include letters, digits and special characters such as +, -, *, / and $. A string in Java is an object of class String. String literals (p. 674) are often referred to as String objects and are written in a program in double quotes.

# Section 16.3 Class String

+   - String objects are immutable (p. 675)—after they’re created, their character contents cannot be changed.
+   - String method length (p. 675) returns the number of characters in a String.
+   - String method charAt (p. 675) returns the character at a specific position.
+   - String method equals tests for equality. The method returns true if the contents of the Strings are equal, false otherwise. Method equals uses a lexicographical comparison (p. 679) for Strings.
+   - When primitive-type values are compared with ==, the result is true if both values are identical. When references are compared with ==, the result is true if both refer to the same object.
+   - Java treats all string literals with the same contents as a single String object.
+   - String method equalsIgnoreCase performs a case-insensitive string comparison.
+   - String method compareTo uses a lexicographical comparison and returns 0 if the Strings are equal, a negative number if the string that calls compareTo is less than the argument String and a positive number if the string that calls compareTo is greater than the argument String.
+   - String method regionMatches (p. 677) compares portions of two strings for equality.
+   - String methods startsWith and endsWith (p. 680) determine whether a string starts with or ends with the specified characters, respectively.
+   - String method indexOf (p. 681) locates the first occurrence of a character or a substring in a string. String method lastIndexOf (p. 681) locates the last occurrence of a character or a substring in a string.
+   - String method substring copies and returns part of an existing string object.
+   - String method concat concatenates two string objects and returns a new string object.
+   - String method replace returns a new string object that replaces every occurrence in a String of its first character argument with its second character argument.
+   - String method toUpperCase (p. 685) returns a new string with uppercase letters in the positions where the original string had lowercase letters. String method toLowerCase (p. 686) returns a new string with lowercase letters in the positions where the original string had uppercase letters.
+   - String method trim (p. 686) returns a new string object in which all white-space characters (e.g., spaces, newlines and tabs) have been removed from the beginning and end of a string.
+   - String method toCharArray (p. 686) returns a char array containing a copy of the string’s characters.
+   - String class static method valueOf returns its argument converted to a string.

# Section 16.4 Class StringBuilder

+   - Class StringBuilder provides constructors that enable StringBuilders to be initialized with no characters and an initial capacity of 16 characters, with no characters and an initial capacity specified in the integer argument, or with a copy of the characters of the String argument and an initial capacity that’s the number of characters in the String argument plus 16.