# 28.2.1  Matching and Searching

While regex_match always checks if the entire text matches the pattern, regex_search also finds matches contained anywhere in the text.

```
```cpp
// https://godbolt.org/z/E9hcWGMVW4
#include <regex>
#include <string>
#include <iostream>
using std::regex; using std::regex_match; using std::regex_search;
int main() {
    std::cout << std::boolalpha;
    regex pattern {"hello"};
    std::string text = "hello world";
    auto b1 = regex_match (text.cbegin(), text.cend(), pattern); // doesn’t match
    std::cout << b1 << "\n"; // Output: false
    auto b2 = regex_search(text.cbegin(), text.cend(), pattern); // found
    std::cout << b2 << "\n"; // Output: true
}
```
```

Listing 28.11 Search and match.

# 28.2.2  The Result and Parts of It

You can optionally pass a parameter to the search functions, in which the exact details of the result are stored. This is useful if you are interested in the start and end position of the match or even the covered subexpressions.

```
```cpp
// https://godbolt.org/z/Yzefv59en
#include <regex>
#include <string>
#include <iostream>
using std::regex; using std::regex_search; using std::cmatch;
int main() {
    cmatch res;                                      // for detailed results
    std::string text = "<h2>Result and parts of It</h2>";
    regex pattern{"(h.)([^ ]+)"};                  // Search pattern with groups
    regex_search(text.c_str(), res, pattern);       // Details to res
    std::cout << res[1] << " "                      // 0-Group 1: H-Level
              << res[2] << std::endl;               // 0-Group 2: H-Text
}
```
```

Listing 28.12 Accessing the match details.