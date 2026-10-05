# Modern C++: Nested Namespaces (C++17)

Consider the nested namespaces:

```
namespace A {
    namespace B {
        namespace C {
            int x = 100;
        }
    }
}
```

In C++17, we can specify the nested namespace C as:

```
namespace A::B::C {
    int x = 100;
}
```

Here is an example:

```
#include <iostream>
namespace A {
    int a = 1;
}
namespace A::B {
    int b = 2;
}
namespace A::B::C {
    int c = 3;
}

int main() {
    std::cout << A::a << " " << A::B::b << " " << A::B::C::c << std::endl;
}

// output
1 2 3
```