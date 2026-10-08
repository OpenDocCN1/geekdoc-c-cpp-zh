Similarly to capturing global variables, you'll get the same issues with static objects:

Capturing Static Variables. Live code @Wandbox

```
#include <iostream>

void bar() {
    static int static_int = 10;
    std::cout << static_int << std::endl;
    auto foo = []() noexcept { return static_int; };
    foo();
    std::cout << static_int << std::endl;
    const auto increase = []() noexcept { ++static_int; };
    increase();
    std::cout << static_int << std::endl;
    const auto moreIncrease = [static_int]()() noexcept { return static_int; };
    moreIncrease();
    std::cout << static_int << std::endl;
}

int main() {
    bar();
}
```

This time we try to capture a static variable and then change its value, but since it has no automatic storage duration, the compiler cannot do it.

The output:

```
10
11
12
13
```

GCC reports a warning when you capture the variable by name [static_int] and Clang shows an error.

# Capturing a Class Member and the Pointer

Things get a bit more complicated when you're in a class member function, and you want to capture a member variable. Since all data members are related to the this pointer, it also has to be stored somewhere.

Have a look:

Error when capturing a member variable. Live code @Wandbox

```
#include <iostream>

struct Baz {
```