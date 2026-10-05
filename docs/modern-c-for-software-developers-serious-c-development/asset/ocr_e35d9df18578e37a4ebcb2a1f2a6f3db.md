# Modern C++: nullpointer (C++11)

C and C++ define the macro NULL as the integer 0 or 0L. NULL is integer type. A pointer that has the value NULL is interpreted as pointing to no value. This gives rise to ambiguous behaviour:

```
void foo(int);      // forward declaration
char* ptr;
ptr = NULL;
foo(ptr);               // equivalent to calling foo(0)
```

For foo(0) has foo received a pointer or an int?

nullptr is a new keyword in C++11. nullptr is meant to be a replacement for NULL. It is a literal constant of type std::nullptr_t. nullptr provides a typesafe pointer value representing an empty (null) pointer.

nullptr it is not convertible to any integral type. Thus we can perform boolean comparisons:

```
#include <iostream>
void foo(int* ptr) {
    if (ptr == nullptr)
        std::cout << "nullptr received" << std::endl;
    else
        std::cout << *ptr << std::endl;
}
int main() {
    int* ptr;
    ptr = nullptr;
    foo(ptr);
}
```