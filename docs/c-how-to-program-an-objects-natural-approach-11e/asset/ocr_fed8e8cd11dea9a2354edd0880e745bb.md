```
```cpp
// fig07_09.cpp
// Attempting to modify a constant pointer to constant data.
#include <iostream>

int main() {
   int x{5};
   int y{6};

   // ptr is a constant pointer to a constant integer.
   // ptr always points to the same location; the integer
   // at that location cannot be modified.
   const int* const ptr{&x};

   std::cout << *ptr << '\n';

   *ptr = 7; // error: *ptr is const; cannot assign new value
   ptr = &y; // error: ptr is const; cannot assign new address
}
```
```

*Compiler error messages from Clang in Xcode:*

```
```text
fig07_09.cpp:16:9: error: read-only variable is not assignable
    *ptr = 7; // error: *ptr is const; cannot assign new value
    ~~~~~^

fig07_09.cpp:17:8: error: cannot assign to variable 'ptr' with const-qualified type 'const int *const'
    ptr = &y; // error: ptr is const; cannot assign new address
    ~~~ ^
```
```

**Fig. 7.9** Attempting to modify a constant pointer to constant data.

# Checkpoint

+   1. *(Code)* Write code that declares `temperaturePtr` as a nonconstant pointer to constant `double` data and initialize the pointer to `nullptr`.
+   
+      **Answer:** `const double* temperaturePtr{nullptr};`

+   2. *(Code)* Consider the following code:
+   
+      ```cpp
+      int x{3};
+      int y{5};
+      int* const ptr{&x};
+      *ptr = 7;
+      ptr = &y;
+      ```
+   
+      Why is the first assignment allowed but the second assignment disallowed?
+   
+      **Answer:** The first assignment is allowed because `*ptr` is not const. The second assignment is disallowed because `ptr` is const, so it cannot be aimed at another variable.

+   3. *(Code)* What's wrong with the following declaration?
+   
+      ```cpp
+      const double* const temperaturePtr;
+      ```
+   
+      **Answer:** `temperaturePtr` is a constant pointer, so it must be initialized to point to a double variable.