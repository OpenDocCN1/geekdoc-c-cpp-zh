```
const long cl=11;
static_long<cl> scl; // Error
```

The constant cl cannot be changed in the program. On the other hand, it cannot be used during compilation as it depends on a run-time value. There are scenarios where we cannot say from the program sources what kind of constant we have, for instance:

Click here to view code image

```
const long ri= floor(sqrt(i));
static_long<ri> sri; // ok with most g++ versions
```

Here, ri is known during compilation when sqrt and floor are both constexpr in the implementation of the standard library (e.g., in most g++ versions since 4.7); otherwise it is an error when used as a template argument.

To ensure that a constant has a compile-time value, we have to declare it constexpr:

Click here to view code image

```
constexpr long ri= floor(sqrt(i)); // compiles with g++ 4.7-4.9
```

This guarantees that ri is known during compilation; otherwise this line does not compile. Note that constexpr is stricter for variables than for functions. A constexpr variable accepts only compile-time values while a constexpr function accepts both compile-time and run-time arguments. Evidently, this requires that the type can be represented at compile time:

Click here to view code image

```
constexpr string name1("Herbert"); // Error (currently)
constexpr string_view name2("Herbert"); // Requires C++17
```

A string is (currently) not allowed at compile time4 as it manages memory dynamically whereas a string_view refers external memory available at compile time (in this case a char sequence in the executable).

4. C++20 allows for restricted memory handling at compile time, which should allow for compile-time strings. However, current compilers by the time of writing (g++-10 and clang++-11) still reject this line.