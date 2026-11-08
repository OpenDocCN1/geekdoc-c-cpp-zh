# 13.10.10  Un-“const” with “mutable”

Psssst! Here’s a secret for you, and you must not tell anyone. And don’t use it, okay? You can make a field mutable in a class, even if you are currently in a const method.

By doing this, you bypass the assurance that the compiler provides you. But sometimes you have to make an exception. For example, if you want to count the number of calls to a method for analysis purposes, which is actually const.

```
```cpp
// https://godbolt.org/z/sPorknEbd
#include <iostream>
class Data {
    int value_;
    mutable size_t getCount_{0};
public:
    explicit Data(int v) : value_{v} { }
    ~Data() {
        std::cout << "get was used " << getCount_ << " times\n";
    }
    int get() const {
        ++getCount_;
        return value_;
    }
};
int main() {
    Data d{42};
    for (int i=0; i<10; ++i) { d.get(); }
} // Output: get was used 10 times
```
```

**Listing 13.20** “mutable” makes a data field in const methods mutable.

If you were to omit `mutable`, the `++getCount_` expression in `get()` would be an error. In methods marked with `const`, it is not possible to modify instance data fields. With `mutable`, you can make an exception for a single field.

And you should treat mutable as an exception: use it only for analysis. If you need it for another reason, reconsider your design.

You can also append a mutable to a lambda. I describe this in more detail in Chapter 23, Section 23.3.6 under the “Mutable Lambdas” section.

# 13.10.11  Const-Correctness

A related and very helpful aspect in the long run is to get used to the correct use of const. Coming from C (or Java), this probably means using more of it. Once in the C++