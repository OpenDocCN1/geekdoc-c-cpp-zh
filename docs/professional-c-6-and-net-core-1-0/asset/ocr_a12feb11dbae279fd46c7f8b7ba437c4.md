| Member Name | Description |
|---|---|
| CultureInvariant | Specifies that the culture of the string is ignored. |
| ExplicitCapture | Modifies the way the match is collected by making sure that valid captures are the ones that are explicitly named. |
| IgnoreCase | Ignores the case of the string that is input. |
| IgnorePatternWhitespace | Removes unescaped whitespace from the string and enables comments that are specified with the pound or hash sign. |
| Multiline | Changes the characters ^ and $ so that they are applied to the beginning and end of each line and not just to the beginning and end of the entire string. |
| RightToLeft | Causes the inputted string to be read from right to left instead of the default left to right (ideal for some Asian and other languages that are read in this direction). |
| Singleline | Specifies a single-line mode where the meaning of the dot (.) is changed to match every character. |

So far, nothing is new from the preceding example apart from some .NET base classes. However, the power of regular expressions comes from that pattern string. The reason is that the pattern string is not limited to only plain text. As hinted earlier, it can also contain what are known as meta-characters, which are special characters that provide commands, as well as escape sequences, which work in much the same way as C# escape sequences. They are characters preceded by a backslash (\ ) and have special meanings.

For example, suppose you wanted to find words beginning with n. You could use the escape sequence \b, which indicates a word boundary (a word boundary is just a point where an alphanumeric character precedes or follows a whitespace character or punctuation symbol):

```
const string pattern = @"\bn";
MatchCollection myMatches = Regex.Matches(input, pattern,
    RegexOptions.IgnoreCase |
    RegexOptions.ExplicitCapture);
```

Notice the @ character in front of the string. You want the \b to be passed to the .NET regular expressions engine at runtime—you don’t want the backslash intercepted by a well-meaning C# compiler that thinks it’s an escape sequence in your source code. If you want to find words ending with the sequence ions, you write this:

```
const string pattern = @"ions\b";
```

If you want to find all words beginning with the letter a and ending with