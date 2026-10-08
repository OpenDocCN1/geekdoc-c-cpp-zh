# Capturing Two Variables by Copy and Mutable. Live code @Wandbox

```
#include <iostream>

int main() {
    const auto print = [](const char *str, int x, int y) {
        std::cout << str << " " << x << " " << y << '\n';
    };
    int x = 1, y = 1;
    print("in main()", x, y);
    auto foo = [x, y, &]() mutable {
        ++x;
        ++y;
        print("in foo()", x, y);
    };
    foo();
    print("in main()", x, y);
}
```

Output:

in main(): 1 1
in foo(): 2 2
in main(): 1 1

In the above example, we can change the values of x and y . Since those are only the copies of x and y from the enclosing scope, we don't see their new values after foo is invoked.

On the other hand, if you capture by reference, then you don't need to apply mutable to the lambda to modify the value. This is because the captured member variables are references and cannot be bound inside a const member function, but you can change the referenced values.

> Capturing a Variable by Reference

```
int x = 1;
std::cout << x << '\n';
const auto foo = [&x]()() noexcept { ++x; };
foo();
std::cout << x << '\n';
```

In the above example, the lambda is not mutable, but it can change the referenced value.

One important thing to notice is that when you apply mutable , then you cannot mark your resulting closure object with const as it prevents you from invoking the lambda!