# Summary

The three subjects of this chapter were the character data type, a C-String (a null-terminated array), and the C++ string class.

We discussed the issues involved in reading a reader when a newline character may be left in the input buffer, and derived the following three rules.

The first rule is to always ignore cin and the string extraction operator (>>) with the no-argument ignore function. The reason is that the cin object with the extraction operator >> leaves a newline in the input buffer, so calling the no-argument ignore function will dispose of leftover newline character.

The second rule is not to use the ignore member function after using the getline function. The reason is that the getline member function removes the newline character that terminated it from the input buffer.

The third rule is that after using the get member function with one argument, as cin.get(ch), to check if you have a newline character in the input buffer, and if you do, call the ignore member function. If you don't, the reason is that the get member function with one argument will leave a newline character in the input buffer if you type a character and then press ENTER, but it won't if you press ENTER.

The C++ standard library cctype contains number of functions that are useful with characters. The tou and lower functions each have one argument, a character. If the character represents a letter, A Z or z, the tou function returns the uppercase of it. Conversely, the lower function returns the lowercase of it. If the argument is not a letter, both functions return the same character that is the argument. A number of other functions in the ctype standard library, including but not limited to isalpha and isdigit, permit you to determine the value of a character, as whether it is a letter, digit, or whitespace.

The cstring standard library provides a number of functions that are useful when working with C-strings. Typically, the string library provides a number of functions that are useful when working with the C++ string class. Use the strlen function to determine the length of a C-string, the length or size member functions to return the length of a C++ string class variable. Use the assignment operator = to assign a value to a C++ string class. Use the strcat function to append a value to a C++ string, and the combined addition and assignment operator += to append a value to a C++ string class variable. Use the strcmp function to compare two C-strings, and the relational operators to compare two C++ string class variables.

The cstdlib standard library provides several functions for converting the C-string representation of a number to a numeric data type, as well as the reverse. These are atoi, or "ASCII to integer," atol, or "ASCII to Long," atof, or "ASCII to float," and itoa, or "Integer to ASCII."