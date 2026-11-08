The program directly displays on line 12 the formatted string. However, the calls on lines 16 and 25 use a string as a buffer. Additionally, std::format_to_n pushes only five characters onto the buffer.

![](bbox=[0.31, 0.17, 0.69, 0.32])

Formatted output

Accordingly, here is the corresponding program using std::vformat and std::vformat_to.

# A first impression of std::vformat, and std::vformat_to

```
```cpp
// formatKumtime.cpp

#include <format>
#include <iostream>
#include <iterator>
#include <string>

int main() {

    std::cout << '\n';

    std::string formatString = "Hello, C++{}!\n";

    std::cout << std::vformat(formatString, std::make_format_args("20")) << '\n';

    std::string buffer;

    std::vformat_to(
        std::back_inserter(buffer),
        formatString,
        std::make_format_args("20"));

    std::cout << buffer << '\n';

}
```
```

The formatString in lines 12 and 18 is lvalue.