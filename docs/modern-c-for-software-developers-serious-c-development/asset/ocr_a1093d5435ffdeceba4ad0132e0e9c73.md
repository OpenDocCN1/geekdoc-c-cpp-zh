# Modern C++: Constexpr Functions (C++14)

C++14 allows more expressions inside the body of constexpr functions:

+   - local variable declarations are allowed inside constexpr functions provided they are not static or thread_local declarations. Local variables must be initialized.

+   - if, switch, for, while, do-while expressions are allowed inside constexpr functions.