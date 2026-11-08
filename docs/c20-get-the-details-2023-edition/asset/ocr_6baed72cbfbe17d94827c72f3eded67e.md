# Other Format Specifier for Chrono

| Specifier | Description | Example |
|---|---|---|
| `%Z` | Time zone abbreviation | CEST |
| `%z` | Offset (hours and minutes) from UTC | +0200 |
| `%j` | Day of the year (Starting with 001) | 221 |
| `%q` | Unit suffix according to the time’s duration | ms |
| `%n` | Newline character | `\n` |
| `%t` | Tabulator character | `\t` |
| `%%` | % character | % |

The following program uses the time specifier and calendar date specifiers.

# Use of the time specifier and calendar date specifiers

```
```cpp
// formattedOutputChrono.cpp

#include <chrono>
#include <iostream>
#include <thread>

int main() {

    std::cout << '\n';

    using namespace std::literals;

    auto start = std::chrono::steady_clock::now();
    std::this_thread::sleep_for(33ms);
    auto end = std::chrono::steady_clock::now();
    std::cout << std::format("The job took {{}} seconds\n", end - start);
    std::cout << std::format("The job took {{:%S}} seconds\n", end - start);

    std::cout << '\n';

    auto now = std::chrono::system_clock::now();
    std::cout << "now: " << now << '\n';
    std::cout << "Specifier {%c}: " << std::format("{%c}\n", now);
    std::cout << "Specifier {%x}: " << std::format("{%x}\n", now);
    std::cout << "Specifier {%X}: " << std::format("{%X}\n", now);
    std::cout << "Specifier {%D}: " << std::format("{%D}\n", now);
    std::cout << "Specifier {%d}: " << std::format("{%d}\n", now);
    std::cout << "Specifier {%y}: " << std::format("{%y}\n", now);
    std::cout << "Specifier {%Y}: " << std::format("{%Y}\n", now);
    std::cout << "Specifier {%B}: " << std::format("{%B}\n", now);
}
```
```