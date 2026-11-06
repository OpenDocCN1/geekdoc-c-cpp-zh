# # *Section 8.2 Pointer Variable Declarations and Initialization*

+   - Pointers are variables that contain as their values memory addresses of other variables.

+   - The declaration

```
```cpp
int* ptr;
```
```

declares `ptr` to be a pointer to a variable of type `int` and is read, “`ptr` is a pointer to `int`.” The `*` as used here in a declaration indicates that the variable is a pointer.

+   - You can initialize a pointer with an address of an object of the same type or with `nullptr` (p. 342).

+   - The only integer that can be assigned to a pointer without casting is `0`.