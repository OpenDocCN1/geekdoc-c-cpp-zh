In addition, the standard library provides two useful functions for getting rid of case differences:

| Upper and lower case |
| --- |
| toupper(c) | c or c's uppercase equivalent |
| tolower(c) | c or c's lowercase equivalent |

Extended character sets, such as Unicode, are supported but are beyond the scope of this book.

# B.8.2 String

The standard library string class, **string**, is a specialization of a general string template **basic_string** for the character type **char**; that is, **string** is a sequence of **chars**:

| String operations |
| --- |
| s=s2 | Assign s2 to s; s2 can be a string or a C-style string. |
| s+=x | Append x at end of s; x can be a character, a string, or a C-style string. |
| s[i] | Subscripting. |
| s+s2 | Concatenation; the result is a new string with the characters from s followed by the characters from s2. |
| s==s2 | Comparison of string values; s or s2, but not both, can be a C-style string. |
| s!=s2 | Comparison of string values; s or s2, but not both, can be a C-style string. |
| s<s2 | Lexicographical comparison of string values; s or s2, but not both, can be a C-style string. |
| s<=s2 | Lexicographical comparison of string values; s or s2, but not both, can be a C-style string. |
| s>s2 | Lexicographical comparison of string values; s or s2, but not both, can be a C-style string. |
| s>=s2 | Lexicographical comparison of string values; s or s2, but not both, can be a C-style string. |
| s.size() | Number of characters in s. |
| s.length() | Number of characters in s. |