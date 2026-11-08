# A formatter for a single value supporting a format specifier (inheritance)

```
```cpp
// formatSingleValueInheritance.cpp

#include <format>
#include <iostream>

class SingleValue {
public:
    SingleValue() = default;
    explicit SingleValue(int s): singleValue{s} {}
    int getValue() const {
        return singleValue;
    }
private:
    int singleValue{};
};

template<>
struct std::formatter<SingleValue> : std::formatter<int> {
    auto format(const SingleValue& singleValue, std::format_context& context) const {
        return std::formatter<int>::format(singleValue.getValue(), context);
    }
};

int main() {

    std::cout << '\n';

    SingleValue singleValue{};
    SingleValue singleValue2020{2020};
    SingleValue singleValue2023{2023};

    std::cout << std::format("{:*>10}", singleValue) << '\n';
    std::cout << std::format("{:*>10}", singleValue2020) << '\n';
    std::cout << std::format("{:*>10}", singleValue2023) << '\n';

    std::cout << '\n';

}
```
```

I derive `std::formatter<SingleValue>` from `std::formatter<int>` (line 18). Only the format functions must be implemented. The output of this program is identical to the output of the previous program `formatSingleValueDelegation.cpp`.