```
basics/move2.cpp

#include <utility>
#include <iostream>

class X {
...;
};

void g (X&) {
std::cout << "g() for variable\n";
}
void g (X const&) {
std::cout << "g() for constant\n";
}
void g (X&&) {
std::cout << "g() for movable object\n";
}

// let f() perfect forward argument val to g():
template<typename T>
void f (T&& val) {
g(std::forward<T>(val)); // call the right g() for any passed argument
val
}

int main()
{
X v; // create variable
X const c; // create constant

f(v); // f() for variable calls f(X&) => calls g(X&)
f(c); // f() for constant calls f(X const&) => calls g(X const&)
f(X()); // f() for temporary calls f(X&&) => calls g(X&&)
f(std::move(v)); // f() for move-enabled variable calls f(X&&) =>
calls g(X&&)
}
```

Of course, perfect forwarding can also be used with variadic templates (see Section 4.3 on page 60 for some examples). See Section 15.6.3 on page 280 for details of perfect forwarding.

# 6.2 Special Member Function Templates

Member function templates can also be used as special member functions, including as a constructor, which, however, might lead to surprising behavior.
Consider the following example: Click here to view code image