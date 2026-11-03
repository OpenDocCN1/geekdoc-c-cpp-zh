+   - The 0 flag (p. 421) prints leading zeros for a value that does not occupy its entire field width.

# ### Section 9.10 Printing Literals and Escape Sequences

Most literal characters to be printed in a printf statement can simply be included in the format control string. However, there are several “problem” characters, such as the quotation mark (", p. 422) that delimits the format control string itself. Various control characters, such as newline and tab, must be represented by escape sequences. An escape sequence is represented by a backslash (\), followed by a particular escape character.

# ### Section 9.11 Reading Formatted Input with scanf

+   - Input formatting is accomplished with the scanf library function.
+   - Integers are input with scanf with the conversion specifiers d and i (p. 424) for optionally signed integers and o, u, x or X for unsigned integers. The modifiers h, l and ll are placed before an integer conversion specifier to input a short, long and long long integer, respectively.
+   - Floating-point values are input with scanf with the conversion specifiers e, E, f, g or G. The modifiers l and L are placed before any of the floating-point conversion specifiers to indicate that the input value is a double or long double value, respectively.
+   - Characters are input with scanf with the conversion specifier c (p. 426).
+   - Strings are input with scanf with the conversion specifier s (p. 426).
+   - A scanf with a scan set (p. 426) scans the characters in the input, looking only for those characters that match characters contained in the scan set. When a character is matched, it’s stored in a character array. The scan set stops inputting characters when a character not contained in the scan set is encountered.
+   - To create an inverted scan set (p. 427), place a caret (^) in the square brackets before the scan characters. This causes characters input with scanf and not appearing in the scan set to be stored until a character contained in the inverted scan set is encountered.
+   - Address values are input with scanf with the conversion specifier p.
+   - Conversion specifier n stores the number of characters input so far in the current scanf. The corresponding argument is a pointer to int.
+   - The assignment suppression character (*, p. 428) reads data from the input stream and discards the data.
+   - A field width is used in scanf to read a specific number of characters from the input stream.

# ## Self-Review Exercises

9.1 Fill in the blanks in each of the following:

+   - a) All input and output is dealt with in the form of ________.
+   - b) The ________ stream is normally connected to the keyboard.
+   - c) The ________ stream is normally connected to the computer screen.
+   - d) Precise output formatting is accomplished with the ________ function.
+   - e) The format control string may contain ________, ________, ________, ________, ________ and ________.
+   - f) The conversion specifier ________ or ________ may be used to output a signed decimal integer.
+   - g) The conversion specifiers ________, ________ and ________ are used to display unsigned integers in octal, decimal and hexadecimal form, respectively.
+   - h) The modifiers ________ and ________ are placed before the integer conversion specifiers to indicate that short or long integer values are to be displayed.