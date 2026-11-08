+   - **string_view**  
+     This provides a read-only span to a string or a const char*. Typically, you use it as a parameter to a function where you previously passed a `string&`. You see an example of `string_view` as a parameter in [Listing 24.39](#).
+   - **"sv" as a suffix**  
+     The standard library also provides the user-defined `"sv` literal to create a string_view. The advantage over `"s` for string is that it does not create a new string, but only a view on the const char*—so almost nothing needs to be copied or created.

```
```cpp
// https://godbolt.org/z/P7zbrh71d
#include <vector>
#include <string>
#include <iostream>
#include <string_view>
using std::string; using std::string_view; using std::vector; using std::cout;

int get_len(string_view str) { return str.size(); } // string_view as parameter

int main() {
    string s1 = "Hello";                 // simply with string literal
    string s2{'H','e','l','l','o'};       // or with list of char
    using namespace std::literals;        // for "s"-suffix and "sv"-suffix
    auto s3 = "Hello"sv;                  // even simpler with string literal
    vector<char> v1{"Hello"};            // no vector with string literal
    vector<char> v2{'H','e','l','l','o'}; // vector of char is okay
    cout << s1 << s2 << s3 << '\n';       // Output of string works
    cout << v1 << v2 << '\n';             // vector has no output

    const auto str = "String"s;           // Stringliteral
    const auto strv = "String"sv;         // String-view literal
    cout << "Length of 'str' is " << get_len(str) << '\n';  // Output: ... 6
    cout << "Length of 'strv' is " << get_len(strv) << '\n'; // Output: ... 11
}
```
```

**Listing 24.89** “string” is more suitable for texts than “vector<char>”.

# 24.11 Special Cases: “vector<bool>”, “array<bool,n>”, and “bitset<n>”

For an array of truth values, the standard library offers several specialized solutions from which you can choose the right one depending on the application.