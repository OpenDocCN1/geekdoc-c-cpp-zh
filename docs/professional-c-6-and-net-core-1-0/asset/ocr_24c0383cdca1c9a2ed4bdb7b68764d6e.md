| Symbol | Description | Example | Matches |
|---|---|---|---|
| ^ | Beginning of input text | ^B | B, but only if first character in text |
| $ | End of input text | X$ | X, but only if last character in text |
| . | Any single character except the newline character (\ ) | i.ation | isation, ization |
| * | Preceding character may be repeated zero or more times | ra*t | rt, rat, raat, raaat, and so on |
| + | Preceding character may be repeated one or more times | ra+t | rat, raat, raaat and so on, but not rt |
| ? | Preceding character may be repeated zero or one time | ra?t | rt and rat only |
| \s | Any whitespace character | \sa | [space]a, \ta, \na (\t and \n have the same meanings as in C#) |
| \S | Any character that isn’t whitespace | \SF | aF, rF, cF, but not \tf |
| \b | Word boundary | ion\b | Any word ending in ion |
| \B | Any position that isn’t a word boundary | \BX\B | Any x in the middle of a word |

If you want to search for one of the meta-characters, you can do so by escaping the corresponding character with a backslash. For example, . (a single period) means any single character other than the newline character, whereas \. means a dot.

You can request a match that contains alternative characters by enclosing them in square brackets. For example, [1c] means one character that can be either 1 or c. If you wanted to search for any occurrence of the words map or man, you would use the sequence ma[np]. Within the square brackets, you can also indicate a range, for example [a-z], to indicate any single lowercase letter, [A-E] to indicate any uppercase letter between A and E (including the letters A and E themselves), or [0-9] to represent a single digit. A shorthand notation for [0-9] is \d. If you wanted to search for an integer (that is, a sequence that contains only the characters 0 through 9), you could write [0-9]+ or [\d]+.

The ^ has a different meaning used within square brackets. Used outside square brackets, it marks the beginning of input text. Within square brackets, it means any character except the following.