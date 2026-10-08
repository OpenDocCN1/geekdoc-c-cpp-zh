This syntax, however, will be possible with C++20, see in this section .

# Improvements for Existing Issues

All in all, new C++14 feature can solve a few problems, for example with movable only types or allow some extra optimisation.

Let's review now.

# Move

Previously, in C++11, you couldn't capture a unique pointer by value. Only capturing by reference was possible. Now, since C++14, we can move an object into a member of the closure type:

Capturing a movable type code @Wandbox

```
#include <iostream>
#include <memory>

int main() {
    std::unique_ptr<int> p(new int{10});
    const auto bar = [ptr=move(p)] {
        std::cout << "pointer in lambda: " << ptr.get() << '\n';
    };
    std::cout << "pointer in main: " << p.get() << '\n';
bar();
}
```

# The output:

```
pointer in main(): 0
pointer in lambda: 0x1413c20
```

Thanks to the closure initialiser you can move the pointer ownership into lambda. As you can see in the example the unique pointer is set to nullptr just after the closure is created. When you call a lambda, then you'll see a valid memory address.

# One Gotcha with std::function

Having a movable-only captured variable in a lambda makes the closure object not copyable. This might be an issue if you want to store such a lambda in std::function which accepts only copyable callable objects.

We can observe this in detail if we run C++Insights on the previous example