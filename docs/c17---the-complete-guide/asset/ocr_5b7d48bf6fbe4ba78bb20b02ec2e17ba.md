+   - The value returned by data() can be nullptr. For example, nullptr is returned after initializing a string view with the default constructor.
+   - There is no allocator support.

Due to the possible nullptr value and possible missing null terminator, you should always use size() before accessing characters via operator [] or data() (unless you know better).

# 19.2 Using String Views

There are two major applications of string views:

+   1. You might have allocated or mapped data with character sequences or strings and want to use this data without allocating more memory. Typical examples are the use of memory-mapped files or dealing with substrings in large texts.
+   2. You want to improve the performance for functions/operations that receive strings to simply process them read-only, without needing a trailing null terminator.

A special form of this might be to deal with string literals as objects with an API similar to strings:
std::string_view hello{"hello world"};

```
std::string_view hello{"hello world"};
```

The first application usually means that only string views are passed around, while the programming logic has to ensure that the underlying character sequences remain valid (i.e., the mapped file content is not unmapped). You might use a string view at any time to initialize or assign its value to a std::string.

Beware of using string views just as “the better string.” This can result in performance problems and severe runtime errors. Read the following subsections carefully.

# 19.3 Using String Views as Parameters

A first example of using a string view as a read-only string is a function that prints a collection of elements with a prefix passed as a string view:

```
#include <string_view>
template<typename T>
void printElems(const T& coll, std::string_view prefix = {})
{
  for (const auto& elem : coll) {
    if (prefix.data()) { // check against nullptr
      std::cout << prefix << ' ';
    }
    std::cout << elem << '\n';
  }
}
```

Here, just by declaring that the function will take a std::string_view, we might save a call to allocate heap memory compared to a function that takes a std::string. Details depend on whether short strings are passed and the short string optimization (SSO) is used. For example, if we declare the function as follows: