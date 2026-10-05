# Modern C++: Conversion From ptr To bool (C++20)

A type conversion from a pointer or a pointer-to-member to bool is narrowing and cannot be used unless an explicit cast is done. The exception is that a nullptr can be cast to bool when used in a direct initialization.