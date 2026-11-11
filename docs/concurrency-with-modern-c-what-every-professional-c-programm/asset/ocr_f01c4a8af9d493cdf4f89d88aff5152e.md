![](bbox=[0.19, 0.114, 0.811, 0.325])

The valid range of `std::chrono::system_clock`

You can add time durations to time points to get new time points. Adding time durations beyond the valid time range is undefined behavior.

# 16.2.2 Cross the valid Time Range

The following example uses the current time and adds or subtracts 1000 years. For the sake of simplicity, I ignore leap years and assume that a year has 365 days.

# Crossing the valid time range

```
```cpp
// timepointAddition.cpp

#include <chrono>
#include <ctime>
#include <iostream>
#include <string>

using namespace std::chrono;
using namespace std;

string timePointAsString(const time_point<system_clock>& timePoint){
    time_t tp= system_clock::to_time_t(timePoint);
    return asctime(gmtime(&tp));
}

int main(){

    cout << '\n';

    time_point<system_clock> nowTimePoint= system_clock::now();
    cout << "Now: " << timePointAsString(nowTimePoint) << '\n';
```
```