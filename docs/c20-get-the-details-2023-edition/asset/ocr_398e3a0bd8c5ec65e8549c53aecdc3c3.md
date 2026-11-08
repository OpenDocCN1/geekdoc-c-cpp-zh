# ### 10.29 Race Conditions

A race condition is a situation in which the result of an operation depends on the interleaving (ordering of operations) of certain individual operations.

Race conditions are quite difficult to see. Whether they occur depends on the interleaving of the threads. That means the number of your cores, your system's utilization, or your executable's optimization level may all be reasons why a race condition appears or does not.

# ### 10.30 Regular Type

In addition to the requirements of the concept `SemiRegular`, the concept `Regular` requires that the type is equally comparable.

# ### 10.31 Scalar Type

A scalar type is either an arithmetic type (see `std::is_arithmetic`¹⁹), an enum, a pointer, a member pointer, or a `std::nullptr_t`.

# ### 10.32 SemiRegular

A semiregular type `X` has to support the Big Six and has to be swappable: `swap(X&, X&)`

# ### 10.33 Short-Circuit Evaluation

Short circuit evaluation means that the evaluation of a logical expression automatically stops when its overall result is already determined.

# ### 10.34 Standard-Layout Type

A standard-layout type does not use features that are not available in C. All its members must have the same access specifier. User-defined special members are allowed. The following characteristic holds for standard layout types.

A standard-layout type can only have

+   * non-virtual functions or non-virtual base classes

¹⁹https://en.cppreference.com/w/cpp/types/is_arithmetic