# Implement or request the equality operator

```
```cpp
// equalityComparison.cpp

#include <iostream>

struct MyInt {
    int value;
    explicit constexpr MyInt(int val): value{val} { }
    bool operator==(const MyInt& rhs) const {
        return value == rhs.value;
    }
};

struct MyDouble {
    double value;

    explicit constexpr MyDouble(double val) : value{val} { }
    bool operator==(const MyDouble& rhs) const = default;
};

template <typename T>
constexpr bool areEqual(const T& lhs, const T& rhs) {
    return lhs == rhs;
}

int main() {

    std::cout << std::boolalpha << '\n';

    MyInt myInt1(2011);
    MyInt myInt2(2014);

    std::cout << "areEqual(myInt1, myInt2): "
              << areEqual(myInt1, myInt2) << '\n';

    MyDouble myDouble1(2011);
    MyDouble myDouble2(2014);

    std::cout << "areEqual(myDouble1, myDouble2): "
              << areEqual(myDouble1, myDouble2) << '\n';

    std::cout << '\n';

}
```
```