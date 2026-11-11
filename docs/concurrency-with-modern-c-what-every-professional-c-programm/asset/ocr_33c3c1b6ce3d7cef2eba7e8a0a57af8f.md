# 16.4.2 Epoch

Thanks to the auxiliary function `time_since_epoch`<sup>9</sup>, each clock returns how much time has passed since the epoch.

Calculating the epoch for each clock

```
```cpp
// now.cpp

#include <chrono>
#include <iomanip>
#include <iostream>

using namespace std::chrono;

template <typename T>
void durationSinceEpoch(const T dur){
    std::cout << "     Seconds since epoch: " << dur.count() << '\n';
    typedef duration<double, std::ratio<60>> MyMinuteTick;
    const MyMinuteTick myMinute(dur);
    std::cout << std::fixed;
    std::cout << "     Minutes since epoch: " << myMinute.count() << '\n';
    typedef duration<double, std::ratio<60*60*24*365>> MyYearTick;
    const MyYearTick myYear(dur);
    std::cout << "     Years since epoch:   " << myYear.count() << '\n';
}

int main(){

    std::cout << '\n';

    system_clock::time_point timeNowSysClock = system_clock::now();
    system_clock::duration timeDurSysClock = timeNowSysClock.time_since_epoch();
    std::cout << "system_clock: " << '\n';
    durationSinceEpoch(timeDurSysClock);

    std::cout << '\n';

    const auto timeNowStdClock = steady_clock::now();
    const auto timeDurStdClock = timeNowStdClock.time_since_epoch();
    std::cout << "steady_clock: " << '\n';
    durationSinceEpoch(timeDurStdClock);

    std::cout << '\n';
```
```

<sup>9</sup> http://en.cppreference.com/w/cpp/chrono/time_point/time_since_epoch