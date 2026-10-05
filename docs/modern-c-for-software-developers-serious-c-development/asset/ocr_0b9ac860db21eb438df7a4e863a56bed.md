```
time_struct = system_clock::to_t (today);
std::cout << "today is: " << ctime(&time_struct);

time_struct = system_clock::to_t (tomorrow);
std::cout << "tomorrow is: " << ctime(&time_struct);
```

Output:
today is: Thu Aug 18 06:01:48 2022
tomorrow will be: Fri Aug 19 06:01:48 2022

# Elapsed Time Calculation

Here is an example of an elapsed time calculation:

```
#include <iostream>
#include <chrono>

int main() {
    std::chrono::steady_clock clock;
    std::chrono::time_point start = clock.now();

    // do some work
    double sum=0;
    for (int ctr = 0; ctr < 1'000'000'000; ctr++)
        sum += ctr;

    std::chrono::time_point end = clock.now();
    std::chrono::duration dur = end - start;

    std::chrono::milliseconds msecs =
        std::chrono::duration_cast<std::chrono::milliseconds>(dur);

    std::cout << msecs.count() << std::endl;
}

# output
3731
```