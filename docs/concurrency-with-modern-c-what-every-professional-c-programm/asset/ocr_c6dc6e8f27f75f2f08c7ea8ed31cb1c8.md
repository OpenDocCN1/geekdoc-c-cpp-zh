# 16.4 Clocks

The fact that there are three different types of clocks begs the question: What are the differences?

+   - **std::chrono::system_clock**: is the system-wide real-time clock (wall-clock). The clock has the auxiliary functions `to_time_t` and `from_time_t` to convert time points into calendar time.
+   - **std::chrono::steady_clock**: is the only clock to provide the guarantee that you cannot adjust it. Therefore, `std::chrono::steady_clock` is the preferred clock to measure time intervals.
+   - **std::chrono::high_resolution_clock** is the clock with the highest accuracy but it can be simply an alias for the clocks `std::chrono::system_clock` or `std::chrono::steady_clock`.

![](bbox=[0.117, 0.338, 0.176, 0.383])

# No guarantees about the accuracy, starting point, and valid time range

The C++ standard provides no guarantee about the accuracy, the starting point or the valid time range of the clocks. Typically, the starting point of `std::chrono::system_clock` is the 1.1.1970, the so-called UNIX-epoch, while for `std::chrono::steady_clock` it is usually the boot time of your PC.

# 16.4.1 Accuracy and Steadiness

It is pretty interesting to know which clocks are steady and what accuracy they provide. Steady means that the clock cannot be adjusted. You can get the answers directly from the clocks.

Accuracy and steadiness of the three clocks

```
```cpp
// clockProperties.cpp

#include <chrono>
#include <iomanip>
#include <iostream>

using namespace std::chrono;
using namespace std;

template <typename T>
void printRatio(){
    cout << " precision: " << T::num << "/" << T::den << " second " << '\\n';
    typedef typename ratio_multiply<T, milli>::type MilliSec;
    typedef typename ratio_multiply<T, mega>::type MicroSec;
    cout << fixed;
}
```
```

[https://en.wikipedia.org/wiki/Wall-clock_time](https://en.wikipedia.org/wiki/Wall-clock_time)