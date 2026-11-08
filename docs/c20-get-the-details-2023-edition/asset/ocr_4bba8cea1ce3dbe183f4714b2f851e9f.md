![](bbox=[0.12, 0.11, 0.9, 0.32])

A C++17 compiler complains about a discarded object and a discarded error code

Way better, but the program still has a few issues. [[nodiscard]] cannot be used for functions such as a constructor returning nothing. Therefore, the temporary MyType(5, true) (line 35) is still created without a warning. Second, the error messages are too general. As a user of the functions, I want to have a reason why discarding the result is an issue.

Both issues can be solved with C++20. Constructors can be declared as [[nodiscard]], and the warning can have additional information.

# Use of the attribute [[nodiscard]] in C++20

```
```cpp
// nodiscardString.cpp

#include <utility>

struct MyType {

    [[nodiscard("Implicit destroying of temporary MyInt.")]] MyType(int, bool) {}

};

template <typename T, typename ... Args>
[[nodiscard("You have a memory leak.")]]
T* create(Args&& ... args)
{
    return new T(std::forward<Args>(args)...);
}

enum class [[nodiscard("Don't ignore the error code.")]] ErrorCode {
    Okay,
    Warning,
    Critical,
    Fatal
};
ErrorCode errorProneFunction() { return ErrorCode::Fatal; }
```
```