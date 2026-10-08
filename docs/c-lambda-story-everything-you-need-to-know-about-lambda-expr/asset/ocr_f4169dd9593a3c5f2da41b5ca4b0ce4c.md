possibly have shorter code.

> > Be prepared for the future:
> In C++20 we have lots of constexpr standard algorithms and containers like std::vector and std::string, so constexpr lambdas will be very handy in that context. Your code will look the same for the runtime version as well as for constexpr (compile-time) version!

Let's now move to the second important feature available since C++17:

# Capture of *this

Do you remember the issue when we wanted to capture a class member? 11;

By default, we capture this (as a pointer!), and that's why we might get into trouble when temporary objects go out of scope.

In C++17 we have another way. We can capture a copy of *this 12:

Capturing *this . Live code @Wandbox

```
#include <iostream>

struct Baz {
    auto foo() {
        return [*this] { std::cout << s << std::endl; }
    }
    std::string s;
};

int main() {
    const auto f1 = Baz["xyz"].foo();
    const auto f2 = Baz["abc"].foo();
    f1();
    f2();
}
```

In the example we can now write [*this] which means the lambda captures a copy of the temporary object, a copy of *this . The copy is then saved in the closure object and then there won't be any undefined behaviour when invoking the lambda later.