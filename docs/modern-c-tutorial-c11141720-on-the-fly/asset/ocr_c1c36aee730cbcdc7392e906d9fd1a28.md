# 6.2 std::regex and Its Related

overloaded forms. The simplest form is to pass std::string and std::regex to match. When the match is successful, it will return true, otherwise it will return false. For example:

```
#include <iostream>
#include <string>
#include <regex>
```

```
int main() {
    std::string fname[] = {"foo.txt", "bar.txt", "test", "a0.txt"};
    // In C++, \\' will be used as an escape character in the string. In order for \\' to be passed
    std::regex txt("[a-z]+\.txt");
    for (const auto &fname : fname) {
        std::cout << fname << " << " << std::regex_match(fname, txt) << std::endl;
    }
}
}
```

Another common form is to pass in the three arguments std::string/std::match/std::regex. The essence of std::smatch is actually std::match_results. In the standard library, std::match_results<std::string,const_iterator>, which means match_results of a substring iterator. Use std::match to easily get the matching results, for example:

```
std::regex base_regex("([a-z]+\.txt");
std::smatch base_match;
for(const auto &fname : fname) {
    if (std::regex_match(fname, base_match, base_regex)) {
        // the first element of std::smatch matches the entire string
        // the second element of std::smatch matches the first expression with brackets
        if (base_match.size() == 2) {
            std::string base = base_match[1].str();
            std::cout << "sub-match[0]:" << base_match[0].str() << std::endl;
            std::cout << fname << " << " sub-match[1]:" << base << " << " << std::endl;
        }
    }
}
```

The output of the above code snippets is:

```
foo.txt: 1
bar.txt: 1
test: 0
a0.txt: 0
AAA.txt: 0
sub-match[0]: foo.txt
```