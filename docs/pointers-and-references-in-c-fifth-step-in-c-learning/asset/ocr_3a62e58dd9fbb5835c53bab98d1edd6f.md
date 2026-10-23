indicates that the value pointed to by the pointer cannot be modified through this pointer.

When we try to modify the value using the `*ptr = 10` assignment, the program fails to compile. It generates a compilation error stating “assignment of read-only location.” This error occurs because the pointer ptr is pointing to a constant value, and attempting to modify a constant value violates the read-only access enforced by the pointer.

A pointer to a constant provides a mechanism to enforce read-only access to the data it points to. It ensures that the value pointed to by the pointer cannot be modified using that pointer. This is useful in scenarios where you want to pass data to a function or share it across multiple parts of the code while ensuring that it remains unchanged.

By declaring a pointer as `const int*`, you are making a promise to the compiler that you won’t modify the value through that pointer. This allows the compiler to perform additional optimizations and guarantees the integrity of the constant data.