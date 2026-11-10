
## 14.2.8 Initializing Arrays of Structures

Initializing arrays of structures is carried out in much the same way as arrays of standard data types. A typical construct for initializing an array of structures would appear as follows.

```c
struct <structure_tag_name >
            /* structure declaration */
{
    <data_type member_name_1>;
    <data_type member_name_2>;
    .
    .
    <data_type member_name_n>;
};
/* declaration of structure array and initialization */
struct <structure_tag_name> <structure_variable>[N]=
{
    {constant01,constant02,__________,constant0n},
    {constant11,constant12,__________,constant1n},
    .
    .
    {constantN1,constantN2,__________,constantNn}};
```

The following example shows how the initialization technique referred to above is implemented.

### EXAMPLE

- 20. Write a program to print the tickets of the boarders of a boat using array of structures with initialization in the program.

```c
#include <stdio.h>
struct boat        /** declaration of structure **/
{
    char name[20];
    int seatnum;
    float fare;
};
int main()
{
    int n;
    struct boat ticket[4]= {{"Vikram", 1,15.50},\
                            {"Krishna", 2,15.50}, {"Ramu", 3,25.50},\
                            {"Gouri", 4,25.50}};
                        /** initialization **/
    printf("\n Boarder Ticket num. Fare");
    for(n=0;n<3;n++)
    printf("\n %s %d %f",ticket[n].name,ticket[n].\
            seatnum,ticket[n].fare);
    return 0;
}
```

### Output

```text
    Boarder Ticket num. Fare
    Vikram 1 15.500000
    Krishna 2 15.500000
    Ramu 3 25.500000
    Gouri 4 25.500000
```

## 14.2.9 Arrays within the Structure

There can be arrays within a structure. In other words, any member within a structure can be an array. When arrays are used in a structure, they are accessed and initialized in a way similar to that illustrated in Example 20. In this example, name[20] is an array within the structure boat. Initialization of the structure means initialization of members: name[20], seatnum, and fare. The printf() statement within the for loop uses the dot operator to access the member name[20], an array, within the structure boat. Therefore, this example demonstrates how an array is used within a structure and also shows the way to initialize it.

> **Note**
>
> - By using typedef, no new data type is produced but an alternate name is given to a known data type.
> - typedef statements can be placed anywhere in a C program as long as they come prior to their first use in the code.
> - An innermost member in a nested structure can be accessed by chaining all the concerned structure variables, from outermost to innermost, with the member using the dot operator.

## 14.2.10 Structures and Pointers

At times, it is useful to assign pointers to structures. A pointer to a structure is not itself a structure, but merely a variable that holds the address of a structure. This pointer variable takes four bytes of memory just like any other pointer in a 32-bit machine. Declaring pointers to structures is basically the same as declaring a normal pointer. A typical construct for declaring a pointer to a structure will appear as follows.

```c
struct <structure_tag_name >
            /* structure declaration */
{
    <data_type member_name_1>;
    <data_type member_name_2>;
    .
    .
    <data_type member_name_n>;
}*ptr;

or

struct <structure_tag_name>
{
    <data_type member_name_1>;
    <data_type member_name_2>;
    .
    .
    <data_type member_name_n>;
};
struct <structure_tag_name> *ptr;
```

This pointer, `*ptr`, can be assigned to any other pointer of the same type, and can be used to access the members of its structure. To access the members within the structure, the dot operator is used with the pointer variable. For example, to enable the pointer variable to access the member `member_name_1`, the following construct is used.

```c
(*ptr).member_name_1
```

The bracket is needed to avoid confusion about the `*` and `.` operators. If the bracket around `*ptr` is done away with, the code will not compile because the `.` operator has a higher precedence than the `*` operator. It gets tedious to type so many brackets when working with pointers to structures. Hence, C includes a shorthand notation that does exactly the same thing.

```c
ptr-> member_name_1
```

This is less confusing and a better way to access a member in a structure through its pointer. The `->` operator, an arrow made out of a minus sign and a greater than symbol, enables the programmer to access the members of a structure directly via its pointer. This statement means the same as the last line of the previous code example, but is considerably clearer. The `->` operator will come in very handy when manipulating complex data structures.

For initializing the structure members through a pointer to the structure, any one of the following constructs is used.

```c
(*ptr).member_name_x = constant;

or

ptr-> member_name_x = constant;
```

where x is 1 to N, and N is the total number of members in the structure. The following example uses pointer to structure.

### EXAMPLE

- 21. Write a program using a pointer to structure illustrating the initialization of the members in the structure.

```c
#include <stdio.h>
#include <conio.h>
struct test1
        /* declaration of structure “test” */
{
    char a;
    int i;
    float f;
};
int main()
{
    struct test1 *pt; /* declaring pointer to the
                         structure */
    clrscr();
    pt->a='k';             /* initializing char a */
    pt->i=15;              /* initializing int i */
    pt->f=27.89;           /* initializing float f */
    printf("\n a=%c, i=%d, f=%f",pt->a,pt->i,pt->f);
    printf("\n Enter new char, int, float:");
    scanf("%c %d %f",&pt->a,&pt->i,&pt->f);
                         /* input for members */
    printf("\n a=%c, i=%d, f=%f",pt->a,pt->i,pt->f);
    return 0;
}

                         /* function to link-in floating
                            point emulator */

void linkfloat()
{
    float a,*x;
    x=&a;
    a=*x;
}
```

### Output

```text
a=k, i=15, f=27.899999
Enter new char, int, float: d 45 67.53
a=d, i=45, f=67.529999
```

The function `linkfloat()` needs to be explained. If this function is not included, the following error is generated.

`scanf: floating point format not linked`

`Abnormal program termination`

A similar message saying “floating point not loaded” is printed by the Microsoft C run-time system when the software needs a numeric coprocessor but the computer does not have one installed. One may fix it by recompiling the program using the floating-point emulation library.

A floating-point emulator is used to manipulate floating point numbers in run-time library functions such as `scanf()` and `atof()`. When compiling the source program if the compiler encounters a reference to the address of a float, it sets a flag to have the linker link in the floating-point emulator. In some cases in which reference to float seems to guess wrongly when the program uses floating point formats in `scanf()` but does not call any other floating point routines. The function `linkfloat()` forces linking of the floating point emulator into an application. There is no need to call this function. Just include it anywhere in the program. This provides a solid clue to the Borland PC linker that the floating-point library is needed.

Another workaround is to define a function in a module that will be included in the link. The function is as follows:

```c
static void forcefloat (float *p)
{
    float f=*p;
    forcefloat(&f);
}
```

The problem can also be solved by including the following code in the program instead of the functions such as `linkfloat()` or `forcefloat()`.

```c
#include <math.h>
double dummy = sin(0.0);
```

This code forces the compiler to load the floating-point version of `scanf()`.

### EXAMPLES

- 22. Write a program using a pointer to structure illustrating the initialization of the members in the structure using a different technique to avoid the floating point error problem.

```c
#include <stdio.h>
struct test1
{
    char a;
    int i;
    float f;
};
int main()
{
    float x;
    struct test1 *q, p;
    clrscr();
    printf("\n Enter char, int, float:");
    scanf("%c %d", &p.a, &p.i);
    scanf("%f", &x);
    p.f = x;
    q = &p;
    printf("\n a=%c, i=%d, f=%f", q->a, q->i, q->f);
    q = NULL;
    return 0;
}
```

### Output

```text
Enter char, int, float: g 32 87.64
a=g, i=32, f=87.639999
```

- 23. Write a program using a pointer to structure illustrating the initialization of the members in the structure using `malloc()`.

```c
#include <stdio.h>
struct A
{
    char ch;
    int in;
    float f;
};
int main()
{
    struct A *sp;
    int n, i;
    printf("\n How many members:");
    scanf("%d", &n);
    sp = (struct A *)malloc(n*sizeof(struct A));
    if(sp==NULL)
    {
        printf("\n Memory allocation unsuccessful");
        exit(0);
    }
    for(i=0;i<n;++i)
    {
        printf("\n Enter ch, in and f:");
        fflush(stdin);
        scanf("%c %d %f", &sp[i].ch, &sp[i].in, &sp[i].f);
    }
    for(i=0;i<n;++i)
        printf("\n ch=%c in=%d f=%f", sp[i].ch,\
            sp[i].in, sp[i].f);
    return 0;
}
void linkfloat()
{
    float a=0.0, *x;
    x=&a;
    a=*x;
}
```

### Output

```text
How many members:2
Enter ch, in and f: g 31 76.56
Enter ch, in and f: k 32 78.34
ch=g in=31 f=76.559998
ch=k in=32 f=78.339996
```

There are many reasons for using a pointer to a struct. One of them is to make two-way communication possible within functions. This aspect is explained with examples in the following section.

## 14.2.11 Structures and Functions

An entire structure can be passed as a function argument just like any other variable. When a structure is passed as an argument, each member of the structure is copied. In fact, each member is passed by value. In case the member is an array, a copy of this array is also passed. This can prove to be inefficient when structures are large or functions are called frequently. Passing and working with pointers to large structures may be more efficient in such cases. The general construct for passing a structure to a function and returning a structure is

```c
struct structure_tag function_name(struct structure_tag structure_variable);
```

Several variations in this construct are made while using this construct. In some cases, the function may receive a structure but may return void or some other data type. In another implementation, no parameters may be passed to a function but it may return a structure. Another option may be to pass a pointer to a structure and return any data type,
