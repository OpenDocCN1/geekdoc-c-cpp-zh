# Chapter 9 Memory Models and Namespaces

Table 9.1 The Five Kinds of Variable Storage

| Description | Duration | Scope | Linkage | How Declared |
|---|---|---|---|--|
| Automatic | Automatic | Block | None | In a block |
| Register | Automatic | Block | None | In a block with the keyword `register` |
| Static with no linkage | Static | Block | None | In a block with the keyword `static` |
| Static with external linkage | Static | File | External | Outside all functions |
| Static with internal linkage | Static | File | Internal | Outside all functions with the keyword `static` |

# Initializing Variables

Static variables are zero-initialized, they may undergo constant expression initialization, and they may undergo dynamic initialization. As you may have surmised, zero-initialization means setting the variable to the zero value. For scalar types, the zero type is cast to the appropriate type. For example, the null pointer, which is initialized by 0 in C++ code, may have a nonzero internal representation, so a pointer variable will be initialized to that value. Structure members are zero-initialized, and any padding bits are set to zero.

Zero-initialization and constant-expression initialization are collectively called static initialization. This means the variable is initialized when the compiler processes the file (or translation unit). Dynamic initialization means the variable is initialized later.

What determines form of initialization takes place? First of all, static variables are zero-initialized, whether or not any initialization is indicated. Next, if the variable is initialized using a constant expression that the compiler can evaluate solely from the file contents (including header files), it can perform constant-expression initialization. The compiler is prepared to do simple calculations if needed. If there's not enough information at this time, the variable will be dynamically initialized. Consider the following:

```
#include <cmath>
int x; // zero-initialization
int y = 5; // constant-expression initialization
long z = 13 * 13; // constant-expression initialization
const double pi = 4.0 * atan(1.0); // dynamic initialization
```

First, x, y, z, and pi are zero-initialized. The compiler evaluates the constant expressions and initializes y and z to 5 and 169, respectively. But initializing pi requires