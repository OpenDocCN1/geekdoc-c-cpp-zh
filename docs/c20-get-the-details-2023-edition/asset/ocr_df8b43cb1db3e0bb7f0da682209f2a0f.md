# 8.1.2.6 std::expected

std::expected<T, E> provides a way to store either of two values. An instance of std::expected always holds a value: either the expected value of type T, or the unexpected value of type E. This vocabulary type requires the header <expected>. Thanks to std::expected, you can implement functions that either return a value or an error. The stored value is allocated directly within the storage occupied by the expected object. No dynamic memory allocation takes place.

std::expected has a similar interface such as std::optional. In contrast to std::optional, std::expected can return an error message.

The various constructors let you define an expected object exp with an expected value. exp.emplace will construct the contained value in-place. You can explicitly ask a std::expected if it has a value, or you can check it in a logical expression. exp.value returns the expected value, and exp.value_or returns the expected value, or a default value. If exp has an unexpected value, the call exp.value will throw a std::bad_expected_access exception.

std::unexpected represents the unexpected value stored in std::expected.

# **std::expected**

```
~~~cpp
1  // expected.cpp
2
3  #include <iostream>
4  #include <expected>
5  #include <vector>
6  #include <string>
7
8  std::expected<int, std::string> getInt(std::string arg) {
9      try {
10        return std::stoi(arg);
11    }
12    catch (...) {
13        return std::unexpected(std::string(arg + ": Error"));
14    }
15 }
16
17
18 int main() {
19
20    std::vector<std::string> strings = {"66", "foo", "-5"};
21
22    for (auto s: strings) {
23        auto res = getInt(s);
24        if (res) {
25            std::cout << res.value() << ' ';    // 66 -5
26        }
~~~
```