tag of a structure. For the same reason, the same member names can be reused in other structures. For
example:

```
struct Person
{
    string name;
    int tax_num;
    string addr;
};
```

These three members have no relation with the respective members of the Company type. As another
example, check the following declarations:

```
int a;
struct S1 { int a[5]; } s1;
struct S2 { int *a; } s2;
```

Next, you'll learn how to write s1.a[0] = a; or s2.a = &a or s2.a = s1.a; without any problem.
Although a structure type is completed with the right brace), a structure can contain a pointer to
instance of itself because C++ allows the declaration of pointers to incomplete types. For example:

```
struct A
{
    A *p;
};
```

When a structure variable is declared, the compiler allocates memory to store its members in the
order which they are declared. For example, the following program displays how many bytes the
variable allocates

```
#include <iostream> // Example 13.1

struct Date
{
    int day;
    int month;
    int year;
};

int main()
{
    Date d;

    std::cout << sizeof(d) << '\n';
    return 0;
}
```

For those who know structures from C, a C structure has similar properties to a C++ structure with
some differences. One difference is that in C++ the struct does not need to be added in the dec-
lclaration of variables. In C++, the tag can be used like a basic type. This change emphasizes the fact
t declaration of a structure defines a new type. Another difference is that in C++ the structure can
also contain functions. However, we will not see such examples of structures, because, we'll see in
Chapter 17, the type that is usually chosen when we want to use functions is the class type and not the
structure. There are more differences; those two are the most important.