| Method | Meaning |
|---|---|
| public static bool IsLowSurrogate(char ch) | Returns true if ch is a valid UTF-32 low surrogate. Otherwise, returns false. |
| public static bool IsLowSurrogate(string str, int idx) | Returns true if str[idx] is a valid UTF-32 low surrogate. Otherwise, returns false. |
| public static bool IsNumber(char ch) | Returns true if ch is a number. Otherwise, returns false. |
| public static bool IsNumber(string str, int idx) | Returns true if str[idx] is a number. Otherwise, returns false. |
| public static bool IsPunctuation(char ch) | Returns true if ch is a punctuation character. Otherwise, returns false. |
| public static bool IsPunctuation(string str, int idx) | Returns true if str[idx] is a punctuation character. Otherwise, returns false. |
| public static bool IsSeparator(char ch) | Returns true if ch is a separator character, such as a space. Otherwise, returns false. |
| public static bool IsSeparator(string str, int idx) | Returns true if str[idx] is a separator character, such as a space. Otherwise, returns false. |
| public static bool IsSurrogate(char ch) | Returns true if ch is a Unicode surrogate character. Otherwise, returns false. |
| public static bool IsSurrogate(string str, int idx) | Returns true if str[idx] is a Unicode surrogate character. Otherwise, returns false. |
| public static bool IsSurrogatePair(char high, char low) | Returns true if high and low form a valid surrogate pair. Otherwise, returns false. |
| public static bool IsSurrogatePair(string str, int idx) | Returns true if the two consecutive characters starting at idx within str form a valid surrogate pair. Otherwise, returns false. |
| public static bool IsSymbol(char ch) | Returns true if ch is a symbolic character, such as the currency symbol. Otherwise, returns false. |
| public static bool IsSymbol(string str, int idx) | Returns true if str[idx] is a symbolic character, such as the currency symbol. Otherwise, returns false. |
| public static bool IsUpper(char ch) | Returns true if ch is an uppercase letter. Otherwise, returns false. |
| public static bool IsUpper(string str, int idx) | Returns true if str[idx] is an uppercase letter. Otherwise, returns false. |
| public static bool IsWhiteSpace(char ch) | Returns true if ch is a whitespace character, such as a space or tab. Otherwise, returns false. |
| public static bool IsWhiteSpace(string str, int idx) | Returns true if str[idx] is a whitespace character, such as a space or tab. Otherwise, returns false. |