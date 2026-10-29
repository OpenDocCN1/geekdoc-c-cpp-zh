other input is accepted by cin and then followed by a getline() method call. There are three solutions to this “phantom” Enter key problem:

+   - Don't mix cin with getline() inputs in the same program.
+   - Follow the cin input with the call to cin.ignore().
+   - Accept the Enter key in a character variable and then ignore it.

The first solution is preferred. All solutions, however, center on the fact that the Enter key is a legitimate character input and must be recognized as such. You encounter this problem again when you learn about accepting char data types in Section 14.2.

# String Processing

Strings can be manipulated by using string class functions or the character-at-a-time functions described in Section 14.2. Table 14.3 lists the most commonly used string class methods plus the standard arithmetic and comparison operators that can also be used with strings. In the examples, class methods are called by giving the object's name first, followed by a period, and then the method's name. With a few notable exceptions, all class methods are called in this way.

Table 14.3 The string Class Processing Methods (Require #include <string>)

| Method/Operation | Description | Example |
|---|---|---|
| int length() | Returns the length of the string | string.length() |
| int size() | Same as the preceding item | string.size() |
| at(index) | Returns the character at the specified index and throws an exception if the index is nonexistent | string.at(4) |
| int compare(str) | Compares the given string with str; returns a negative value if the given string is less than str, a 0 if they're equal, and a positive value if the given string is greater than str | string1.compare(string2) |
| c_str() | Returns the string as a NULL-terminated C-string | string1.c_str() |
| bool empty | Returns true if the string is empty; otherwise, returns false | string1.empty() |
| erase(ind,n); | Removes n characters from the string, starting at index ind | string1.erase(2,3) |
| erase(ind) | Removes all characters from the string, starting from index ind until the end of the string, and the length of the remaining string becomes ind | string1.erase(4) |