**Table 2.7** Predefined Character Class Names Used with \p

| Character Class Name | Explanation |
| --- | --- |
| posixClass | posixClass is one of Lower, Upper, Alpha, Digit, Alnum, Punct, Graph, Print, Cntrl, XDigit, Space, Blank, ASCII, interpreted as POSIX or Unicode class, depending on the UNICODE_CHARACTER_CLASS flag |
| IsScript, sc=Script, script=Script | A script accepted by Character.UnicodeScript.forName |
| InBlock, blk=Block, block=Block | A block accepted by Character.UnicodeBlock.forName |
| Category, InCategory, gc=Category, general_category=Category | A one- or two-letter name for a Unicode general category |
| IsProperty | Property is one of Alphabetic, Ideographic, Letter, Lowercase, Uppercase, Titlecase, Punctuation, Control, White Space, Digit, Hex_Digit, Join_Control, Noncharacter_Code_Point, Assigned |
| javaMethod | Invokes the method Character.isMethod (must not be deprecated) |

+   - Most characters match themselves, such as the `ava` characters in the preceding example.
+   - The `.` symbol matches any character (except possibly line terminators, depending on flag settings).
+   - Use `\` as an escape character. For example, `\.` matches a period and `\\` matches a backslash.
+   - `^` and `$` match the beginning and end of a line, respectively.
+   - If `X` and `Y` are regular expressions, then `XY` means “any match for `X` followed by a match for `Y`.” `X | Y` means “any match for `X` or `Y`.”
+   - You can apply quantifiers `X+` (1 or more), `X*` (0 or more), and `X?` (0 or 1) to an expression `X`.
+   - By default, a quantifier matches the largest possible repetition that makes the overall match succeed. You can modify that behavior with suffixes `?` (reluctant, or stingy, match: match the smallest repetition count) and `+` (possessive, or greedy, match: match the largest count even if that makes the overall match fail).

For example, the string `cab` matches `[a-z]*ab` but not `[a-z]*+ab`. In the first case, the expression `[a-z]*` only matches the character `c`, so that the characters `ab` match the remainder of the pattern. But the greedy version