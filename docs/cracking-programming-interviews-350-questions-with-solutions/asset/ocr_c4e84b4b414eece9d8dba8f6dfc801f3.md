```
```text
void operator=(const A&) = default;

explicit default.cpp:9:5:
error: exception specification of
explicitly defaulted
    destructor does not match the calculated one
    ~A() throw(int) = default;
    ^
4 errors generated.
```
```

+   - `constexpr A() = default;` is ill-formed because implicit `A()` is not `constexpr`
+   - `A(int a = 0) = default;` is ill-formed because of the present of default argument
+   - `void operator=(const A&) = default;` is ill-formed because of non-matching return type
+   - `A() throw(int) = default;` is ill-formed because exception specification does not match.

# ### Question 163 — prevent new instance of class

How to design a class such that its instance cannot be dynamically allocated with `new`?

# ### Solution of Question 163

One can prevent use of a class in certain new expressions by using deleted definitions of a user-declared operator new for that class as shown below.

*Program 12.12: prevent new instance of class*

```
```cpp
#include <stddef>
struct A
{
    void *operator new(std::size_t) = delete;
    void *operator new[](std::size_t) = delete;
};
int main()
{
    A *p = new A;
    A *q = new A[3];
}
```
```

Compiler error is