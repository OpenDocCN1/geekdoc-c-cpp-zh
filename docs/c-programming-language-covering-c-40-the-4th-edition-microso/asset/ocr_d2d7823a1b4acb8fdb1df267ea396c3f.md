The intuitive rule for mixing of pointers and references is that referents of references (objects) are permitted to contain pointers, but referents of pointers are not permitted to contain references.

Some examples of pointer types are given in the table below:

| Example | Description |
|---|---|
| byte* | Pointer to byte |
| char* | Pointer to char |
| int** | Pointer to pointer to int |
| int*[] | Single-dimensional array of pointers to int |
| void* | Pointer to unknown type |

For a given implementation, all pointer types must have the same size and representation.

Unlike C and C++, when multiple pointers are declared in the same declaration, in C# the * is written along with the underlying type only, not as a prefix punctuator on each pointer name. For example:

```
int* p1, p2; // NOT as int *p1, *p2;
```

The value of a pointer having type T* represents the address of a variable of type T. The pointer indirection operator * (§18.5.1) may be used to access this variable. For example, given a variable P of type int*, the expression *P denotes the int variable found at the address contained in P.

Like an object reference, a pointer may be null. Applying the indirection operator to a null pointer results in implementation-defined behavior. A pointer with value null is represented by all-bits-zero.

The void* type represents a pointer to an unknown type. Because the referent type is unknown, the indirection operator cannot be applied to a pointer of type void*, nor can any arithmetic be performed on such a pointer. However, a pointer of type void* can be cast to any other pointer type (and vice versa).