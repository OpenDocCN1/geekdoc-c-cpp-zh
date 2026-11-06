
If `vPtr` had been incremented to `3016`, which points to `v[4]`, the statement

```cpp
vPtr -= 4;
```

would set `vPtr` back to `3000`—the beginning of the built-in array. If a pointer is being incremented or decremented by one, the increment (`++`) and decrement (`--`) operators can be used. Each of the statements

```cpp
++vPtr;
vPtr++;
```

increments the pointer to point to the built-in array’s *next* element. Each of the statements

```cpp
--vPtr;
vPtr--;
```

decrements the pointer to point to the built-in array’s *previous* element.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1073_0.png)

### Error-Prevention Tip 8.5

*There’s no bounds checking on pointer arithmetic. You must ensure that every pointer arithmetic operation that adds an integer to or subtracts an integer from a pointer results in a pointer that references an element within the built-in array’s bounds.*

## 8.8.2 Subtracting Pointers

Pointer variables pointing to the *same* built-in array may be subtracted from one another. For example, if `vPtr` contains the address `3000` and `v2Ptr` contains the address `3008`, the statement

```cpp
x = v2Ptr - vPtr;
```

would assign to `x` the *number of built-in array elements* from `vPtr` to `v2Ptr`—in this case, `2`. *Pointer arithmetic is meaningful only on a pointer that points to a built-in array.* We cannot assume that two variables of the same type are stored contiguously in memory unless they’re adjacent elements of a built-in array.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1073_1.png)

### Common Programming Error 8.4

*Subtracting or comparing two pointers that do not refer to elements of the same built-in array is a logic error.*

## 8.8.3 Pointer Assignment

A pointer can be assigned to another pointer if both pointers are of the *same* type. Otherwise, a cast operator (normally a `reinterpret_cast`; discussed in **Section 14.8**) must be used to convert the value of the pointer on the right of the assignment to the pointer type on the left of the assignment. The exception to this rule is the **pointer to `void`** (i.e., `void*`), which is a generic pointer capable of representing *any* pointer type. Any pointer to a fundamental type or class type can be assigned to a pointer of type `void*` without casting. However, a pointer of type `void*` *cannot* be assigned directly to a pointer of another type—the pointer of type `void*` must first be *cast* to the proper pointer type.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1074_0.png)

### Common Programming Error 8.5

*Assigning a pointer of one type to a pointer of another (other than `void*`) without using a cast is a compilation error.*

## 8.8.4 Cannot Dereference a `void*`

A `void*` pointer *cannot* be dereferenced. For example, the compiler “knows” that an `int*` points to four bytes of memory on a machine with four-byte integers. Dereferencing an `int*` creates an *lvalue* that is an alias for the `int`’s four bytes in memory. A `void*`, however, simply contains a memory address for an *unknown* data type. You cannot dereference a `void*` because the compiler does *not* know the type of the data to which the pointer refers and thus not the number of bytes.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1075_0.png)

### Common Programming Error 8.6

The allowed operations on `void*` pointers are: comparing `void*` pointers with other pointers, casting `void*` pointers to other pointer types, and assigning addresses to `void*` pointers. All other operations on `void*` pointers are compilation errors.

## 8.8.5 Comparing Pointers

Pointers can be compared using equality and relational operators. Comparisons using relational operators are meaningless unless the pointers point to elements of the same built-in array. Pointer comparisons compare the *addresses* stored in the pointers. A comparison of two pointers pointing to the same built-in array could show, for example, that one pointer points to a higher-numbered element of the built-in array than the other pointer does. A common use of pointer comparison is determining whether a pointer has the value `nullptr`, `0`, or `NULL` (i.e., the pointer does not point to anything).

## 8.9 Relationship Between Pointers and Built-in Arrays

Built-in arrays and pointers are intimately related in C++ and may be used *almost* interchangeably. Pointers can be used to do any operation involving array subscripting.

Assume the following declarations:

```cpp
int b[5]; // create 5-element int array b; b is a const pointer
int* bPtr; // create int pointer bPtr, which isn't a const pointer
```

We can set `bPtr` to the address of the first element in the built-in array `b` with the statement

```cpp
bPtr = b; // assign address of built-in array b to bPtr
```

This is equivalent to assigning the address of the first element as follows:

```cpp
bPtr = &b[0]; // also assigns address of built-in array b to bPtr
```

The expression

```cpp
b += 3;
```

causes a compilation error, because it attempts to *modify* the value of the built-in array’s name with pointer arithmetic.

## 8.9.1 Pointer/Offset Notation

Built-in array element `b[3]` can alternatively be referenced with the pointer expression

```cpp
*(bPtr + 3)
```

The `3` in the preceding expression is the **offset** to the pointer. When the pointer points to the beginning of a built-in array, the offset indicates which built-in array element should be referenced, and the offset value is identical to the subscript. This notation is referred to as **pointer/offset notation**. The parentheses are necessary, because the precedence of `*` is higher than that of `+`. Without the parentheses, the preceding expression would add `3` to a copy of `*bPtr`’s value (i.e., `3` would be added to `b[0]`, assuming that `bPtr` points to the beginning of the built-in array).

Just as the built-in array element can be referenced with a pointer expression, the address

```cpp
&b[3]
```

can be written with the pointer expression

```cpp
bPtr + 3
```

## 8.9.2 Pointer/Offset Notation with the Built-in Array’s Name as the Pointer

The built-in array name can be treated as a pointer and used in pointer arithmetic. For example, the expression

```cpp
*(b + 3)
```

also refers to the element `b[3]`. In general, all subscripted built-in array expressions can be written with a pointer and an offset. In this case, pointer/offset notation was used with the built-in array’s name as a pointer. The preceding expression does *not* modify the built-in array’s name; `b` still points to the built-in array’s first element.

## 8.9.3 Pointer/Subscript Notation

Pointers can be subscripted exactly as built-in arrays can. For example, the expression

```cpp
bPtr[1]
```

refers to `b[1]`; this expression uses **pointer/subscript notation**.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1081_0.png)

### Good Programming Practice 8.3

*For clarity, use built-in array notation instead of pointer notation when manipulating built-in arrays.*

## 8.9.4 Demonstrating the Relationship Between Pointers and Built-in Arrays

**Figure 8.17** demonstrates the four notations we just discussed:

- *array subscript notation*
- *pointer/offset notation with the built-in array’s name as a pointer*
- *pointer subscript notation*
- *pointer/offset notation with a pointer*

to accomplish the same task, namely displaying the four elements of the built-in array of `int`s named `b`.

```cpp
// Fig. 8.17: fig08_17.cpp
// Using subscripting and pointer notations with built-in arrays.
#include <iostream>
using namespace std;

int main() {
    int b[]{10, 20, 30, 40}; // create 4-element built-in array b
    int* bPtr{b}; // set bPtr to point to built-in array b

    // output built-in array b using array subscript notation
    cout << "Array b displayed with:\nArray subscript notation\n";

    for (size_t i{0}; i < 4; ++i) {
        cout << "b[" << i << "] = " << b[i] << '\n';
    }

    // output built-in array b using array name and pointer/offset notation
    cout << "\nPointer/offset notation where "
         << "the pointer is the array name\n";

    for (size_t offset1{0}; offset1 < 4; ++offset1) {
        cout << "*(" << offset1 << ") = " << *(b + offset1) << '\n';
    }

    // output built-in array b using bPtr and array subscript notation
    cout << "\nPointer subscript notation\n";

    for (size_t j{0}; j < 4; ++j) {
        cout << "bPtr[" << j << "] = " << bPtr[j] << '\n';
    }
}
```
