```
#include <iostream>
#include <ratio>

int main()
{
    std::ratio<3,7> rl;
    std::cout << rl.num << " " << rl.den << std::endl;
    typedef std::ratio<4, 8> r2;
    std::cout << r2::num << " " << r2::den << std::endl;
}
// Output
3 : 7
1 : 2
```

Notice that in the declaration: ratio<4, 8>, r2::num and r2::den are reduced to the largest common denominator.

# Durations

std::chrono::duration is a class template that represents a time interval. It is declared as follows:

```
#include <chrono>

template<class Type, class Period = std::ratio<1>>
class duration;
```

A class template has two parameters. Type is an arithmetic type such as int, long, double, float and so forth. This represents the duration in ticks (the number of ticks since the clock's epoch). Period is a parameter of type std::ratio. It represents the number of ticks in a second or the number of seconds from one tick to the next if it is greater than a second. Period is a compile-time rational constant.

Period<1,500> means that there are five thousand ticks in a second. Period<1000,1> (or Period<1000>) means there is a tick every 1000 seconds.