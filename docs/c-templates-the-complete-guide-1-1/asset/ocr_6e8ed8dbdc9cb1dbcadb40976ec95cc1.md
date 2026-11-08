```
```cpp
#include <utility>
#include <iostream>

class X {
    ...
};

void g (X) {
    std::cout << "g() for val\n";
}

void g (X const&) {
    std::cout << "g() for const\n";
}

void g (X&&) {
    std::cout << "g() for movable object\n";
}

// let f() perfect forward argument val to g()

template<typename T>
void f (T&& val)
{
    g(std::forward<T>(val));  // call the right g()
}

int main()
{
    X v;              // create variable

    X const c;        // create constant

    f(v);             // f() for variable calls f(X&)
    f(c);             // f() for constant calls f(X const&)
    f(X());           // f() for temporary calls f(X&&)
    f(std::move(v));  // f() for non-const movable variable
}
```
```

Of course, perfect forwarding can also be used with variadic templates (see Section 4.3 on page 6 for some examples). See Section 15.6.3 on page 336 for details of perfect forwarding.

# 6.2 SPECIAL MEMBER FUNCTION TEMPLATES

Member function templates can also be used as special member functions, including as a constructor, which, however, might lead to surprising behavior.

Consider the following example:

Click here to view code image

```
```cpp
#include <utility>
#include <string>
#include <iostream>

class Person
{
private:
    std::string name;

public:
    // constructor for passed initial name
```
```