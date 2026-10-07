
# Chapter 4 Compound Types

## Note
Pointers are among the most powerful of C++ tools. They are also the most dangerous because they permit computer-unfriendly actions, such as using an uninitialized pointer to access memory or attempting to free the same memory twice. Furthermore, until you get used to pointer notation and pointer concepts through practice, pointers can be confusing. Because pointers are an important part of C++ programming, they weave in and out of future discussions in this book. This book discusses pointers several more times. The hope is that each exposure will make you more comfortable with them.

## Combinations of Types

This chapter has introduced arrays, structures, and pointers. These can be combined in various ways, so let's review some of the possibilities, starting with a structure:

```cpp
struct antarctica_years_end {
    int year;
    /* some really interesting data, etc. */
}
```

We can create variables of this type:
`antarctica_years_end s01, s02, s03; // s01, s02, s03 are structures`

We can access members using the membership operator:
`s01.year = 1998;`

We can create a pointer to such a structure:
`antarctica_years_end * pa = &s02;`

Provided the pointer has been set to a valid address, then we can use the direct membership operator to access members:
`pa->year = 1999;`

We can create arrays of structures:
`antarctica_years_end trio[3]; // array of 3 structures`

We then use the membership operator to access members of an element:
`trio[0].year = 2003; // trio[0] is a structure`

Here, trio is an array, but trio[0] is a structure, and trio[0].year is a member of ship structure. Because array name is a pointer, we can also use the direct member-operator:
`trio(opt+1)->year = 2004; // same as trio[1].year = 2004;`

We can create an array of pointers:
`const antarctica_years_end * arp[3] = {&s01, &s02, &s03};`

This is starting to look a bit complicated. How can we access data with this array?
Well, if arp is an array of pointers, then arp[1] must be a pointer, and we can use the direct membership operator with it to access a member:

```cpp
std::cout << arp[1]->year << std::endl;
```

We can create a pointer to point to:

```cpp
const antarctica_years_end **ppa = arp;
```

Here, arp is the name of array; hence, it is the address of its first element. But this first element is a pointer, so ppa has to be a pointer to a pointer to const antarctica_years_end, hence the \\*. There are several ways you could mess up this declaration. For example, you could omit the const, for an or two, transpose letters, or otherwise mangle the structure type. Here is an instance for which the C++11 version of auto is convert. The compiler is perfectly aware of what type arp is, so it can deduce the type for you:

```cpp
auto ppb = arp; // C++11 automatic type deduction
```

In the past, the compiler used its knowledge of the correct type to complain about errors you may have made in the declaration; now it can let its knowledge work for you. How can you use ppa to access data? Because ppa is a pointer to a pointer to a structure, so can use it with the direct membership:

```cpp
std::cout << (*ppa)->year << std::endl;
std::cout << (*ppb+1)->year << std::endl;
```

Because ppa points to the first member of arp, *ppa is the first member, which is &s01. So (*ppa)->year is the year member of s01. In the second statement, ppb+1 points to the next element, arp[1], which is &s02. The parentheses are needed to get the correct associations. For example, ppa->year would attempt to apply the * operator to ppa->year, which fails because the year member is not a pointer.
Is this really true?

Listing 4.23 incorporates all the preceding statements into a short:

Listing 4.23 mixtypes.cpp

```cpp
// mixtypes.cpp -- some combinations
#include <iostream>

struct antarctica_years_end
{
    int year;
    /* some interesting data, etc. */
};

int main()
{
  antarct_years_end s01, s02, s03;
  s01.year = 1998;
  antarct_years_end * pa = &s02;
  pa->year = 1999;
  antarct_years_end trio[3]; // array of 3 structures
  trio[0].year = 2003;
  std::cout << trio->year << std::endl;
  const antarctica_years_end * arp[3] = {&s01, &s02, &s03};
  std::cout << arp[1]->year << std::endl;
  const antarctica_years_end ** ppa = arp;
  auto ppb = arp; // C++11 automatic type deduction
  // or else use antarctica_years_end ** ppb = arp;
  std::cout << (*ppb)->year << std::endl;
  std::cout << (*(ppb+1))->year << std::endl;
  return 0;
}
```

The program compiles and works as promised.

## Array Alternatives

Earlier this chapter mentioned the vector and array template classes as alternatives to the built-in array. Let's take a brief look now how they are used and at some of the benefits of using them.

## The vector Template Class

The vector template class is similar to the string class in that it is a dynamic array. You can set the size of a vector object during runtime, and you can append new data to the end or insert new data in the middle. Basically, it's an alternative to using new to create a dynamic array. Actually, the vector class does use new and delete to manage memory, but it does so automatically.

At this time we won't venture deeply into what it means to be a template class. Instead, we'll look at a few basic practical matters. First, to use a vector object, you will need to include the header. Second, the vector identifier is part of the std namespace, so you can use it. Third, the vector uses a different syntax to indicate the number of elements. Fourth, the vector class uses a different syntax to indicate data. Here are some examples:

```cpp
#include <vector>
...
using namespace std;
vector<int> vi; // create a vector of ints
int n;
cin >> n;
vector<double> vd(n); // create a vector of size n
vector<double> vd = {1.1, 2.2, 3.3}; // initialize with values
```
