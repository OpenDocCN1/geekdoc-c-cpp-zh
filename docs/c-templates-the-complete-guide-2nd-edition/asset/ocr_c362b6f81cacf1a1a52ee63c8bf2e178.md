```
#include <tuple>
std::tuple<bool, int> bi{true, 42};
auto [b, i] = bi;
int r = i;    // initializes r to 42
```