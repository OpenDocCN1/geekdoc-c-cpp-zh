# 682 Pointers

# Program 12.6

```
#include <iostream>
using namespace std;

int main() {
    const int ARRAYSIZE = 5;

    int i, grade[ARRAYSIZE] = {98, 87, 92, 79, 85};

    for (i = 0; i < ARRAYSIZE; i++))
        cout << "\n" << i << " = " << *(grade + i);
    cout << endl;

    return 0;
}
```

In most respects, an array name and a pointer can be interchangeably changed. An array name, however, is a variable, and the address stored in the pointer can be changed by an assignment statement. For example, a statement such as grade = &grade[2] is invalid. This should come as no surprise; the purpose of an array name is to locate the beginning of the array correctly, allowing a programmer to change the address stored in the array defeats this purpose and leads to havoc when array elements are referenced. Expressions taking the address of an array name are invalid because the compiler creates an internal to the computer, not stored in memory, as pointer variables are. Therefore, trying to store the address of grade by using the expression &grade results in a compiler error.

An interesting side to referencing array elements with pointers is that it can be replaced with a subscript reference. For example, if numPtr is declared as a pointer, the expression (numPtr + i) can also be written as numPtr[i], even though numPtr isn't created as an array. As before, when the compiler encounters the subscript notation, it replaces it internally with the pointer notation.

# Dynamic Allocation

As dynamic in a program, sufficient storage for it is assigned from a pool of computer memory locations available to the caller. After memory locations have been reserved for a variable, these locations are fixed for the life of that variable, whether or not they're used. For example, if a function requests storage for an array of 500 integers, the storage is allocated and fixed from the point of the array's definition. If the application requires fewer than 500 integers, the unused allocated storage isn't released back to the system until the array goes out of existence. If, on the other hand, the application requires

> *This topic can be omitted on first reading with no loss of subject continuity.