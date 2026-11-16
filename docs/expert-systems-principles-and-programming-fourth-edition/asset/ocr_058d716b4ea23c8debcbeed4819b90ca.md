A symbol is a field that starts with a printable ASCII character and is followed by zero or more characters. The end of a symbol is reached when a delimiter is encountered. Delimiters include any nonprintable ASCII character (including spaces, tabs, carriage returns, and line feeds), the " (double quotation mark) character, the ( (opening parenthesis) character, the ) (closing parenthesis) character, the ; (semicolon) character, the & (ampersand) character, the | (vertical bar) character, the ~ (tilde) character, and the < (less than) character. Symbols cannot contain delimiters (with the exception of the < character, which may be the first in a symbol). Also, the ? and $* (question mark and dollar sign/question mark) sequence of characters cannot be placed at the beginning of a symbol since they are used to denote variables (see Section 7.19). In addition, a sequence of characters that does not exactly follow the numeric field format is treated as a symbol. The following are examples of valid symbols:

+   Space-Station
+   February
+   fire
+   activate_sprinkler_system
+   notify-fire-department
+   shut-down-electrical-junction-387
+   !?$*^
+   345B
+   346-95-6156

Notice how the underscore and hyphen characters are used to tie symbols together to make them into a single field.

CLIPS will preserve the uppercase and lowercase letters it finds in tokens. Because it distinguishes between uppercase and lowercase letters, CLIPS is called case-sensitive. For example, the following symbols are considered different by CLIPS:

+   case-sensitive
+   Case-SENSITIVE
+   CASE-SENSITIVE

The next type of field is a string. A string must begin and end with double quotation marks, which are part of the field. There can be zero or more characters of any kind between the double quotes, including characters normally used by CLIPS as delimiters. The following are examples of valid CLIPS strings:

+   "Activate the sprinkler system."
+   "Shut down electrical junction 387."
+   "!?$*"
+   "John Q. Public"

Spaces normally act as delimiters in CLIPS to separate fields (such as symbols) and other tokens. Additional spaces used between tokens are discarded.