# # Regular Expressions

Regular expression support appears in C++ 11 and above. It helps you look for patterns in strings. For example, you can ensure that email addresses and telephone numbers are in the right format before someone enters them into a database, reducing a few data errors in the process. You can also use regular expressions to perform search-and-replace operations. The following table contains the Regular Expression category classes.

| | | |
|---|---|---|
| basic_regex | match_results | regex_error |
| regex_iterator | regex_token_iterator | regex_traits |
| sub_match | | |

# ## Strings

The Strings category provides a wide range of support for strings in C++. You have seen many examples of the `<string>` header, the most commonly used header, in use in this book. Humans understand strings quite well, but computers handle characters and, therefore, strings as numbers. To make strings easier to use, you need library support. The following table lists the String category headers and their purpose.

| Header | C++ Version | Short Description |
|---|---|---|
| `<cctype>` | | Determines the category of narrow (char) characters. |
| `<charconv>` | C++ 17 and above | Conversion to and from characters. |
| `<cstring>` | | Narrow character string handling functions. |
| `<cuchar>` | C++ 11 and above | C-style Unicode character conversion functions. |
| `<cwchar>` | | Wide and multibyte character string handling functions. |
| `<cwctype>` | | Determines the category of wide (wchar_t) characters. |
| `<format>` | C++ 20 and above | String formatting functionality. |
| `<string_view>` | C++ 17 and above | Basic string view handling class. |
| `<string>` | | Basic string handling class. |