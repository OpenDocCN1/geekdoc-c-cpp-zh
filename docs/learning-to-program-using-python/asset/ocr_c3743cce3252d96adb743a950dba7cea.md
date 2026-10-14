+   str.expandtabs([tabsize])

+   Return a copy of the string where all tab characters are replaced by one or more spaces, depending on the current column and the given tab size. The column number is reset to zero after each newline occurring in the string. If tabsize is not given, a tab size of 8 characters is assumed. This doesn’t understand other non-printing characters or escape sequences.

+   str.find(sub[, start[, end]])

+   Return the lowest index in the string where substring sub is found, such that sub is contained in the range [start, end]. Optional arguments start and end are interpreted as in slice notation. Return -1 if sub is not found. An alternative method is index(), which uses the same parameters but raises ValueError when the substring isn’t found.

+   str.format(format_string, *args, **kwargs)

+   Perform a string formatting operation. The format_string argument can contain literal text or replacement fields de- limited by braces {}. Each replacement field contains either the numeric index of a positional argument, or the name of a keyword argument. Returns a copy of format_string where each replacement field is replaced with the string value of the corresponding argument. >>> "The sum of 1 + 2 is {0}".format(1+2) 'The sum of 1 + 2 is 3'

+   See Format String Syntax for a description of the various formatting options that can be specified in format strings.

+   This method of string formatting is the new standard in Python 3.x, and should be preferred to the % formatting described in the text. However, if you are using a version of Python before 2.6, you will have to use the % method.

+   str.isalnum()