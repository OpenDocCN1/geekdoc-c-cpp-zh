The complete implementation is even more complex. To support `std::ref()` and `std::cref()`, the function also unwraps instances of `std::reference_wrapper` into real references.

The C++ standard library now perfectly forwards passed arguments in many places in a similar way, often combined with using `std::decay<>`.

# 7.7 SUMMARY

+   - When testing templates, use string literals of different length.
+   - Template parameters passed by value decay, while passing them by reference does not decay.
+   - The type trait `std::decay<>` allows you to decay parameters in templates passed by reference.
+   - In some cases `std::decay<>` and `std::ref()` allow you to pass arguments by reference when function templates declare them to be passed by value.
+   - Passing template parameters by value is simple but may not result in the best performance.
+   - Pass parameters to function templates by value unless there are good reasons to do otherwise.
+   - Ensure that return values are usually passed by value (which might mean that a template parameter can't be specified directly as a return type).
+   - Always measure performance when it is important. Do not rely on intuition; it's probably wrong.

+   1. A constant rvalue reference `X const&&` is also possible but there is no established semantic meaning for it.
+   
+   2. Note that since C++17 you can pass temporary entities (rvalues) by value even if no copy or move constructor is available (see Section 8.2.1 on page 676). So, since C++17 the additional constraint is that copying for values is not possible.
+   
+   3. The implementation of the string class might itself have some optimizations to make copying cheaper. One is the small string optimization (SSO), using some memory directly inside the object to hold the value without allocating memory or using the value in the value of the object. Another is copy-on-write optimization, which creates a copy using the same memory as the source as long as neither source nor the copy is modified. However, the copy-on-write optimization has significant drawbacks in multithreaded code. For this reason, it is forbidden for standard strings since C++11.
+   
+   4. The term decay comes from C, and also applies to the type conversion from a function to a function pointer (see Section 11.1.1 on page 159).
+   
+   5. The use of `const_cast` is another, more explicit, way to modify the referenced object.
+   
+   6. When passing `std::move(c)`, `std::move()` first converts `c` to `std::string const&`, which then has the effect that `T` is deduced as `std::string const`.
+   
+   7. You can also call `get()` on a reference wrapper and use it as a function object.
+   
+   8. See C++11 library issue 18 [LWG] for details.