```
std::chrono::seconds s1; // uninitialized value
std::chrono::seconds s2{}; // zero initialized
```

# What you cannot do in this:

```
std::chrono::seconds s = 3; // Error: not implicitly from int
```

This is very important, because just as important as what you can do with <chrono> is what you cannot do with it. For example, if this initialization were allowed, you would be able to write sleep(3) again, and you would have automatic conversion of int to seconds (or nanoseconds?).

Instead, you need to write:

```
std::chrono::seconds s{};
```

This way, you protect yourself from errors.

You can output time spans like these to a stream. cout << s, for example, outputs 3s. This is possible in C++20. Before that, you would use count() to get the enclosed value:

```
std::cout << s.count() << "\n";
```

Using chrono::duration as a parameter or variable looks like the following listing in practice.

```
// https://cppbolt.org/z/47iH9e7v
#include <chrono>
#include <iostream>
void sleep(std::chrono::seconds dur) {
    std::cout << dur.count() << "s\n";
}
// / ... / ... / ...
int main() {
    using namespace std::chrono;
    sleep(3); // Error: no implicit conversion from int
    sleep(seconds(4)); // okay
    sleep(5s); // okay
    seconds x{6};
    sleep(x);
    auto y = 10s; // Incrementing with seconds
    y += 20s;
    sleep(y); // now 30s
}
```