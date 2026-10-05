In the new new_str string, all occurrences of the ";" pattern are replaced with ",". If you only want to replace the first match, pass regex_replace and regex_constants::format_first_only as an additional parameter.

# 28.2.4 Rich in Variants

We have already seen that the text to be searched can be passed in different ways. The functions are indeed very flexible for various needs due to numerous overloads.

For example, there are variants of regex_search that could be informally summarized as:

+   - Text to be searched, such as string, const char*, or a pair of iterators

+   - Optional match_results, like cmatch

+   - The pattern to be searched as regex

+   - Optional flags, which default to regex_constants::match_default if omitted

The same applies to regex_match and regex_replace as well.

The standard library's regular expressions are not limited to character strings of char. Especially wchar_t and its string variant wstring are supported. In the background general templates are working, the central one being regex_traits. This is where the functions for interpretingting regular expressions and text are grouped together. Normally you do not need to do anything here, but there is nothing wrong with interpreting something