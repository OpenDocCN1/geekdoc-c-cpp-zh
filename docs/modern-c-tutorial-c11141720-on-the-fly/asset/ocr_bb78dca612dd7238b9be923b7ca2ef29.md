5.3 std::unique_ptr CHAPTER 05 SMART POINTERS AND MEMORY MANAGEMENT

# 5.3 std::unique_ptr

std::unique_ptr is an exclusive smart pointer that prohibits other pointers from sharing the same object, thus keeping the code safe

```
std::unique_ptr<int> pointer = std::make_unique<int>(10); // make_unique was introduced in C++14
std::unique_ptr<int> pointer2 = pointer; // illegal
```

make_unique is not complicated. C++11 does not provide std::make_unique, which can be implemented by itself:

```
template<typename T, typename ...Args>
std::unique_ptr<T> make_unique(Args&&... args) ) {
    return std::unique_ptr<T>(new T(std::forward<Args>(args)...));
}
```

As for why it wasn't provided, Herb Sutter, chairman of the C++ Standards Committee, mentioned in his blog that it was because they were forgotten.

Since it is movable, in other words it cannot be copied. However, we can use std::move to transfer it to other unique_ptr, for example:

```
#include <iostream>
#include <memory>
```

```
struct Foo {
    Foo() { std::cout << "Foo" << std::endl; }
    ~Foo() { std::cout << "-Foo" << std::endl; }
    void foo() { std::cout << ":foo" << std::endl; }
};
```

```
void f(const Foo&) {
    std::cout << "f(const Foo&)" << std::endl;
}
```

```
int main() {
    std::unique_ptr<Foo> p1(std::make_unique<Foo>());

    // p1 is not empty, prints
    if (p1) p1->foo(); {
        std::unique_ptr<Foo> p2(std::move(p1));
    }
}
```