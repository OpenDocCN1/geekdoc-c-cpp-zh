
- **Note**
  - Any member in a structure can be accessed by relating them to the structure variable with a dot operator.
  - Structures that are not explicitly initialized by the programmer are, by default, initialized by the system. In most of the C compilers, for integer and float data type members, the default value is zero and for char and string type members, the default value is '\0'.
  - Comparing one structure variable with another is not allowed in C. However, when comparing two structures, one can compare the individual fields in the structure.

### 14.2.5 Typedef and Its Use in Structure Declarations

The typedef keyword allows the programmer to create a new data type name for an existing data type. No new data type is produced but an alternate name is given to a known data type. The general form of the declaration statement using the typedef keyword is given as follows.

```c
typedef <existing data type> <new data type>;
```

The typedef statement does not occupy storage; it simply defines a new type. typedef statements can be placed anywhere in a C program as long as they come prior to their first use in the code.

The following examples show the use of typedef.

```c
typedef int id_number;
typedef float weight;
typedef char lower_case;
```

In the preceding example, id_number is the new data type name given to data type int, while weight is the new data type name given to data type float and lower_case is the new data type name given to data type char. Therefore, the following statements

```c
id_number vinyal, komal, jaspal;
weight apples, pears, mangoes;
lower_case a, b, c;
```

mean that vinyal, komal, and jaspal are variable names that are declared to hold int data type. The new data type, id_number, suggests that the data content of the variable names vinyal, komal, and jaspal are integers and that it gives their identification number. The two other examples shown also carry similar meanings. Therefore, by the typedef keyword, the suggested use of type names can be understood easily. This is one of the benefits of using the typedef keyword. Moreover, typedef makes the code more portable.

Complex data type like structure can use the typedef keyword. For example,

```c
typedef struct point
{
    int x;
    int y;
} Dot;
Dot left, right;
```

shows that left and right are the structure variables of structure type point.

When typedef is used to name a structure, the structure tag name is not necessary. Such an example follows.

```c
typedef struct   /* no structure tag name used */
{
    float real;
    float imaginary;
} complex;      /* means complex number */
complex u, v;
```

The preceding example declares u and v as complex numbers having a real part and an imaginary part. The following are some examples involving structures and typedef.

## EXAMPLES

15. Write a program that prints the weight of various sizes of fruits.

```c
#include <stdio.h>
typedef struct fruits
{
    float big;
    float medium;
    float small;
} weight;
int main()
{
    weight apples = {200.75, 145.5, 100.25};
    weight pears = {150.50, 125.50};
    weight mangoes = {1000, 567.25, 360.25};
    printf("\n\n apples: big %7.2fkg, medium %7.2fkg, small %7.2fkg", apples.big, apples.medium, apples.small);
    printf("\n\n pears: big %7.2fkg, medium %7.2fkg, small %7.2fkg", pears.big, pears.medium, pears.small);
    printf("\n\n mangoes: big %7.2fkg, medium %7.2fkg, small %7.2fkg", mangoes.big, mangoes.medium, mangoes.small);
    return 0;
}
```

**Output**

```text
apples: big 200.75kg, medium 145.50kg, small 100.25kg
pears: big 150.50kg, medium 125.50kg, small 0.00kg
mangoes: big 1000.00kg, medium 567.25kg, small 360.25kg
```

16. Write a program that prints the x-y coordinates of the two ends of a line.

```c
#include <stdio.h>
typedef struct          /* no tag */
{
    int x;
    int y;
} Dot;             /* a new type name */
Dot left, right;
                    /* declaring structures "left"
                       and "right" */

int main()
{
    printf("\n Enter x & y coordinates of left and\
right:");
    scanf("%d %d %d %d", &left.x, &left.y, &right.x,\
&right.y);
    printf("\n left: x=%d, y=%d, right: x=%d, y=%d",\
    left.x, left.y, right.x, right.y);
    return 0;
}
```

**Output**

```text
Enter x & y coordinates of left and right:4 20 30 20
left: x=4, y=20, right: x=30, y=20
```

### 14.2.6 Nesting of Structures

A structure can be placed within another structure. In other words, structures can contain other structures as members. A structure within a structure means nesting of structures. In such cases, the dot operator in conjunction with the structure variables are used to access the members of the innermost as well as the outermost structures.

### EXAMPLE

17. Write a program to demonstrate nesting of structures and accessing structure members.

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
    } invar;
                        /* structure_variable of inner structure */
};
int main()
{
    struct outer outvar;
                        /* declaring structure_variable of outer */
    outvar.out1 = 2;    /* assigning values to member */
    outvar.out2 = 10.57;
                        /* assigning values to member */
    outvar.invar.in1 = 2 * outvar.out1;
    outvar.invar.in2 = outvar.out2 + 3.65;
    printf(" out1=%d, out2=%6.2f, in1=%d, in2=%6.2f",\
    outvar.out1, outvar.out2, outvar.invar.in1,\
    outvar.invar.in2);
    return 0;
}
```

**Output**

```text
out1=2, out2= 10.57, in1=4, in2= 14.22
```

It must be noted that an innermost member in a nested structure can be accessed by chaining all the concerned structure variables, from outermost to innermost, with the member using the dot operator. This technique has been used in the previous example, where the innermost members in1 and in2, belonging to the structure inner, are assigned values.

What happens when the first structure type is declared outside and before the second structure type and is incorporated as a member of the second structure type? The following example depicts what happens in such a case. The structure members are accessed in the same way as was done in the earlier example.

### EXAMPLE

18. Write a program to demonstrate nesting of structures, accessing structure members, and using structure type declaration different from that in the previous example.

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
    outs.out1 = 2;          /* assigning values to
                               members */
    outs.out2 = 10.57;      /* assigning values to
                               members */
    outs.inf.in1 = 2 * outs.out1;
    outs.inf.in2 = outs.out2 + 3.65;
    printf(" out1=%d, out2=%6.2f, in1=%d, in2=%6.2f",\
    outs.out1, outs.out2, outs.inf.in1,\
    outs.inf.in2);
    return 0;
}
```

**Output**

```text
out1=2, out2= 10.57, in1=4, in2= 14.22
```

It must be understood that, in principle, structures can be nested indefinitely. Statements like the following are syntactically acceptable, but are bad style.

```c
Outer_struct_variable.member1.member2.member3.member4.member5 = 3;
```

However, one may be curious to know what happens if a structure contains an instance of its own type. The following example may be examined in this context.

```c
struct compute
{
    int int_member;
    struct compute self_member;
};
```

For the computer to compile a statement of this type, it would theoretically need an infinite amount of memory. In practice, however, the programmer will simply receive an error message along the following lines.

```text
In function 'main':
field self_member has incomplete type
```

The compiler conveys to the programmer that 'self_member' has been declared before its data type 'compute' has been fully declared. Since the programmer declares 'self_member' in the middle of declaring its own data type, this is quite natural.

### 14.2.7 Arrays of Structures

Just as there can be arrays of basic types such as integers and floats, so also there can be *arrays of structures*. This means that the structure variable would be an array of objects, each of which contains the member elements declared within the structure construct. The general construct for declaration of an array of structures is given as follows.

```c
struct <structure_tag_name>
{
    <data_type member_name1>;
    <data_type member_name2>;
    :
    :
} <structure_variable>[index];
```

or

```c
struct <structure_tag_name> <structure_variable>[index];
```

Figure 14.3 depicts the arrays formed for the array objects declared to be of type structure_tag_name having structure_variable as its name. Here, the term 'index' specifies the number of array objects.

![](img/57923fbb5279ba385cf6b5a2e2c2ea5f_422_0.png)

### EXAMPLE

19. Write a program to illustrate the use of array of structures.

```c
#include <stdio.h>
struct test1
{
    char a;
    int i;
    float u;
} m[3];
int main()
{
    int n;
    for(n = 0; n <= 2; ++n)
    {
        printf("\n Enter ch, in, fl:");
        fflush(stdin);      /* clear stdin stream */
                            /* input the values of array
                               of structures */
        scanf("%c %d %f", &m[n].a, &m[n].i, &m[n].u);
        fflush(stdout);     /* clear stdout stream */
                            /* output the values of array
                               of structures */
        printf("\n a=%c, i=%d, u=%f", m[n].a, m[n].i, m[n].u);
    }
    return 0;
}
```

**Output**

```text
Enter ch, in, fl:g 45 678.1956
a=g, i=45, u=678.195618
Enter ch, in, fl:j 76 345.5674
a=j, i=76, u=345.567413
Enter ch, in, fl:k 69 123.333547
a=k, i=69, u=123.333549
```
