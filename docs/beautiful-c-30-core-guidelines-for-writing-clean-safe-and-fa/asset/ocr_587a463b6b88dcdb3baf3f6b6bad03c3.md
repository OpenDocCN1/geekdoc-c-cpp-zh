```
#include <variant>

std::variant<int, float> v;
v = 12;
float f = std::get<float>(v); // Will throw std::bad_variant_access
```