![](bbox=[0.115, 0.099, 0.587, 0.224])

This means that at the end, the vector only has to release the old memory and update its members:

![](bbox=[0.115, 0.27, 0.587, 0.397])

# Conditional noexcept Declarations

However, is it OK to mark the move constructor with `noexcept`? Well, we move the name (a `std::string`) and write something to the standard output stream. If we throw there, we violate the guarantee not to throw. In that case, at runtime the program will call `std::terminate()`, which usually calls `std::abort()` to signal an abnormal end of the program (and often creates a core dump).

Therefore, we should give the guarantee not to throw if the string member and the output operation do not throw. The keyword `noexcept` was introduced because you can use it to specify a conditional guarantee not to throw. It would look as follows (see *basics/personcond.hpp* for the full example):

```
```cpp
class Person {
 private:
   std::string name;
 public:
   ...
   Person(Person&& p)
      noexcept(std::is_nothrow_move_constructible_v<std::string>
                  && noexcept(std::cout << name))
      : name{std::move(p.name)} {
         std::cout << "MOVE " << name << '\n';
      }
   ...
}
```
```

With `noexcept(...)`, we guarantee not to throw if the compile-time expression within the parentheses is true. In this case, we require two things to give the guarantee:

+   - With `std::is_nothrow_move_constructible_v<std::string>` (before C++20, you had to use `std::is_nothrow_move_constructible<std::string>::value`), we use a standard type trait (type function) to tell us whether the move constructor of `std::string` guarantees not to throw.