+   - StringBuilder method length (p. 688) returns the number of characters currently stored in a StringBuilder. StringBuilder method capacity (p. 688) returns the number of characters that can be stored in a StringBuilder without allocating more memory.
+   - StringBuilder method ensureCapacity (p. 688) ensures that a StringBuilder has at least the specified capacity. Method setLength increases or decreases the length of a StringBuilder.
+   - StringBuilder method charAt (p. 690) returns the character at the specified index. Method setCharAt (p. 690) sets the character at the specified position. StringBuilder method getChars (p. 690) copies characters in the StringBuilder into the character array passed as an argument.
+   - StringBuilder’s overloaded append methods (p. 691) add primitive-type, character array, String, Object or CharSequence (p. 707) values to the end of a StringBuilder.
+   - StringBuilder’s overloaded insert (p. 693) methods insert primitive-type, character array, String, Object or CharSequence values at any position in a StringBuilder.

# Section 16.5 Class Character

+   - Character method isDefined (p. 695) determines whether a character is in the Unicode character set.
+   - Character method isDigit (p. 695) determines whether a character is a defined Unicode digit.
+   - Character method isJavaIdentifierStart (p. 696) determines whether a character can be used as the first character of a Java identifier. Character method isJavaIdentifierPart (p. 696) determines if a character can be used in an identifier.
+   - Character method isLetter (p. 696) determines if a character is a letter. Character method isLetterOrDigit (p. 696) determines if a character is a letter or a digit.
+   - Character method isLowerCase (p. 696) determines whether a character is a lowercase letter. Character method isUpperCase (p. 696) determines whether a character is an uppercase letter.
+   - Character method toUpperCase (p. 696) converts a character to its uppercase equivalent. Character method toLowerCase (p. 696) converts a character to its lowercase equivalent.
+   - Character method digit (p. 696) converts its character argument into an integer in the number system specified by its integer argument radix (p. 697). Character method forDigit (p. 696) converts its integer argument digit into a character in the number system specified by its integer argument radix.
+   - Character method charValue (p. 698) returns the char stored in a Character object. Character method toString returns a String representation of a Character.

# Section 16.6 Tokenizing Strings

+   - Class String’s split method (p. 705) tokenizes a String based on the delimiter (p. 699) specified as an argument and returns an array of Strings containing the tokens (p. 699).

# Section 16.7 Regular Expressions, Class Pattern and Class Matcher

+   - Regular expressions (p. 700) are sequences of characters and symbols that define a set of strings. They’re useful for validating input and ensuring that data is in a particular format.
+   - String method matches (p. 700) receives a string that specifies the regular expression and matches the contents of the String object on which it’s called to the regular expression. The method returns a boolean indicating whether the match succeeded.
+   - A character class is an escape sequence that represents a group of characters. Each character class matches a single character in the string we’re attempting to match with the regular expression.
+   - A word character (\w; p. 700) is any letter (uppercase or lowercase), any digit or the underscore character.