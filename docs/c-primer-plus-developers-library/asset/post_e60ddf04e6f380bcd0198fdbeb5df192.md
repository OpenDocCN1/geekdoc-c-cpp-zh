
## Listing 4.22 delete.cpp

```cpp
// delete.cpp -- using the delete operator
#include <iostream>
#include <cstring>        // or string.h
using namespace std;
char * getname(void);     // function prototype
int main()
{
    char * name;          // create pointer but no storage

    name = getname();     // assign address of string to name
    cout << name << " at " << (int *) name << "\n";
    delete [] name;       // memory freed

    name = getname();     // reuse freed memory
    cout << name << " at " << (int *) name << "\n";
    delete [] name;       // memory freed again
    return 0;
}

char * getname()          // return pointer to new string
{
    char temp[40];        // temporary storage
    cout << "Enter last name: ";
    cin >> temp;
    char * pn = new char[strlen(temp) + 1];
    strcpy(pn, temp);     // copy string into smaller space

    return pn;            // temp lost when function ends
}
```

Here is a sample run of the program in Listing 4.22:

```text
Enter last name: Plopper
Plopper at 0x004326b8
Enter last name: Pook
Pook at 0x004301c8
```

## Program Notes

Consider the function getname() in the program in Listing 4.22. It uses cin to place an input word into the temp array. Next, it uses new to allocate new memory to hold the word. Including the null character, the program needs strlen(temp) + 1 characters to store the string, so that's the value given to new. After the space becomes available, getname() uses the standard library function strcpy() to copy the string from temp to the new block. The function doesn't check to see whether the string fits, but getname() covers that by requesting the right number of bytes with new. Finally, the function returns pn, the address of the string copy.

In `main()`, the return value (the address) is assigned to the pointer name. This pointer is defined in `main()`, but it points to the block of memory allocated in the `getname()` function. The program then prints the string and the address of the string.

Next, after it frees the block pointed to by name, `main()` calls `getname()` a second time. C++ doesn’t guarantee that newly freed memory is the first to be chosen the next time `new` is used, and in this sample run, it isn’t.

Note in this example that `getname()` allocates memory and `main()` frees it. It’s usually not a good idea to put new and delete in separate functions because that makes it easier to forget to use `delete`. But this example does separate new from delete just to show that it is possible.

To appreciate some of the more subtle aspects of this program, you should know a little more about how C++ handles memory. So let’s preview some material that’s covered more fully in Chapter 9.

## Automatic Storage, Static Storage, and Dynamic Storage

C++ has three ways of managing memory for data, depending on the method used to allocate memory: automatic storage, static storage, and dynamic storage, sometimes called the *free store* or *heap*. Data objects allocated in these three ways differ from each other in how long they remain in existence. We’ll take a quick look at each type. (C++11 adds a fourth form called *thread storage* that we’ll discuss briefly in Chapter 9.)

### Automatic Storage

Ordinary variables defined inside a function use *automatic storage* and are called *automatic variables*. These terms mean that the variables come into existence automatically when the function containing them is invoked, and they expire when the function terminates. For example, the `temp` array in Listing 4.22 exists only while the `getname()` function is active. When program control returns to `main()`, the memory used for `temp` is freed automatically. If `getname()` returned the address of `temp`, the name pointer in `main()` would be left pointing to a memory location that would soon be reused. That’s one reason you have to use `new` in `getname()`. Actually, automatic values are local to the block that contains them. A *block* is a section of code enclosed between braces. So far, all our blocks have been entire functions. But as you’ll see in the next chapter, you can have blocks within a function. If you define a variable inside one of those blocks, it exists only while the program is executing statements inside the block.

Automatic variables typically are stored on a *stack*. This means that when program execution enters a block of code, its variables are added consecutively to the stack in memory and then are freed in reverse order when execution leaves the block. (This is called a *last-in, first-out*, or *LIFO*, process.) So the stack grows and shrinks as execution proceeds.

> **Note**
> 
> Pointers are among the most powerful of C++ tools. They are also the most dangerous because they permit computer-unfriendly actions, such as using an uninitialized pointer to access memory or attempting to free the same memory block twice. Furthermore, until you get used to pointer notation and pointer concepts through practice, pointers can be confusing. Because pointers are an important part of C++ programming, they weave in and out of future discussions in this book. This book discusses pointers several more times. The hope is that each exposure will make you more comfortable with them.

## Combinations of Types

This chapter has introduced arrays, structures, and pointers. These can be combined in various ways, so let’s review some of the possibilities, starting with a structure:

```cpp
struct antarctica_years_end
{
    int year;
    /* some really interesting data, etc. */
};
```

We can create variables of this type:

```cpp
antarctica_years_end s01, s02, s03;  // s01, s02, s03 are structures
```

We can then access members using the membership operator:

```cpp
s01.year = 1998;
```

We can create a pointer to such a structure:

```cpp
antarctica_years_end * pa = &s02;
```

Provided the pointer has been set to a valid address, we then can use the indirect membership operator to access members:

```cpp
pa->year = 1999;
```

We can create arrays of structures:

```cpp
antarctica_years_end trio[3];  // array of 3 structures
```

We can then use the membership operator to access members of an element:

```cpp
trio[0].year = 2003;  // trio[0] is a structure
```

Here trio is an array but trio[0] is a structure, and trio[0].year is a member of that structure. Because an array name is a pointer, we also can use the indirect membership operator:

```cpp
(trio+1)->year = 2004;  // same as trio[1].year = 2004;
```

We can create an array of pointers:

```cpp
const antarctica_years_end * arp[3] = {&s01, &s02, &s03};
```

This is starting to look a bit complicated. How can we access data with this array? Well, if arp is an array of pointers, then arp[1] must be a pointer, and we can use the indirect membership operator with it to access a member:

```cpp
std::cout << arp[1]->year << std::endl;
```

We can create a pointer to such an array:

```cpp
const antarctica_years_end ** ppa = arp;
```

Here, arp is the name of an array; hence, it is the address of its first element. But its first element is a pointer, so ppa has to be a pointer to a pointer to const antarctica_years_end, hence the **. There are several ways you could mess up this declaration. For example, you could omit the const, forget an * or two, transpose letters, or otherwise mangle the structure type. Here is an instance for which the C++11 version of auto is convenient. The compiler is perfectly aware of what type arp is, so it can deduce the correct type for you:

```cpp
auto ppb = arp; // C++11 automatic type deduction
```

In the past, the compiler used its knowledge of the correct type to complain about errors you may have made in the declaration; now it can let its knowledge work for you. How can you use ppa to access data? Because ppa is a pointer to a pointer to a structure, *ppa is a pointer to a structure, so you can use it with the indirect membership operator:

```cpp
std::cout << (*ppa)->year << std::endl;
std::cout << (*(ppb+1))->year << std::endl;
```

Because ppa points to the first member of arp, *ppa is the first member, which is &s01. So (*ppa)->year is the year member of s01. In the second statement, ppb+1 points to the next element, arp[1], which is &s02. The parentheses are needed to get the correct associations. For example, *ppa->year would attempt to apply the * operator to ppa->year, which fails because the year member is not a pointer.

Is all this really true? Listing 4.23 incorporates all the preceding statements into a short program.

## Listing 4.23 **mixtypes.cpp**

```cpp
// mixtypes.cpp -- some type combinations
#include <iostream>

struct antarctica_years_end
{
    int year;
    /* some really interesting data, etc. */
};

int main()
```
