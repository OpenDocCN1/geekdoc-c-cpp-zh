# Common regular expression elements

| Element | Description |
|---|---|
| Ordinary character | Matches any character other than ., $, ^, [, {, (, |, ), *, +, ?, or \\. |
| \\ | Matches the character that follows. |
| \\d | Matches any decimal digit (0-9). |
| \\D | Matches any character other than a decimal digit. |
| \\w | Matches any word character (a-z, A-Z, and 0-9). |
| \\W | Matches any character other than a word character. |
| \\s | Matches any white space character (space, tab, new line, etc.). |
| \\S | Matches any character other than a whitespace character. |
| [abcd] | Matches any character included between the brackets. |
| [^abcd] | Matches any character that is not included between the brackets. |
| [a-z] | Matches any characters in the indicated range. |
| {n} | Matches exactly *n* occurrences of the preceding element or group. |
| {n,} | Matches at least *n* occurrences of the preceding element or group. |
| {n,m} | Matches at least *n* but no more than *m* occurrences of the preceding element or group. |
| * | Matches zero or more occurrences of the preceding element. |
| ? | Matches zero or one occurrence of the preceding element. |
| + | Matches one or more occurrences of the preceding element. |
| \| | Matches any of the elements separated by the vertical bar. |
| ( ) | Groups the elements that appear between the parentheses. |

# Examples of regular expressions

| Expression | Example | Description |
|---|---|---|
| \\d{3} | 289 | A three digit number. |
| \\w{8,20} | Frankenstein | At least eight but no more than twenty word characters. |
| \\d{2}-\\d{4} | 10-3944 | A two-digit number followed by a hyphen and a four-digit number. |
| \\w{1,8}\.\\w{1,3} | freddy.jpg | Up to eight letters or numbers, followed by a period and up to three letters or numbers. |
| (AB)\|(SB)-\\d{1,5} | SB-3276 | The letters AB or SB, followed by a hyphen and a one- to five-digit number. |
| \\d{5}(-\\d{4})? | 93711-2765 | A five-digit number, optionally followed by a hyphen and a four-digit number. |
| \\w*\\d\\w* | arm01 | A text entry that contains at least one numeral. |
| [xyz]\\d{3} | x023 | The letter x, y, or z, followed by a three-digit number. |

# Notes

+   - A regular expression can include elements other than those shown above. For more information, see the *Regular Expression Language Elements* topic in help.
+   - The standard regular expressions use only the elements shown above.