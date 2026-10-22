+   - `invoke_result<>` is available since C++17 and replaces `result_of<>`, which is deprecated since C++17, because `invoke_result<>` provides some improvements such the easier syntax and permitting abstract types for T.
+   - For example:

[Click here to view code image](#)

```
std::string foo(int);

using R0 = typename std::result_of<decltype(&foo)(int)>::type; // C++11
using R1 = std::result_of_t<decltype(&foo)(int)>; // C++14
using R2 = std::invoke_result_t<decltype(foo), int>; // C++17

struct ABC {
virtual ~ABC() = 0;
void operator() (int) const {
}
};

using T1 = typename std::result_of<ABC(int)>::type; // ERROR: ABC is abstract
using T2 = typename std::invoke_result<ABC, int>::type; // OK since C++17
```

See Section 11.1.3 on page 163 for a full example.

# D.3.2 Test for Specific Operations

| Trait | Effect |
|---|---|
| `is_constructible<T, Args...>` | Can initialize type *T* with types *Args* |
| `is_trivially_constructible<T, Args...>` | Can trivially initialize type *T* with types *Args* |
| `is_nothrow_constructible<T, Args...>` | Can initialize type *T* with types *Args* and that operation can’t throw |
| `is_default_constructible<T>` | Can initialize *T* without arguments |