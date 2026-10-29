We can utilize these classes to simplify our patterns. For example, if we want to match two consecutive words, then the regular expression of \w+\s\w+ will match any sequence of one or more word characters, followed by a whitespace, followed by any sequence of one or more word characters.

To match regular expressions in C++11, include the <regex> library. The regex class is part of the std namespace and takes a pattern as input. The regular expression library has the functions regex_match to exactly match a pattern to a string, regex_search to look for occurrences of patterns in a string, and regex_replace to replace matches in the string with a format string.

The following code illustrates regex_match to determine whether text1 or text2 matches the pattern of two words separated by whitespace. Note that since we need to include a literal \ in the pattern, the C++11 literal string format becomes very useful to simplify the pattern string. Otherwise, we would need two \s to represent a single \, since \ is the escape character.

```
#include <iostream>
#include <string>
#include <regex>

using namespace std;

int main()
{
    string text1 = "word1 word2";
    string text2 = "OnlyOneWord";
    string pattern = R"(\w+\s\w+)";
    regex reg(pattern);

    if (regex_match(text1, reg))
        cout << "Text1 matches pattern" << endl;
    else
        cout << "Text1 does not match pattern" << endl;

    if (regex_match(text2, reg))
        cout << "Text2 matches pattern" << endl;
    else
        cout << "Text2 does not match pattern" << endl;
    return 0;
}
```

Sample Dialogue:

```
Text1 matches pattern
Text2 does not match pattern
```