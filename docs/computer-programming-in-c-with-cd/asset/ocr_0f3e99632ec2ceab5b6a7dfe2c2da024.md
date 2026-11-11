In the preceding snippet, the structure user_var occupies eight bytes in memory—four bytes are used for the float variable f and four bytes are used for the character variable ch. The instance s1, of the user_var structure, uses the memory allocations, as shown in Figure 14:

![](bbox=[0.152, 0.177, 0.858, 0.318])

Now, modify the preceding code snippet. However this time, define the user_var as a union, as given in the following code snippet:

```
```cpp
union user_var
{
    float f;
    char ch[4];
} s1;
```
```

In the preceding code snippet, the union user_var occupies only 4 bytes of memory as the memory required for the float variable and char variable share the memory between them, as shown in Figure 15:

![](bbox=[0.152, 0.536, 0.858, 0.681])

As a result, the less amount of memory of the computer system is used when you declare s1 variable using union. You can access the union member element by using the dot (.) operator. For example, to access f member element of the union variable s1, you can use s1.f.

Listing 13 shows the process to declare a user-defined data type through union (you can find the MyUnion.cpp file on the CD in the code\chapter5 folder):

# **▶ Listing 13: Declaring and Using a Union**

```
```cpp
#include <iostream.h>

struct struct_user_var
{
    float f;
    char ch[4];
}struct_var;
union union_user_var
```
```