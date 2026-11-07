The program has the following output:

```
std::is_nothrow_move_constructible<Base>: false
is_nothrow_movable<Base>:                  true
```

Therefore, if you have to implement the move constructor in a class derived from an abstract base class, you could use such a helper type trait to declare the move constructor as follows:

```
class Drv : public Base {
    MemType member;
    ...
    // move constructor:
    Drv(Drv&&) noexcept(is_nothrow_move_v<Base> &&
                        is_nothrow_move_v<MemType>);
};
```

To not having the need to implement all pure virtual functions, a compiler supported type trait is missing in the C++ standard.

# 7.4 When and Where to Use noexcept

As seen, noexcept was introduced in C++11 as a response to the problem that we cannot use move semantics when reallocating elements in a vector.

In principle, you can now mark every function with a (conditional) noexcept. This might not only help in situations like vector reallocations (note that the move constructor might then call other functions where we also need the noexcept guarantee), but we might also help the compiler to optimize code because no code has to be generated to handle exceptions. So the question is, where to place noexcept in your code?

For the C++11 standard library, we were in a hurry to decide where to place noexcept (the reallocation problem was detected very late and the final semantic meaning of noexcept was clarified right in the week where we shipped C++11). Therefore, we followed a pretty conservative approach that was proposed in http://wg21.link/n3279, which could also be a useful guideline for your code. Roughly speaking, the guideline is:

+   - Each library function that the library working group agree cannot throw and that has a “wide contract” (i.e., does not specify undefined behavior due to a precondition) should be marked as unconditionally noexcept.
+   - If a library swap function, move constructor, or move assignment operator is ”conditionally wide” (i.e., can be proven not to throw by applying the noexcept operator), then it should be marked as conditionally noexcept. No other function should use a conditional noexcept specification.
+   - No library destructor should throw. It should use the implicitly supplied (non-throwing) exception specification.
+   - Library functions designed for compatibility with C code may be marked as unconditionally noexcept.

The following examples demonstrate what the first item means:

+   - For containers and strings, the member functions empty() and clear() are marked with noexcept because there is no useful way to implement them in a way that they might throw.