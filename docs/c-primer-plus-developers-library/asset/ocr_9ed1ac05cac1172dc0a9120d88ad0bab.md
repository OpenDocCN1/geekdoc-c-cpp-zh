This is starting to look a bit complicated. How can we access data with this array? Well, if arp is an array of pointers, then arp[1] must be a pointer, and we can use the indirect membership operator with it to access a member:

```
std::cout << arp[1]->year << std::endl;
```

We can create a pointer to such an array:

```
const antarctica_years_end ** ppa = arp;
```

Here, arp is the name of an array; hence, it is the address of its first element. But its first element is a pointer, so ppa has to be a pointer to a pointer to const antarctica_years_end, hence the **. There are several ways you could mess up this declaration. For example, you could omit the const, forget an * or two, transpose letters, or otherwise mangle the structure type. Here is an instance for which the C++11 version of auto is convenient. The compiler is perfectly aware of what type arp is, so it can deduce the correct type for you:

```
auto ppb = arp; // C++11 automatic type deduction
```

In the past, the compiler used its knowledge of the correct type to complain about errors you may have made in the declaration; now it can let its knowledge work for you. How can you use ppa to access data? Because ppa is a pointer to a structure, *ppa is a pointer to a structure, so you can use it with the indirect membership operator:

```
std::cout << (*ppa)->year << std::endl;
std::cout << (*(ppb+1))->year << std::endl;
```

Because ppa points to the first member of arp, *ppa is the first member, which is &s01. So (*ppa)->year is the year member of s01. In the second statement, ppb+1 points to the next element, arp[1], which is &s02. The parentheses are needed to get the correct associations. For example, *ppa->year would attempt to apply the * operator to ppa->year, which fails because the year member is not a pointer.

Is all this really true? Listing 4.23 incorporates all the preceding statements into a short program.

# Listing 4.23  **mixtypes.cpp**

```
// mixtypes.cpp -- some type combinations
#include <iostream>

struct antarctica_years_end
{
    int year;
    /* some really interesting data, etc. */
};

int main()
```