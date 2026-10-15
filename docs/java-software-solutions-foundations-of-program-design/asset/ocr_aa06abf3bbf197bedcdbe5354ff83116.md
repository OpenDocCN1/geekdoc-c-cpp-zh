# Regular Expressions

Throughout the book we’ve used the Scanner class to read interactive input from the user and parse strings into individual tokens such as words. In Chapter 5 we also used it to read input from a data file. Usually we used the default whitespace delimiters for tokens in the scanner input.

The Scanner class can also be used to parse its input according to a regular expression, which is a character string that represents a pattern. A regular expression can be used to set the delimiters used when extracting tokens, or it can be used in methods like findInLine to match a particular string.

Some of the general rules for constructing regular expressions include:

+   - The dot (.) character matches any single character.
+   - The * character, which is called the Kleene star, matches zero or more characters.
+   - A string of characters in square brackets ([ ]) matches any single character in the string.
+   - The \ character followed by a special character (such as the ones in this list) matches the character itself.
+   - The \ character followed by a character matches the pattern specified by that character (see the following table).

For example, the regular expression B.b* matches Bob, Bubba, and Baby. The regular expression T[aei]*ing matches Taking, Tickling, and Telling.

These examples are just a few of many. Figure H.1 specifies some of the patterns that can be matched in a Java regular expression, and this list is not complete. See the online documentation for the Pattern class for a complete list.