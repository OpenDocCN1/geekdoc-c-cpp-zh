# 8 • Pointers 173

```
a = *ptr; // ptr has not been initialized.
std::cout << a << '\n';
```

For example, if we add the statement ptr = &b; before that, the program is executed successfully; a will be equal to b and the program outputs 10. Typically, in Unix/Linux environment, this type of error is indicated with the pop-up runtime message Segmentation fault. Similarly, in the following code, since ptr has not been initialized, it is important to read a value and save it in *ptr.

```
int *ptr, i;
cin >> *ptr;
```

If we add the statement ptr = &i; before cin, the code is fine; the input value is stored into *ptr, that is, i. Always remember, initialize the pointer before using it, don't let it blowing in the wind. Listen to Blowing in the wind from Bob Dylan to bear in mind. * & cancel each other when used together. For example, the following program displays the addresses of i:

```
#include <iostream> // Example 8.5
int main() {
    int *ptr, i;
    ptr = &i;
    std::cout << &i << ' ' << *ptr << ' ' << &ptr << ' ' '\n';
}
```

Because the /** marks the beginning of a comment, in a statement such as a = b*/ptr; whatever follows/ with /*is is considered, the compilation faults. In case, leave a space or use parentheses. For example, a = b/ptr; or a = b/(*ptr);
Let's see, according to what you've learned so far, can you find the output of the following program?

```
#include <iostream> // Example 8.6
int main() {
    int *ptr1, i = 4;
    double *ptr2, j = 1.78;
    ptr1 = &i;
    ptr2 = &j;
    *ptr1 = i + *ptr2;
    std::cout << i << ' ' << sizeof(ptr1)*sizeof(ptr2) << ' ' << sizeof(ptr2) << ' ' '\n';
    return 0;
}
```

Since ptr1 points to the address of i and ptr2 to the address of j, the statement *ptr1 = i+*ptr2 is equivalent to i+j. Since i is integer, it becomes 5. As said, the pointer variables allocate the same size no matter the type they point to. If we assume that it is 4 octets and ptr2 is a pointer to double, the program displays: 5 16 8