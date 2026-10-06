```
const int fibonacci[NFonacci] = { 0, 1, 1, 2, 3, 5, 8, 13, 21, 34 };
```

It would have been tempting to declare the constant as a const int variable. Unfortunately, some compilers have issues with const variables as array size specifiers. We will explain the enum keyword later in this appendix.

Iterating through an array is normally done using an integer. For example:

```
for (int i = 0; i < NFonacci; ++i)
std::cout << fibonacci[i] << std::endl;
```

It is also possible to traverse the array using a pointer:

```
const int ptr = &fibonacci[0];
while (ptr != &fibonacci[10]) {
  std::cout << ptr << std::endl;
  ++ptr;
}
```

We initialize the pointer with the address of the first item and loop until we reach the "one past the last" item (the "eleventh" item, fibonacci[10]). At each iteration, the ++ operator advances the pointer to the next item.

Instead of &fibonacci[0], we could have written fibonacci. This is because the name of an array used is automatically converted into a pointer to the first item in the array. Similarly, we could substitute fibonacci + 10 for &fibonacci[10]. This works the other way as well: We can retrieve the contents of the current item using either *ptr or ptr[0] and could access the next item using *(ptr + 1) or ptr[1]. This principle is sometimes called "equivalence of pointers and arrays".

To prevent what it considers to be a gratuitous inefficiency, C++ does not let us pass arrays by function value. Instead, they must be passed by address. For example:

```
#include <iostream>
void printIntegerTable(const int *table, int size)
{
  for (int i = 0; i < size; ++i)
  std::cout << table[i] << std::endl;
}
```