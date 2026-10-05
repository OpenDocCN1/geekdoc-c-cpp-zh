# 368 Introduction to C++

Let's explain the program. Since d contains three integer members, the allocated memory is 3*4 = 12 bytes. However, the allocated size may be larger than the sizes of the members added together. For example, if we change the type of the day member from int to char, the program may display again 12, not 9 as expected.

This can happen if the compiler requires each member be stored in an address multiple of some number (typically four). This requirement may make it faster for access to the structure members. If we assume that the month member should be stored in an address multiple of four, the compiler would also allocate three bytes, a "hole", right after the day member. In that case, the program would display 12. Holes may exist between members and at the end of the structure, but not at the beginning.

I won't get into details, but if you write an application that uses many structures and the memory is limited, keep in mind that the order of the declarations might affect the alignment and create holes.

```
struct S1
{
    char c;
    double d;
    short s;
}

struct S2
{
    double d;
    short s;
    char c;
}
```

Although the members are the same, reordering the members, from the larger to smaller may save memory. For example, an S1 variable might allocate more bytes than an S2 variable, that is 24 bytes instead of 16, in case the compiler leaves holes to align the members to the larger type (i.e., double). And if we have an array of S1 elements, the "holes" remain between the successive elements, to keep the alignment.

> To calculate the memory size of a structure variable always use the sizeof operator; don't add the sizes of its members.

Although it is not often used, it is good to know about the offsetof. It is defined in cstdef and takes two arguments. The first one is the type of the structure and the second one of a member. The macro calculates the number of bytes from the beginning of the structure up to the member. For example, consider the S2 structure. Since C++ guarantees that the address of the first member is the same as the address of its entry, the statement:

```
cout << offsetof(S2, d); outputs 0.
```

If we replace d with s, the code outputs 8. Because a structure may contain holes, if you write an application to run in different platforms and member alignment matters might be useful to check the portability of your program. Note that the use of offsetof imposes restrictions that you should consider before using it.

C++ provides the alignof operator, which returns the alignment, in bytes, of the indicated type. For example:

```
double d;
cout << alignof(d) << '\\n';
```

The code outputs the alignment of the double type (e.g., 8).