The instance “k” of the above defined structure is initialized by assigning value to individual named members. Here, a “dot” is used with the member’s name for assigning a value.

```
struct employee
{
    int emp_num;
    char designation[40];
    char kind_of_leave_applied[30];
    int number_of_days;
    int begin_date;
};
struct employee mangal_singh = {.kind_of_leave_applied = "Medical leave", .begin_date = 230910, .emp_num = 0691};
```

The “struct employee” defines a template of a structure with tagname “employee”. An instance of the structure is created by the statement “struct employee mangal_singh”. This instance is initialized. But, it may be noted that only some of the members are initialized. In the C compilers not complying to C99, such initialization is not allowed. For such compilers, while initializing an instance of a structure, the members of the structure have to be assigned a value or a character, whichever is appropriate, in the order of their definition and members not assigned are given default value of 0 or \0, which has been mentioned earlier. But, C99 allows the members of a structure to be initialized by name, which is shown in the above example.

Further, note that the order of the initialization is different from that of the definition of the members in the structure. The member “kind_of_leave_applied” is placed first, the member “begin_date” is placed second and the member “emp_num” is placed third, while the other remaining members are not assigned anything. Members uninitialized are filled up with the default value of 0. It may be observed that this not only decouples the order of the definition from the order of the initialization, but it is more readable. This means, the programmer only needs to fill out the portions of the structure that are presently relevant and is able to initialize the elements of the structure using the set notation without the need to remember the order of the elements of the structure. Also, if new elements to the structure are added in later versions, they get initialized to a known value.

Some examples using named initialization in structures are given below for getting more familiar with its applications.

# 9. Demonstration of named initialization in a structure.

```
#include<stdio.h>
struct
{
    float x, y, z;
} s = {.y = 0.6, .x = 2.7, .z = 14.6};
int main()
{
    float p,q,r;
    p= s.x + s.y + s.z;
    q= s.z*s.x;
    r= s.z/s.x;
    printf("\n p = %.2f",p);
    printf("\n q = %.2f",q);
    printf("\n r = %.2f",r);
    return 0;
}
```

```
printf("\n q = %.2f",q);
printf("\n r = %.2f",r);
return 0;
}
```

**Output**

p = 17.90
q = 39.42
r = 5.41

# 10. Another demonstration of named initialization in a structure.

```
#include<stdio.h>
struct test
{
    float x, y, z;
};
int main()
{
    float p,q,r;
    struct test s= { .y = 1.24, .x = 3.8, .z = 11.7};
    p= s.x + s.y + s.z;
    q= s.z*s.x;
    r= s.z/s.x;
    printf("\n p = %.2f",p);
    printf("\n q = %.2f",q);
    printf("\n r = %.2f",r);
    return 0;
}
```

**Output**

p = 16.74
q = 44.46
r = 3.08

# 11. One more demonstration of named initialization in a structure.

```
#include<stdio.h>
struct test
{
    float x, y, z;
};
int main()
{
    float p,q,r;
    struct test s;
    s.y= 5.94;
    s.z= 19.45;
    s.x= 23.17;
    p= s.x + s.y + s.z;
    q= s.z*s.x;
    r= s.z/s.x;
    printf("\n p = %.2f",p);
    printf("\n q = %.2f",q);
```