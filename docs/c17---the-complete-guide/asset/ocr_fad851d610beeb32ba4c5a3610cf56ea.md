While passing a temporary (which is a prvalue when used) to the function is no longer a copy/move, returning the parameter requires copy/move support because the returned object has a name.

As part of this change, a couple of modifications and clarifications were made in the terminology of value categories.

# 5.2 Benefit of Mandatory Copy Elision for Temporaries

One benefit of this feature is, of course, that better performance is now guaranteed when returning a value that is expensive to copy (although all major compilers did the copy elision anyway). Although move semantics helps to reduce copying costs significantly, not performing copies can still be a significant improvement (e.g., if the objects have many fundamental data types as members). This might reduce the need to use out-parameters rather than simply returning a value (provided the return value is created with the return statement).

Another benefit is the ability to now define a factory function that always works because it can now also return an object even when neither copying nor moving is allowed. For example, consider the following generic factory function:

lang/factory.hpp

```
#include <utility>

template<typename T, typename... Args>
T create(Args&&... args)
{
    ...
    return T{std::forward<Args>(args)...};
}
```

This function can now even be used for a type such as std::atomic<>, where neither the copy nor the move constructor is defined:

lang/factory.cpp

```
#include "factory.hpp"
#include <memory>
#include <atomic>

int main()
{
    int i = create<int>(42);
    std::unique_ptr<int> up = create<std::unique_ptr<int>>(new int{42});
    std::atomic<int> ai = create<std::atomic<int>>(42);
}
```

As another effect, for classes with explicitly deleted move constructors, you can now return temporaries by value and initialize objects with them: