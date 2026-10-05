```
#include <iostream>
#include <chrono>
#include <ratio>

int main()
{
    std::chrono::duration<long, std::ratio<1>> dr1(100);
    std::cout << "duration = " << dr1.count() << std::endl;

    std::chrono::duration<long, std::ratio<60, 1>> dr2(50);
    std::cout << "duration = " << dr2.count() << std::endl;

    std::chrono::duration<double, std::ratio<1, 2>> dr3(100);
    std::cout << "duration = " << dr3.count() << std::endl;

    // add two duration objects
    auto dr4 = dr1 + dr2;
    std::cout << "duration = " << dr4.count() << std::endl;

    // subtract duration objects
    auto dr5 = dr2 - dr1;
    std::cout << "duration = " << dr5.count() << std::endl;

    return 0;

    // output
    duration = 100
    duration = 50
    duration = 100
    duration = 3100
    duration = 2900
```

The function template std::duration_cast converts a duration object to a duration object with a different period. Since the compiler will implicitly convert the periods of duration objects to a common period, this function is only needed if there is a loss of precision when converting between duration types. The duration_cast function template is declared as follows:

```
template <class ToDuration, class Rep, class Period>
constexpr ToDuration duration_cast(const duration<Rep, Period>& d);
```

ToDuration is the duration type that we are casting to. The parameter inside duration cast is some duration object.