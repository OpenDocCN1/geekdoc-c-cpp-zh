
### PROGRAM 14.13a: student_management.c (Pre-main and main sections)

```c
add_student(stud);
average = display_marks(stud);
printf("Average marks of class = %.2f\n", average);
fputs("\nEnter Roll No: ", stdout);
scanf("%d", &roll_no);
q = search_student(stud, roll_no);
if (q != NULL)
    printf("%-20s %4d %5hd %5hd %5hd %6hd\n", q->name, q->roll_no,
    q->marks[0], q->marks[1], q->marks[2], q->marks[3]);
else
    fputs("Not found", stdout);
return 0;
}
```

### PROGRAM 14.13b: student_management.c (The function definitions)

```c
void add_student(STUDENT p[])
{
    short i = 0;
    do {
        fputs("Name: ", stdout);
        if (scanf("%[^\n]", p->name) != 1)
            break;
        fputs("Roll No: ", stdout);
        scanf("%d", &p->roll_no);
        fputs("Marks in 3 subjects: ", stdout);
        scanf("%hd%hd%hd", &p->marks[0], &p->marks[1], &p->marks[2]);
        p->marks[3] = p->marks[0] + p->marks[1] + p->marks[2];
        FLUSH_BUFFER
        p++;                           /* Moves pointer to next element */
    } while (i++ < COLUMNS - 1);       /* Won't accept more than 50 records */
    return;
}

float display_marks(STUDENT p[])
{
    short i; int total_marks = 0;
    fputs("Name           Roll No Phys Chem Maths Total\n", stdout);
    for (i = 0; i < COLUMNS; i++, p++) {
        if (p->roll_no > 0) {
            printf("%-20s %4d %5hd %5hd %5hd %6hd\n", p->name, p->roll_no,
            p->marks[0], p->marks[1], p->marks[2], p->marks[3]);
            total_marks += p->marks[3];
        }
        else
            break;
    }
    return (float) total_marks / i;   /* Returns average of total marks */
}
```

```c
STUDENT *search_student(STUDENT p[], int f_roll_no)
{
    short i;
    for (i = 0; i < COLUMNS; i++, p++)
        if (p->roll_no == f_roll_no)
            return p;
    return NULL;
}
```

### PROGRAM OUTPUT: student_management.c

```text
Name: Sohini Gupta
Roll No: 1111
Marks in 3 subjects: 70 85 90
Name: Shiksha Agarwal
Roll No: 2222
Marks in 3 subjects: 55 75 60
Name: Juhi Parekh
Roll No: 3333
Marks in 3 subjects: 95 90 98
Name: [Enter]
```

| Name | Roll No | Phys | Chem | Maths | Total |
|---|---:|---:|---:|---:|---:|
| Sohini Gupta | 1111 | 70 | 85 | 90 | 245 |
| Shiksha Agarwal | 2222 | 55 | 75 | 60 | 190 |
| Juhi Parekh | 3333 | 95 | 90 | 98 | 283 |

```text
Average marks of class = 239.33

Enter Roll No: 2222
Shiksha Agarwal     2222    55    75     60    190
```

**Pre-main and main Sections** The array, stud, is first initialized by setting the first element to zero. (Setting only the first member of this element using {""} would have been enough.) The program can now evaluate the number of utilized array elements by checking the roll_no field. The three functions (discussed next) are invoked sequentially.

**Function Definitions** All three functions use the parameter STUDENT p[] to represent the array of structures. However, p is actually a pointer to the beginning of the array, stud, defined in main. The functions use p for navigating the array; every invocation of p++ advances the pointer to the next array element.

The **add_student** function invokes **scanf** twice in a **do-while** loop to accept user data. Because **scanf** returns the number of items successfully read, pressing [Enter] without keying in data terminates this loop. The loop will otherwise terminate after 50 records have been entered. **add_student** also sets the fourth element of the marks array to the sum of the first three elements.

The **display_marks** function uses a for loop to display each record. Even though the loop can iterate 50 times, it terminates prematurely when roll_no is no longer a positive integer. The function also returns the average marks of the class. The **search_student** function searches for a roll number and returns a pointer to the matching array element if the number is found.

## 14.11 UNIONS

When searching a database using a person’s id, you must have often wanted to search by name as well. That is possible if the two attributes are held in a union, a data type that resembles a structure in form. A union comprises two or more members that share the same memory, with the most recent assignment to a member being active at any instant. Consider the following declaration and definition of a union:

```c
union uemp {
    short emp_id;
    char name[30];
} u;
```

Declares union of type uemp  
Defines union variable u of type uemp

A union is declared, defined and accessed exactly like a structure. The previous statement declares a two-member union named uemp and simultaneously defines the union variable u. The members are accessed as u.emp_id and u.name. However, both members share a single memory region and you can correctly access only one member at a time—the one that was last assigned. For instance, you can assign and access emp_id in this way:

```c
u.emp_id = 1234;
printf("%hd:\n", u.emp_id);
```

Prints 1234

If you subsequently assign u.name, everything will work as expected:

```c
strcpy(u.name, "George Martin");
printf("%s:\n", u.name);
```

Prints George Martin

However, u.name overwrites the memory segment previously used by u.emp_id, so you can’t access the latter now (even though the compiler won’t complain):

```c
printf("%hd:\n", u.emp_id);
```

Output is undefined

Barring this essential difference, unions are handled like structures. You can separate the definition of a union from its declaration, and typedef works in identical manner on unions. You can create pointers to unions and also create arrays of unions. Because of these similarities, unions are most useful when they are used as members of structures or comprise structures as members.

> **Takeaway:** The members of a union can’t be accessed simultaneously because they share a single memory region. You can correctly access only the member that was last assigned.

### 14.11.1 Unique Attributes of Unions

Apart from the difference in the way structures and unions use computer memory, there are some unique features possessed by unions. The following features need to be kept in mind:

- *All members of a union can’t be initialized simultaneously.* This is obvious because only one member is correctly accessible at any point of time. You can initialize only the first member:

    ```c
    union uemp u2 = {1234};
    ```

    Initializes only emp_id

- The size of a union is determined by the size of the member having the largest footprint in memory. For uemp, this would be 30, the size of the name field. As with structures, issues related to alignment on word boundaries (14.3) may increase this number.

- The compiler doesn’t output an error when you access a member that was not the last one to be assigned. A programmer must keep track of the member that is active at any instant.

- You can use a union to assign a value to a member and read it back using a different member. For instance, you can store a string in a char array and then examine its bit pattern by reading the int member of the union.

A union can easily determine whether a machine is little-endian or big-endian. In a big-endian machine, the most significant bit is stored first while the reverse is true for little-endian machines. However, unions are mainly used as memory-saving objects.

> Tip: It is often necessary to include a member that saves the type of information currently saved in the union. This value could be 0, 1, 2, etc., which could be used by the program to determine the currently active member.

### 14.11.2 intro2unions: An Introductory Program

Program 14.14 defines two union variables, u1 and u2, based on the ucust template. u1 is not initialized but u2 is initialized with a single value which is automatically assigned to the first member (aadhar_id). The remaining two members are assigned later. Note that after u2.name has been assigned, u2.aadhar_id and u2.cust_id evaluate to incorrect values.

```c
/* intro2unions.c: Demonstrates basic features of unions. */
#include <stdio.h>
#include <string.h>

int main(void)
{
    union ucust {                         /* Declares union of type ucust */
        int aadhar_id;                    /* Only one of these three members ... */
        short cust_id;                    /* ... is active at any time. But ... */
        char name[30];                    /* ... this one determines size of u1. */
    } u1;                                 /* Defines union variable of type ucust */

    printf("Size of u1 is %d\n", sizeof(u1));

    union ucust u2 = {1234567890};        /* Initializes a second variable */
    printf("u2.aadhar_id = %d\n", u2.aadhar_id);

    u2.cust_id = 3456;
    printf("u2.cust_id = %d\n", u2.cust_id);
    strcpy(u2.name, "Paul McCartney");
```
