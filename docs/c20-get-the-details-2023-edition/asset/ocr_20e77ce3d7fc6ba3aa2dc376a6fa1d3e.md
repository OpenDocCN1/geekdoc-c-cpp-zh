```
```text
Hello world from main: /app/example.cpp:int main() in (21, 8)

Hello world from func: /app/example.cpp:void func() in (17, 8)
```
```

Displaying log information with the GCC compiler

# 5.7.5 `std::to_address`

`std::to_address(p)` returns the address of p without forming a reference to the object pointed to by p. The utility function `std::to_address` can handle raw pointers and fancy pointers (smart pointers) uniquely.

Displaying the address of raw pointers and smart pointers in an unique way

```
```cpp
// toAddress.cpp

#include <iostream>
#include <memory>

int main() {

    std::cout << '\n';

    int myInt[5];

    int* pMyInt{&myInt};
    std::cout << "std::to_address(pMyInt): " << std::to_address(pMyInt) << '\n';

    auto uniq = std::make_unique<int>(5);
    std::cout << "std::to_address(uniq): " << std::to_address(uniq) << '\n';
    std::cout << "std::to_address(uniq.get()): " << std::to_address(uniq.get()) << '\n';

    auto shar = std::make_shared<int>(5);
    std::cout << "std::to_address(shar): " << std::to_address(shar) << '\n';
    std::cout << "std::to_address(shar.get()): " << std::to_address(shar.get()) << '\n';

    std::cout << '\n';

}
```
```