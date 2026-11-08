For this purpose, you can use a special form of `new` to enforce `nullptr` behavior.

```
```cpp
// https://godbolt.org/z/s8KoE4TS
#include <new> // nothrow
std::string *ps = new(std::nothrow) std::string{};
if(ps == nullptr) {
    std::cerr << "Memory allocation failed\n";
    return SOME_ERROR;
}
```
```

**Listing 17.11** Nothrow-new does not throw “bad_alloc”, but returns “nullptr”.

A new called in this way never throws an exception (although the called constructor might). Instead, it returns a `nullptr` in the case of an error.

> **Tip**
> 
> Prefer RAII when designing your objects: write code that utilizes RAII.