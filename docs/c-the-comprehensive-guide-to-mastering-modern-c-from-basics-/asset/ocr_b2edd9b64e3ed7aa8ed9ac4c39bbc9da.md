+   - Write template <typename TYPE> in the line before the
function.

Done. It looks like the following listing for max2.

```
// https://godbot.org/z/acMjvcSMS
#include <string>
#include <cmath> // sin, cos
template<typename TYPE>
constexpr TYPE max2(const TYPE &a, const TYPE &b)
{ return a > b ? a : b; }
int main() {
    double e = max2(sin(3.141592/2), cos(3.141592/2));
    double i = max2(10+45, 100/50);
    std::string s = max2(std::string("Ernie"), std::string("Bert\));
}
```

**Listing 21.6** A simple function template is much better than a macro.

Congratulations! You have written your first function
template. This implementation is as flexible as a macro,
as as fast as overloaded functions, and most importantly,
type-safe.

And starting from C++20, even abbreviated function
templates are possible:

```
constexpr auto max2(const auto &a, const auto &b) { return a > b ? a :
b; }
```

If you want, you can even add overloads for individual
types. And that's exactly what you should do if you want
to get rid of the annoying explicit conversions to
std::string for the arguments to "Ernie" and "Bert". If you
omit them here, the compiler will try to find an overload
for max2(const char[6], const char[5]). It won't succeed
because they are two different types—but in the