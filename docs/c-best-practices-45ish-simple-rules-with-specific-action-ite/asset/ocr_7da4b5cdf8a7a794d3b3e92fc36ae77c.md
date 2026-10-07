# # 3. Use the Tools: Automated Tests

You need a single command to run tests.
If you don't have that, no one will run the tests.

+   - Catch2¹ - popular and well supported testing framework from Phil Nash²
and Martin Hořeňovský³
- doctest⁴ - similar to catch2, but trimmed for compile-time performance
- Google Test⁵
- Boost.Test⁶ - testing framework, boost style.

ctest⁷ is a test runner for CMake that can be used with any of the frame-works. It is utilized via the add_test⁸ feature of CMake.

You need to be familiar with these tools, what they do, and pick from them.
Without automated tests, the rest of this book is pointless. You cannot apply the practical exercises if you cannot verify that you did not break the existing code.
Oleg Rabaev of CppCast stated:

+   - If a component is hard to test, it is not properly designed.
- If a component is easy to test, it is a good indication that it is properly designed.

> ¹https://github.com/catchorg/Catch2
²https://twitter.com/phil_nash
³https://twitter.com/horenmar_ctu
⁴https://github.com/onctam/doct
⁵https://github.com/google/googletest
⁶https://www.boost.org/libs/1_74_0/libs/test/doc/html/index.html
⁷https://cmake.org/cmake/cmake/help/latest/manual/ctest.1.html
⁸https://cmake.org/cmake/cmake/help/latest/command/add_test.html