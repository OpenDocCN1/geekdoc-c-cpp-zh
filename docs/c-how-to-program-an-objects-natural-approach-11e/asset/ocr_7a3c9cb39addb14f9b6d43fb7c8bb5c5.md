```
```cpp
// fig12_06.cpp
// Demonstrating standard new throwing bad_alloc when memory
// cannot be allocated.
#include <array>
#include <format>
#include <iostream>
#include <memory>
#include <new> // bad_alloc class is defined here

int main() {
    std::array<std::unique_ptr<double[]>, 1000> items{};

    // aim each unique_ptr at a big block of memory
    try {
        for (int i{}; auto& item : items) {
            item = std::make_unique<double[]>(500'000'000);
            std::cout << std::format(
                "items[{}] points to 500,000,000 doubles\n", i++);
        }
    }
    catch (const std::bad_alloc& memoryAllocationException) {
        std::cerr << std::format("Exception occurred: {}\n",
            memoryAllocationException.what());
    }
}
```
```

![](bbox=[0.166, 0.498, 0.834, 0.668])

**Fig. 12.6** | new throwing `bad_alloc` on failure.

# 12.8.2 new Returning nullptr on Failure

You should use the version of `new` that throws `bad_alloc` exceptions on failure. However, the C++ standard specifies you also can use the version of `new` that returns `nullptr` upon failure—this version is useful in systems that do not allow exception handling. For this purpose, header `<new>` defines object `std::nothrow` (of type `nothrow_t`), which is used as follows:

```
```cpp
std::unique_ptr<double[]> ptr{
    new(std::nothrow) double[500'000'000]};
```
```

You cannot use `make_unique` here because it uses the default version of `new`.