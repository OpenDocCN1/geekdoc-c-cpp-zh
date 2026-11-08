```
    void writeName() {
        std::cout << "\nFoo\n";
    }

};

export struct Bar {
    Foo getFoo() {
        return Foo{};
    }
};
```

The module bar exports the class Bar. Bar is visible and reachable. On the contrary, Foo is not visible.

# Using the module bar

```
#include <utility>

import bar;

int main() {

    Bar b;
    // Foo f;
    auto f = b.getFoo();
    f.writeName();

    using FooAlias = decltype(std::declval<Bar>().getFoo());
    FooAlias f2;
    f2.writeName();

}
```

The class Foo is not exported and, therefore, not visible. Its usage in line 6 would cause a linker error. On the contrary, Foo is reachable because the member function getFoo (line 18 in bar.cpp) returns it. Consequently, the function writeName (line 8) can be invoked. Furthermore, I can create a type alias to Foo (line 12), use it to instantiate Foo (line 13), and invoke writeName (line 14) on it. The expression std::declval<Bar>().getFoo() in line 12 returns the object that a call Bar.getFoo() would return. Finally, decltype returns the type of this hypothetical object.