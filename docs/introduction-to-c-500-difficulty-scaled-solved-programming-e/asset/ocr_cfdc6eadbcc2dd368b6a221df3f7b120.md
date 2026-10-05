# 372 Introduction to C++

the case, the comparison to work in my platform and in customer's, because of different holes there. I'm scared by the thought that I had to look for that bug! Sometimes every programmer needs a shelter of luck, Gimme Shelter from Rolling Stones.

# Structure Containing Arrays

Since a structure may contain any type of data, it may contain one or more arrays. For example, what is the output of the following program?

```
#include <iostream> // Example 13.3
#include <string>
struct Student
{
    char name[50];
    float grd[2];
}
int main()
{
    Student s1, s2;
    strcpy(s1.name, "somebody");
    s1.grd[0] = 8.5;
    s1.grd[1] = 7.5;
    std::cout << s1.name << ' ' << s1.name[0] << ' ' << *s1.name << '\n';
    s2 = s1;
    std::cout << s2.name << ' ' << s2.grd[0] << ' ' << s2.grd[1] << '\n';
    return 0;
```

As you see, an array member is treated just like an ordinary array. For the example, strcpy(s1.name, "somebody"); copies the string somebody into name. The value of s1.name[0] becomes 's', s1.name[1] becomes 'o', and so on.

When using pointer arithmetic to handle the elements of an array, the * operator must precede the name of the structure. For example, since s1.name can be used as a pointer to its first character, *s1.name is equal to s1.name[0], *(s1.name+1) is equal to s1.name[1], and so on. As with ordinary arrays, the parentheses must be present for priority reasons. The assignment s2 = s1; copies the arrays. Therefore, the program outputs:

somebody s
somebody 8.5 7.5

# Structure Containing Pointers

A structure may contain one or more pointer members. A pointer member is treated just like an ordinary array. For example, what is the output of the following program?

```
#include <iostream> // Example 13.4
struct Student
{
    const char *name;
    float *avg_grd;
}
```