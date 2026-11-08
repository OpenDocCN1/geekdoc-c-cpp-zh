# Pack Expansion in Init-Capture

```
```cpp
// packExpansionInitCapture.cpp

#include <iostream>
#include <memory>
#include <utility>

template<typename Callable, typename ... Args>
auto packExpansion(Callable call, Args ... args) {
    return [call, ...args = std::move(args)] {
        return call(args...);
    };
}

void func(int fir, double sec, bool thi) {
    std::cout << std::boolalpha;
    std::cout << "fir: " << fir << '\n';
    std::cout << "sec: " << sec << '\n';
    std::cout << "thi: " << thi << '\n';
}

int main() {

    std::cout << '\n';

    auto lamb1 = packExpansion(func, 1, 2, true);
    lamb1();

    std::cout << '\n';

}
```
```

In line 10, I apply pack expansion in init-capture. Due to syntactical restrictions, the ellipsis is before args: [call, ...args = std::move(args)].