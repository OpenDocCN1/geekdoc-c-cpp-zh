# Chapter 9 511

Program 9.8), a string, or any other input is accepted by cin and then followed by a getline() call. There are three solutions to this "phantom" Enter key problem:

+   - Don't mix cin with getline() inputs in the same program.
- Follow the cin input with the call to cin.ignore().
- Accept the Enter key in a character variable and then ignore it.

The preferred solution is the first one. All solutions, however, center on the fact that the Enter key is a legitimate character input and must be recognized as such. You will encounter this problem when you learn about accepting char data types in Section 9.4.

# String Processing

Strings can be manipulated using string class functions or the character-at-time functions described in Section 9.4. Table 9.4 lists the most commonly string class functions the standard arithmetic and comparison operators can also be used with strings.

Table 9.4 The string Class Functions (Require the Header File string)

| Function/Operation | Description | Example |
| --- | --- | --- |
| int length() | Returns the length of the string | string.length() |
| int size() | Same as the preceding item | string.size() |
| at(int index) | Returns the character at the specified index and throws an exception if the index is nonexistent | string.at(4) |
| int compare(str) | Compares the given string to str; returns a negative value if the given string is less than str, a 0 if they are equal, and a positive value if the given string is greater than str | string1.compare(str2) |
| c_str() | Returns the string as a null-terminated C-string | string1.c_str() |
| bool empty | Returns true if the string is empty, otherwise, returns false | string1.empty() |