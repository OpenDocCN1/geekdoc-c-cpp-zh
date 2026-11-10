```
```c
{
    int x;
    int y;
}Dot;             /* a new type name */
Dot left,right;
                    /* declaring structures "left"
                       and "right" */

int main()
{
    printf("\n Enter x & y coordinates of left and\
right:");
    scanf("%d %d %d %d",&left.x,&left.y,&right.x,\
&right.y);
    printf("\n left: x=%d, y=%d, right: x=%d, y=%d",\
    left.x, left.y, right.x,right.y);
    return 0;
}
```
```

```
```
Output
Enter x & y coordinates of left and right:4 20 30 20
left: x=4, y=20, right: x=30, y=20
```
```

# ### 14.2.6 Nesting of Structures

A structure can be placed within another structure. In other words, structures can contain other structures as members. A structure within a structure means nesting of structures. In such cases, the dot operator in conjunction with the structure variables are used to access the members of the innermost as well as the outermost structures.

# **EXAMPLE**

17. Write a program to demonstrate nesting of structures and accessing structure members.

```
```c
#include <stdio.h>
struct outer    /* declaration of outer structure */
{
    int out1;           /* member of outer structure */
    float out2;         /* member of outer structure */
    struct inner        /* declaration of inner structure */
    {
        int in1;        /* member of inner structure */
        float in2;      /* member of inner structure */
    }invar;
                        /* structure_variable of inner structure*/
};
int main()
{
    struct outer outvar;
                        /* declaring structure_variable of outer */
    outvar.out1= 2;     /* assigning values to member */
    outvar.out2= 10.57;
                        /* assigning values to member */
    outvar.invar.in1= 2* outvar.out1;
    outvar.invar.in2= outvar.out2 + 3.65;
```
```

```
```c
    printf(" out1=%d, out2=%6.2f, in1=%d, in2=%6.2f",\
    outvar.out1, outvar.out2,outvar.invar.in1,\
    outvar.invar.in2);
    return 0;
}
```
```

```
```
Output
out1=2, out2= 10.57, in1=4, in2= 14.22
```
```

It must be noted that an innermost member in a nested structure can be accessed by chaining all the concerned structure variables, from outermost to innermost, with the member using the dot operator. This technique has been used in the previous example, where the innermost members in1 and in2, belonging to the structure inner, are assigned values.

What happens when the first structure type is declared outside and before the second structure type and is incorporated as a member of the second structure type? The following example depicts what happens in such a case. The structure members are accessed in the same way as was done in the earlier example.

# **EXAMPLE**

18. Write a program to demonstrate nesting of structures, accessing structure members, and using structure type declaration different from that in the previous example.

```
```c
#include <stdio.h>
struct first   /* declaration of first structure */
{
    int in1;                /* member of first */
    float in2;              /* member of first */
};
struct second /* declaration of second structure */
{
    int out1;               /* member of second */
    float out2;             /* member of second */
    struct first inf;       /* structure_variable of first
                               structure */
};
int main()
{
    struct second outs;     /* structure_variable of
                               second structure */
    outs.out1= 2;           /* assigning values to
                               members */
    outs.out2= 10.57;       /* assigning values to
                               members */
    outs.inf.in1= 2* outs.out1;
    outs.inf.in2= outs.out2 + 3.65;
    printf(" out1=%d, out2=%6.2f, in1=%d, in2=%6.2f",\
    outs.out1, outs.out2, outs.inf.in1,\
    outs.inf.in2);
    return 0;
}
```
```