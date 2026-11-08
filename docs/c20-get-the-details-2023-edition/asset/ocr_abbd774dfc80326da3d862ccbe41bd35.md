![](bbox=[0.3, 0.095, 0.7, 0.258])

Current time with the C++20 clocks

The GPS time is 18 seconds ahead of the UTC time. The TAI time is 37 seconds ahead of the UTC time and 19 seconds ahead of the GPS time.

Thanks to the C++17 std::chrono::floor⁴, you can display the time point in different granularities. In this case, the time point has to be of type std::chrono::local_time.

# **The local time displayed in different resolutions**

```
```cpp
// timePointsOutputGranularity.cpp

#include <chrono>
#include <iostream>

int main() {

    std::cout << '\n';

    auto now = std::chrono::system_clock::now();

    auto zonedTime = std::chrono::zoned_time(std::chrono::current_zone(), now);
    auto localTime = zonedTime.get_local_time();

    std::cout << "local_time: "
              << localTime << '\n';

    std::cout << "std::chrono::floor<std::chrono::microseconds>(localTime): "
              << std::chrono::floor<std::chrono::microseconds>(localTime) << '\n';

    std::cout << "std::chrono::floor<std::chrono::milliseconds>(localTime): "
              << std::chrono::floor<std::chrono::milliseconds>(localTime) << '\n';

    std::cout << "std::chrono::floor<std::chrono::seconds>(localTime): "
              << std::chrono::floor<std::chrono::seconds>(localTime) << '\n';
}
```
```

⁴https://en.cppreference.com/w/cpp/chrono/duration/floor