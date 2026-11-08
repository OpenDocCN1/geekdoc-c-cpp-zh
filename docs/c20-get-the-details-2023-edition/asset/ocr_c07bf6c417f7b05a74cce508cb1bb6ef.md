# The current time displayed with the C++20 clocks

```
```cpp
// timePointsOutput.cpp

#include <chrono>
#include <iostream>

int main() {

    std::cout << '\n';

    auto nowSystemClock = std::chrono::system_clock::now();
    std::cout << "nowSystemClock: " << nowSystemClock << '\n';

    auto nowSteadyClock = std::chrono::steady_clock::now();
    // std::cout << "nowSteadyClock: " << nowSteadyClock << '\n';     ERROR

    auto nowFileClock = std::chrono::file_clock::now();
    std::cout << "nowFileClock:  " << nowFileClock << '\n';

    auto nowGPSClock = std::chrono::gps_clock::now();
    std::cout << "nowGPSClock: " << nowGPSClock << '\n';

    // auto nowLocal_Clock = std::chrono::local_t::now();             ERROR

    auto nowTAIClock = std::chrono::tai_clock::now();
    std::cout << "nowTAIClock:   " << nowTAIClock << '\n';

    auto nowUTCClock = std::chrono::utc_clock::now();
    std::cout << "nowUTCClock:  " << nowUTCClock << '\n';

    std::cout << '\n';

}
```
```

The program shows two interesting facts. First, the current time given by the `std::chrono::steady_clock::now()` cannot be displayed (line 14). Second, the pseudo clock `std::chrono::local_t` has not static member function `now()` (line 22).