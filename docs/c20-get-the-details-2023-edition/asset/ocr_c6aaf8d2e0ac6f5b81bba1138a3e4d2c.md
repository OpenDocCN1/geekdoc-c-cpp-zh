![](bbox=[0.283, 0.123, 0.717, 0.455])

std::shift and std::shift_right applied onto two containers

# 5.3.6 String prefix and suffix checking

std::string gets new member functions starts_with and ends_with. They allow you to check if a std::string starts or ends with a specified substring.

Check if a string starts with or ends with a given string

```
```cpp
// stringStartsWithEndsWith.cpp

#include <iostream>
#include <string_view>
#include <string>

template <typename PrefixType>
void startsWith(const std::string& str, PrefixType prefix) {
    std::cout << "           starts with " << prefix << " "
              << str.starts_with(prefix) << '\\n';
}

template <typename SuffixType>
void endsWith(const std::string& str, SuffixType suffix) {
    std::cout << "             ends with " << suffix << " "
              << str.ends_with(suffix) << '\\n';
}
```
```